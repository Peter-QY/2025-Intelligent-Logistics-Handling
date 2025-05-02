# 2025 西工大工创基地物流搬运下位机代码

*本工程基于STM32F10ZET6搭建*

## 所使用的配件

摁键模块（一键启动）

扫码模块 GM65

串口屏

四个脉轮

六个42张大头步进电机

两个20kg舵机

正点原子STM32F103ZET6最小系统板

5v 8v稳压扩展版

一个摄像头模组（树莓派使用）

树莓派

接线若干

滑轨、底盘碳板、打印件若干

## 串口区

- 树莓派4B串口通信
  USART1_TX  PA9
  USART1_RX  PA10
- 串口屏
  USART2_TX  PD5      重定义而来，PA2已用于舵机输出PWM *==GPIO_PinRemapConfig(GPIO_Remap_USART2,ENABLE)==*
  USART2_RX  PD6      重定义而来，PA3已用于舵机输出PWM
- 未使用到的串口，但可以用于别的用途
  USART3_TX  PD8      重定义而来，PB10已用于爪子升降输出PWM *==GPIO_PinRemapConfig(GPIO_Remap_USART3,ENABLE)==*
  USART2_RX  PD9      重定义而来，PB11已用于MOTOR2输出PWM
- 陀螺仪 HWT101
  UART4_TX  PC10
  UART4_RX  PC11
- 扫码模块 XM1605
  UART5_TX   PC12
  UART5_RX   PD2

## 按键区

- 一键启动按钮
  PD8

## I2C

- OLED 0.96寸(暂未使用)
  SCL    PD4
  SDA    PD1

### 舵机区

- Servo1   ==暂时没有用到==
  TIM5_CH2 PA1        输出PWM波
- Servo2  ==控制爪子张开闭合==
  TIM5_CH3 PA2        输出PWM波
- Servo3  ==控制爪子云台旋转==
  TIM5_CH4 PA3        输出PWM波

##  步进电机区

- MOTOR1   ==爪子升降==
  PA4    DIR
  PC5    ENM
  PB10   STEP      PA2重映射而来，TIM2_CH3   *==GPIO_PinRemapConfig(GPIO_FullRemap_TIM2,ENABLE)==*
- MOTOR2   ==暂时没有用到==
  PA5    DIR
  PC5    ENM
  PB11   STEP      PA3重映射而来，TIM2_CH4   *==GPIO_PinRemapConfig(GPIO_FullRemap_TIM2,ENABLE)==*
- MOTOR3   ==左前轮==
  PG7   DIR
  PC5   ENM
  PC6   STEP        PA6重映射而来，TIM3_CH1   *==GPIO_PinRemapConfig(GPIO_FullRemap_TIM3,ENABLE)==*
- MOTOR4 
  PG8    DIR   ==右前轮==
  PC5    ENM
  PC7    STEP       PA7重映射而来，TIM3_CH2   *==GPIO_PinRemapConfig(GPIO_FullRemap_TIM3,ENABLE)==*
- MOTOR5  ==物块旋转台==
  PG13   DIR
  PD7    ENM
  PB8   STEP        TIM4_CH3
- MOTOR6   ==暂时没有用到==
  PE6   DIR
  PD7   ENM
  PB9   STEP        TIM4_CH4
- MOTOR7    ==右后轮==
  PA8  DIR
  PD7  ENM
  PC8  STEP        PB0重映射而来，TIM3_CH3   *==GPIO_PinRemapConfig(GPIO_FullRemap_TIM3,ENABLE)==*
- MOTOR8    ==左后轮==
  PC1  DIR
  PD7  ENM
  PC9  STEP        PB1重映射而来，TIM3_CH4   *==GPIO_PinRemapConfig(GPIO_FullRemap_TIM3,ENABLE)==*

> 四个车轮电机挂载在同一个定时器TIM3的四个输出通道上
> 爪子升降挂载在一个定时器TIM2的一个输出通道CH3上
> 物块旋转台挂载在一个定时器TIM4的一个输出通道CH3上
> 空闲两个电机 MOTOR2和MOTOR6分别是TIM2_CH4和TIM4_CH4
> TIM2和TIM3进行了完全重映射
> 三个舵机用了TIM5的三个通道


TIM1_CH4  可以用来输出PWM驱动ws2812
