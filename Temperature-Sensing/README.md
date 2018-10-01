# STM32F407-Familiarization

## Temperature Sensing

The STM32F407 is a much more complicated processor than what I am used to. 32-bit and crammed full of accessories, it is quite a step up from the PIC10F220 of yester-project. Whilst reading through the features in the datasheet, something caught my eye: an in-chip temperature sensor. Having never used a microcontroller with a sensor built-in, I thought interfacing with this would be a nice and easy first exercise.

For output, the STM32F4 Discovery Board has 4 different-colored LEDs (Red Green Blue Orange) plus an ST-Link debugger. I thought it would be nice if the Green LED indicated "normal" or the "baseline" temperature, the Red LED indicated "hot" or a higher-than-baseline temperature, and the Blue LED indicated "cold" or a lower-than-baseline temperature. In addition to the LEDs, I wanted to see the actual ADC value displayed in my console window, so I setup the on-board ST-Link for Single Wire Output (SWO).

The first step was to figure out how to get the ADC reading this supposed internal temperature sensor. According to the datasheet, it existed at "ADC_CHANNEL_16" on ADC1, but ST's Hardware Abstraction Library allows me to simply call it "ADC_CHANNEL_TEMPSENSOR". After reading some documentation on how to do a conversion, I had an output going to my console.

![img](https://i.imgur.com/mZPv2gv.png)

It's a little jumpy, but I've had experience with jumpy sensors before. One averaging algorithm later, and...

![img](https://i.imgur.com/6U67eoK.png)

Ah, much better. Now to do something with it. I wrote a Goldilocks function to implement my idea from above, and ended up with this:

![img](https://i.imgur.com/yt0Gckk.gif)

Since the output to the console is just the raw ADC value, I'd like to make a function that takes that and converts it to either Fahrenheit or Celsius. Additionally, I'm using ADC1 for the sole purpose of converting the temperature sensor channel. In the future, I'll need to take a look at how to use multiple channels on ADC1 so I'm not gimping the chip's functionality.