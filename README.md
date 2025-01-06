# STM32_HelloWorld

## 1. Blinking LED with STM32F407VGT6
### Hardware Requirements
1. LED (Any color)
2. 220Ω current-limiting resistor
3. Jumper wires

### Pin Configuration

- LED positive (anode) → PC1 via 220Ω resistor
- LED negative (cathode) → GND

### Code Overview
```c
HAL_GPIO_TogglePin(GPIOC, GPIO_PIN_1);  // Toggle LED state
HAL_Delay(1000);                        // Wait for 1 second

```
### Demo:
<div align="center">
  <img src="https://github.com/LeninValentine06/STM32_HelloWorld/blob/2cd2cf001b1ecbaec113c7af238500b1bcc9b18b/assets/BLINK-LED.gif" width="800"></div>

