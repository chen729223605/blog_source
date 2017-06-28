---
title: STM8学习笔记（一）
tags: STM8
grammar_cjkRuby: true
---

## 1 时钟
### 1.1 时钟初始化 使用内部始终 且不分频
```cpp
  // 用内部时钟 分频系数为1 
  CLK_HSIPrescalerConfig(CLK_PRESCALER_HSIDIV1);
  
```

## 2 GPIO

### 2.1 设置为输出模式
```cpp
  // LED初始化
  GPIO_Init(GPIOD, GPIO_PIN_0, GPIO_MODE_OUT_PP_LOW_FAST);
```

### 2.2 设置为输入模式
```cpp
GPIO_Init(SPI_NSS_GPIO_PORT, SPI_NSS_PIN, GPIO_MODE_IN_PU_NO_IT);
```

## 3 TIM
### 更新事件
产生途径
当TIM1_CR1寄存器的UDIS位为0 
1.  计数器溢出 且 重复计数器TIM1_RCR=0（一般这个都为0）
2.  将TIMX_EGR寄存器的UG位               通过软件或者从模式控制器 同样产生一个更新事件


事件作用
1. 所有寄存器被更新
2. 设置 TIMX_SR寄存器的UIF 为有效（当TIMX_CR1.URS==0时）
3. 自动装载影子寄存器被重新植入预装载寄存器的值（TIMX_ARR）
4. 预分频器的缓存器被置入预装载寄存器的值（TIMX_PSC）

### 配置注意点
- 预装载允许位 TIM1_CR1.ARPE位要注意 默认情况下是0 关闭的 向ARR寄存器写值的时候直接写到影子寄存器

### 3.1 设置捕获比较通道4 输出PWM波
- 用库函数配置TIM1的捕获比较通道
- 在输出之前 要先配置PC4 为推挽输出模式
- 时钟为输入时钟的2分频 输入时钟为系统时钟16M  即 时钟为8M

```cpp
  //复位
  TIM1_DeInit();
  // 时钟初始化 不分频 向上计数 自动重装值 49999，重复计数值0
  TIM1_TimeBaseInit(1,TIM1_COUNTERMODE_UP,49999,0);
  
  /* 输出比较通道 3 初始化，匹配时输出电平翻转，启用输出比较， 禁
  用输出比较互补输出，脉宽 5000，输出比较极性位低电平，互补输出比较极性高电平，输出比较空闲状
  态高电平，互补输出比较空闲状态低电平*/
//  TIM1_OC3Init(TIM1_OCMODE_TOGGLE,TIM1_OUTPUTSTATE_ENABLE,TIM1_OUTPUTNSTATE_DISABLE,
//               5000-1,TIM1_OCPOLARITY_LOW,TIM1_OCNPOLARITY_HIGH,TIM1_OCIDLESTATE_SET,
//               TIM1_OCNIDLESTATE_RESET);
  
  /* 输出比较通道 4 初始化，匹配时输出电平翻转，启用输出比较， 禁
     用输出比较互补输出，脉宽 5000，输出比较极性位低电平，互补输出比较极性高电平，输出比较空闲状
     态高电平，互补输出比较空闲状态低电平*/
  TIM1_OC4Init(TIM1_OCMODE_TOGGLE,TIM1_OUTPUTSTATE_ENABLE,
               5000-1,TIM1_OCPOLARITY_LOW,TIM1_OCIDLESTATE_SET);
  // 使能计数器
  TIM1_Cmd(ENABLE);

  // 输出比较4预装载使能
  TIM1_OC4PreloadConfig(ENABLE);
  
  // 使能TIM1输出
  TIM1_CtrlPWMOutputs(ENABLE); 

```

### 3.2 定时器更新中断

```cpp

  //复位
  TIM1_DeInit();
  
  // 时钟初始化 16分频 向上计数 自动重装值 49999，重复计数值0
  TIM1_TimeBaseInit(16-1,TIM1_COUNTERMODE_UP,49999,0);
  
  // 开启中断
  TIM1_ITConfig(TIM1_IT_UPDATE,ENABLE);
 
  // 使能计数器
  TIM1_Cmd(ENABLE);
```

中断程序
```cpp
/**
  * @brief  Timer1 Update/Overflow/Trigger/Break Interrupt routine.
  * @param  None
  * @retval None
  */
INTERRUPT_HANDLER(TIM1_UPD_OVF_TRG_BRK_IRQHandler, 11)
{
  /* In order to detect unexpected events during development,
     it is recommended to set a breakpoint on the following instruction.
  */
  if(TIM1_GetITStatus(TIM1_IT_UPDATE) == SET){
  
  static uint8_t time_50ms=0;
  time_50ms++;
  
  if(time_50ms%10==0)
    GPIO_WriteReverse(GPIOD,GPIO_PIN_0);
  
   TIM1_ClearITPendingBit(TIM1_IT_UPDATE);
  }
}
```

