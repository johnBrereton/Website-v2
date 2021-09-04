# Home Automation and Control
---

Today more than half (69%) of homes in the United States have at least one smart device such as a smart speaker or thermostat.  Smart homes have the potential to be revolutionary technolgy that changes the lives of households arround the world.  Unfortunatly ever since smart homes became a reality they have stuggled with two major problems, reliability and compatability.

Many smart home products that are bought to maket are severly underdeveloped especially in regards to firmware.  They struggle with connectivity issues and bugs in general.  Furthermore several of the companies making smart home products are less established brands with the possibility of going out of buisness, ending firmware updates for users.

The other major issue with smart homes is compatability.  Some smart devices are not able to communicate with other smart devices resulting in a very unintutiv experience.  Users may need to download several apps or may only to be able to control some of their devices with their smart speaker.

After experiencing both of these issues, I began to look for a solution.  I wanted to be able to control all of my smart home devices in one app and keep the device communications within my local network so if a manufacturer were to go out of buisness my smart home devices would continue to work.  After looking into the plethora of smart home control apps ([Google home](https://assistant.google.com/smart-home/), [Samsung smartthings](https://www.smartthings.com), etc.), I decided on [Apple Homekit](https://www.apple.com/ios/home/accessories/).  Apple homekit has a very streamlined interface, supports local network device communication, third party device connection hubs, and supports all major device types.

To solve the issue of compatabilty I setup a server running homebridge on a raspberry pi.  Homebridge is a linux based smart home integration platform that acts as a third party device connetion hub in homekit.  With homebridge I can write plugins or use plugins that other people have already made to integrate almost any smart device into apple homekit.

