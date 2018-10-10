# STM32F407-Familiarization

## FreeRTOS Demo

Being familiar with an RTOS is something I've seen requested on many job applications. Now that I have a development board capable of running one, I figured it was about time I got started learning FreeRTOS.

This example contains two tasks: one blinks an LED every second, the other finds every 32-bit prime number and illuminates the LED when found. When power is applied, the two tasks are run synchronously... The LED blinks while the poor microprocessor slaves away doing pointless math. This is a very good demonstration of how FreeRTOS allows for the abstraction of tasks, and takes care of running them together.

https://i.imgur.com/Bft7EIz.gifv