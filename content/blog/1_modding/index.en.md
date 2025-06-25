---
title: PC Modding
subtitle: "Custom cable sleeves and hardline water cooling"
summary: Over the past 6 years I customized my PC to my likings. This includes creating custom sleeved cables with precise routing, a hardline watercooling loop for the CPU and lots of RGB lighting controlled by an ESP32 microcontroller.
date: 2022-01-10
cardimage: modding_card.jpeg
authors:
  - Dominik: author.png
---
## My hardware
- Nvidia GeForce RTX 3070
- Amd Ryzen 5 7600X
- 32GB DDR5 RAM


## Custom sleeved cables

My PC case, the Phanteks Enthoo Evolv, features tempered glass panels on both sides. This means there is no place to hide cables and without proper cable management, my PC looked like a mess. To fix this, I purchased a modular power supply unit from Corsair and created my own set of cables. Each wire was cut to length individually and routed using custom brackets made from aluminium. This way, no wires are loose and there is no leftover cables that need to be stashed somewhere. Both ends were crimped and connected to ATX/Molex terminals.

To improve the looks even further, each wire was sleeved in either red or carbon grey to go along with the color theme of the hardware.

{{< figGrid subfolder="images" figCaption="Top: Tools needed for cutting wires, crimping and sleeving. And the final result. Bottom: Watercooling and lighting in place." >}}

## Hardline water cooling

As an modding enthusiast, upgrading to a watercooling solution has been a dream of mine for years. In 2020 I was able to afford the necessary components like a CPU waterblock from Phanteks, a radiator and a pump from Singularity Computers. These three components were connected using hardline tubes from Alphacool. These were heated, bent and cut by hand to fit my build. This way the coolant is moved from the pump to the CPU waterblock, where it absorbs the heat from the CPU. The coolant moves through the radiator at the top of my case to disapate the heat to the surrounding air. Then the coolant returns to the pump again. It took a couple hours to get all the compoponents installed and to prepare the tubes to my liking. After leak testing (and fixing a small leak near the pump) the watercooling loop was up and running with blood red coolant! 

## RGB lighting with ESP32 microcontroller

To put the custom cables and the watercooling loop into the perfect light, I installed a bunch of RGB lights. As the case interior and components are mostly black, a few lights were not able to illuminate the PC as most of the light is absorbed. I added three Corsair RGB fans to the radiator at the top. These ensured even lighting to the mainboard and GPU. LEDs at the bottom were added as well. My RAM did not feature any RGB lighting, so I purchased DIY RAM heatsinks to replace the stock ones. With those I added RGB to my RAM as well. To sync all of these I used an ESP32 microcontroller hidden underneath the top panel of my case. This microcontroller is connected to the internal USB of the mainboard and is responsible for the lighting of the fans, RAM and leds at the bottom. The USB connection is used to change colors and animations of the lighting from a desktop application written in C#.