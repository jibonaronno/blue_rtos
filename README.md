# CMSIS RTOS V2 on STM32F103C8T6 with C++ support (Experimental)
## Using STM32CubeIDE
After changing the the filename main.cpp, some generated code did not compiled due to some compatibility issue.<br />
The code was: <br />
```c
const osThreadAttr_t blink01_attributes = {
  name : "blink01",
  stack_size : 128 * 4,
  priority : (osPriority_t) osPriorityNormal
};

const osThreadAttr_t blink02_attributes = {
  name : "blink02",
  priority : (osPriority_t) osPriorityBelowNormal,
  stack_size : 128 * 4
};
```
These codes were generated and does not support by C++ as the assignment of members are gapped. So I removed the const property and assignes the members in the main function.<br />

Note that this code is generated from cubemx. So when regenerated the project then these initial codes will get back again and also before regeneration rename main.cpp to main.c . So take care of these codes after regeneration.

## delay_us(us, htim) features and delay.cpp
RTOS cannot do us delay. I am applying us delay usiing the help of TIM3. delay.cpp has the delay_us() function. Parameter needs a Timer reference. I am using TIM3. Configured by cubemx as Prescaler:72, Period:65535, ARR:Enabled. At the main() it must need to start by HAL_TIM_Base_Start(&htim3); before osKernelStart(); . 

```c
/* USER CODE END TIM3_Init 1 */
  htim3.Instance = TIM3;
  htim3.Init.Prescaler = 72;
  htim3.Init.CounterMode = TIM_COUNTERMODE_UP;
  htim3.Init.Period = 65535;
  htim3.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
  htim3.Init.AutoReloadPreload = TIM_AUTORELOAD_PRELOAD_ENABLE;
```
