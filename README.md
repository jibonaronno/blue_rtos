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
These codes were generated and does not support by C++ as the assignment of members are gapped. So I removed the const property and assignes the members in the main function.
