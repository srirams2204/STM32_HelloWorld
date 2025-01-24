# STM32_HelloWorld

## Table of Contents
- [Overview](#overview)
- [Blinking LED](#blinking-led) <!-- - [Blink and Fade LED](#blink-and-fade-led) -->
- [Printf with ITM Data Console](#printf-with-itm-data-console)<!-- - [PWM Generation and Duty Cycle](#pwm-generation-and-duty-cycle) --><!-- - [ADC (Analog to Digital Converter)](#adc-analog-to-digital-converter) -->
- [1Hz Signal Generator Timer](#1hz-signal-generator-timer)
- [Contributors](#contributors)
- [References](#references)

## Overview
This repository provides basic programs for STM32 microcontrollers, including LED blinking, serial print (UART), and ADC reading. While these examples are compatible with most STM32 boards, the STM32F407G-DISC1 is used for programming and testing. The code is developed using STM32CubeIDE with HAL libraries, offering a foundation for embedded systems development.

Link to STM32F407G-DISC1 ---> https://www.st.com/en/evaluation-tools/stm32f4discovery.html

<div align="center">
  <img src="https://github.com/user-attachments/assets/ed98e83f-f1c6-48b0-84dd-4d02ee2a9480" width="800"></div>

## Blinking LED 
### Hardware Requirements
1. LED (Any color)
2. 220Ω current-limiting resistor
3. Jumper wires

### Pin Configuration

|     STM32F407G-DISC    |           LED           | 
|------------------------|-------------------------|
| LED positive (anode)   | PC1 via 220Ω resistor   | 
| LED negative (cathode) | GND                     | 

### Code Overview
```c
HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_1);  // Toggle LED state
HAL_Delay(1000);                        // Wait for 1 second

```
### OR
```c
HAL_GPIO_WritePin(GPIOC, GPIO_PIN_1, GPIO_PIN_RESET);  // Set LED to LOW
HAL_Delay(1000);                                       // Wait for 1 second
HAL_GPIO_WritePin(GPIOC, GPIO_PIN_1, GPIO_PIN_SET);    // Set LED to HIGH
HAL_Delay(1000);                                       // Wait for 1 second
```
### Demo:
<div align="center">
  <img src="https://github.com/LeninValentine06/STM32_HelloWorld/blob/2cd2cf001b1ecbaec113c7af238500b1bcc9b18b/assets/BLINK-LED.gif" width="800"></div>

## Printf with ITM Data Console
### Hardware Requirements
1. STM32 Board
2. Programming Cable
   
### Code Overview
***Include***
```c
#include "stdio.h"
```
***ITM Printf Function***
```c
int _write(int file, char *ptr, int len){
	int i = 0;
	for (i = 0; i < len; i++){
		ITM_SendChar(*ptr++);
	}
	return len;
}
```
***Main***
```c
while(1){
   printf("Hello World!\n");
   HAL_Delay(1000);
}
```

### Demo
<div align="center">
  <img src="https://github.com/user-attachments/assets/60fd0dd1-5a37-4eeb-9ae8-d8a2d4186d81" width="800"></div>
  
## 1Hz Signal Generator Timer
### Hardware Requirements
- LED (Any color)
- 220Ω current-limiting resistor
- Jumper wires

### Timer Configuration
<div align="center">
  <img src="https://github.com/user-attachments/assets/96f93230-a93d-4f0e-a2da-adcdfe64811d" width="800"></div>

### TIMER Frequency Formula & Prescalar Calculation
From the Timer Configuration image HCLK is '100MHz'  
**Prescaler** - Divides the timer HCLK by a factor ranging between 1 upto 65,535 (i.e unsigned 16-bit integer values)
**Period** - Maximum value for the timer counter before it restarts to count again (i.e unsigned 16-bit integer values)

<div align="center">
  <img src="https://github.com/user-attachments/assets/c33ea9d1-a5cc-4438-851c-a8df723f75e9" width="800"></div>

```
HCLK = 100000000 Hz or 100MHz
HCLK / 10,000 = 10,000
         |
     PRESCALAR
10,000 / 10,000 = 1Hz
           |
        PERIOD
Prescaler (PSC - 16 bits value) = 10,000 - 1 = 9999 
Counter Period (AutoReload Register - 32 bits value ) = 10,000 - 1 = 9999 
```
### Code Overview
If the period exceed the total amount it will reset, interrupt and start again
```
/* USER CODE BEGIN 0 */
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim) {
	HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_15);
}
/* USER CODE END 0 */
```
Activate the Selected Timer
```
/* USER CODE BEGIN 2 */
HAL_TIM_Base_Start_IT(&htim2);
/* USER CODE END 2 */
```

### Demo
<div align="center">
  <img src="https://github.com/srirams2204/STM32_HelloWorld/blob/ce64435ad578df577c9ede1e74380eb12ef0e5e3/assets/TIMER_1Hz.gif" width="800"></div>

## Contributors
- [@Sriram S](https://github.com/srirams2204)
- [@Lenin Valentine](https://github.com/LeninValentine06)

## Reference
***Mastering STM32*** - A step-by-step guide to the most complete ARM Cortex-M platform, using the official STM32Cube development environment **(By Carmine Noviello)**
