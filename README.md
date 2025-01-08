# STM32_HelloWorld

## Table of Contents
- [Overview](#overview)
- [Blinking LED](#blinking-led)
- [Blink and Fade LED](#blink-and-fade-led)
- [Serial Print with ITM Data Console](#serial-print-with-itm-data-console)
- [PWM Generation and Duty Cycle](#pwm-generation-and-duty-cycle)
- [ADC (Analog to Digital Converter)](#adc-analog-to-digital-converter)
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

## Blink and Fade LED
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

## Contributors
- [@Sriram S](https://github.com/srirams2204)
- [@Lenin Valentine](https://github.com/LeninValentine06)

## Reference

