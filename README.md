# Basic Satellite
## An Amazon Basics speaker converted to a Rhasspy satellite
----
A voice announcements speaker that works with the Rhasspy voice control system. Basically, a cheap, small speaker with decent audio quality for voice output, controlled by an ESP32-based board with [ESP32 Rhasspy Satellite](https://github.com/Romkabouter/ESP32-Rhasspy-Satellite) firmware. 

Amazon sells these cheap little speaker pairs called "Amazon Basics PC speakers", which I used for the project. I find their audio quality good enough for the intended voice announcement use case. It consists of one "active" speaker powered by USB, which has a little power amplifier PCB inside, and a second one that is a "passive" speaker driven by the first one. I used the "active" part for this one, and kept the "passive" one for another project.

I bought this from [amazon.de](https://www.amazon.de/dp/B07DDK3W5D) in Germany, it looks like the same speaker is also available from [amazon.com](https://www.amazon.com/dp/B07DDK3W5D) in the US. 

The first step is to open the speaker, remove all the hot glue they used to fix the little PCB, and then remove the PCB. In its place, I put a prototype board from [Aliexpress](https://www.aliexpress.com/item/10050034994159) that has a footprint for an ESP8266 or ESP32 module. The protoboard needs to be cut to have the same irregular shape as their little amplifier PCB. I made a cardboard template cut to size and used that to test the fit inside the speaker enclosure.

<img src="pictures/2/Basic Satellite 1.jpg" width="49%" /> 
<img src="pictures/2/Basic Satellite 2.jpg" width="49%" /> 

Next, build the ESP32 module. You need
- ESP32 WROOM module, e.g. from [Aliexpress](https://www.aliexpress.com/item/32840441199.html)
- MAX58397A based module, D/A converter with 3W class D amplifier 
- 3.3V voltage regulator module
- a few resistors etc.

The [schematics](hardware/Basic-Satellite.pdf) and complete [bill of materials](hardware/BOM%20Rhasspy-Satellite.xlsx) are available in the ```hardware``` folder.

Begin by placing all components on the cut-to-size prototype board without soldering and slide it into the speaker enclosure to make sure everything fits nicely.

![](pictures/2/Basic%20Satellite%206.jpg)

Finally, connect the leads from the speaker itself, from the LED module in the foot of the speaker, and from the USB cable that came with the speaker to the electronics module.

Theoretically, one could also connect a digital microphone to the ESP32 module, the firmware supports the INMP441 and similar models. I tried one from Aliexpress, but didn't manage to position it in such a way that the sound quality was good enough for voice recognition purposes -- I'm not an audio engineer. 

Also, if you do want to use a microphone, the ESP32 module will continuously stream the audio signal to the Rhasspy server, and the voice recognition happens there. I didn't like the idea of a continuous audio stream going through my Wifi network.