## 4 UART

### 4.1 串口初始化


```cpp
void InitUart(void){
  UART2_DeInit();
  UART2_Init(115200,UART2_WORDLENGTH_8D,UART2_STOPBITS_1,UART2_PARITY_NO,UART2_SYNCMODE_CLOCK_DISABLE,UART2_MODE_TXRX_ENABLE);
  UART2_ITConfig(UART2_IT_RXNE_OR, ENABLE);
  UART2_Cmd(ENABLE);
}

```

## 5 SPI 


### 5.1 SPI从机

初始化程序如下
```cpp
/**
* @brief spi初始化
* @note cubemx配置生成的spi初始化如下 

        
static void MX_SPI1_Init(void)
{

  hspi1.Instance = SPI1;
  hspi1.Init.Mode = SPI_MODE_MASTER;
  hspi1.Init.Direction = SPI_DIRECTION_2LINES;
  hspi1.Init.DataSize = SPI_DATASIZE_8BIT;
  hspi1.Init.CLKPolarity = SPI_POLARITY_LOW;
  hspi1.Init.CLKPhase = SPI_PHASE_2EDGE;
  hspi1.Init.NSS = SPI_NSS_SOFT;
  hspi1.Init.BaudRatePrescaler = SPI_BAUDRATEPRESCALER_256;
  hspi1.Init.FirstBit = SPI_FIRSTBIT_MSB;
  hspi1.Init.TIMode = SPI_TIMODE_DISABLE;
  hspi1.Init.CRCCalculation = SPI_CRCCALCULATION_DISABLE;
  hspi1.Init.CRCPolynomial = 10;
  if (HAL_SPI_Init(&hspi1) != HAL_OK)
  {
    Error_Handler();
  }

}
*/
void InitSPI(void){
  SPI_DeInit();
  // 初始化 高字节先发/最大时钟分频32/从机模式/空闲时CLOCK 0 /相位 第2个EDGE/数据方向 2线双向/硬件NSS/CRC计算值 0x07（正常无效）
  SPI_Init(SPI_FIRSTBIT_MSB,SPI_BAUDRATEPRESCALER_32,SPI_MODE_SLAVE,SPI_CLOCKPOLARITY_LOW,SPI_CLOCKPHASE_2EDGE,SPI_DATADIRECTION_2LINES_FULLDUPLEX,SPI_NSS_HARD,0x07);
  // 开启接收完成中断
  SPI_ITConfig(SPI_IT_RXNE,ENABLE);
  // 开启发送为空中断
  SPI_ITConfig(SPI_IT_TXE,ENABLE); 
  SPI_Cmd(ENABLE); 
}

```

中断程序如下
```cpp
/**
  * @brief  SPI Interrupt routine.
  * @param  None
  * @retval None
  */
uint8_t spi_data;
uint8_t spi_send_data[8] = {0x12,0x23,0x34,0x45,0x56,0x67,0x78,0x89};
uint8_t spi_send_i = 0;
INTERRUPT_HANDLER(SPI_IRQHandler, 10)
{
  /* In order to detect unexpected events during development,
     it is recommended to set a breakpoint on the following instruction.
  */
  
  if(SPI_GetFlagStatus(SPI_FLAG_RXNE) == SET){
    // 接收完成
    spi_data = SPI_ReceiveData();
    (void)spi_data;
  }
  if(SPI_GetFlagStatus(SPI_FLAG_TXE) == SET){
    // 发送为空 需要将新的值写入到发送缓冲区
    SPI_SendData(spi_send_data[(spi_send_i++)%8]); 
  }
}

```


## 6 ADC

### 6.1初始化

查询方式初始化如下
```cpp
/**
* @brief ADC初始化
*/
void InitADC(void){

  ADC1_DeInit();
  //初始化 ADC:单次转换/通道 8/时钟分频/关闭事件/数据右对齐/使能施密特触发器
  ADC1_Init(ADC1_CONVERSIONMODE_SINGLE,
            ADC1_CHANNEL_8,
            ADC1_PRESSEL_FCPU_D2,
            ADC1_EXTTRIG_TIM,
            DISABLE,
            ADC1_ALIGN_RIGHT,
            ADC1_SCHMITTTRIG_CHANNEL8,ENABLE);
  
  ADC1_Cmd(ENABLE);
  
}
```
