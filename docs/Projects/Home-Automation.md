# Home Automation and Control
---

<div width="100%"><img src="\img\Homekit-Demo.png"><img src="\img\Homebridge-Logo.png"> </div>

Today more than half (69%) of homes in the United States have at least one smart device such as a smart speaker or thermostat.  Smart homes have the potential to be revolutionary technology that changes households around the world.  Unfortunately, ever since smart homes became a reality they have struggled with two major problems, reliability, and compatibility.

Many smart home products that are brought to market are severely underdeveloped especially in regards to firmware.  They struggle with connectivity issues and bugs in general.  Furthermore several of the companies making smart home products are less established brands with the possibility of going out of business, ending firmware updates for users.

The other major issue with smart homes is compatibility.  Some smart devices are not able to communicate with other smart devices resulting in a very unintuitive experience.  Users may need to download several apps or may only be able to control some of their devices with their smart speaker.

After experiencing both of these issues, I began to look for a solution.  I wanted to be able to control all of my smart home devices in one app and keep the device communications within my local network so if a manufacturer were to go out of business my smart home devices would continue to work.  After looking into the plethora of smart home control apps ([Google home](https://assistant.google.com/smart-home/), [Samsung smartthings](https://www.smartthings.com), etc.), I decided on [Apple HomeKit](https://www.Apple.com/ios/home/accessories/).  Apple HomeKit has a very streamlined interface, supports local network device communication, third-party device connection hubs, and supports all major device types.

To solve the issue of compatibility I set up a server running Homebridge on a raspberry pi.  Homebridge is a Linux-based smart home integration platform that acts as a third-party device connection hub in HomeKit.  With Homebridge, I can write plugins or use plugins that other people have already made to integrate almost any smart device into Apple HomeKit.

After setting up Homebridge and integrating my smart home devices, I can control every smart home device in my house with one app, and don't have to worry about device support by manufacturers.