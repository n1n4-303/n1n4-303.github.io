---
layout: default
title: "Create your own VCV Rack module with Pd"
permalink: /tutorials/vcv-pd
---

# Create your own VCV Rack module with Pd

<br />VCV Prototype is a scripting language host for VCV Rack from which you can create your own VCV Rack module. Now, after being funded support to Pd and Vult DSP language were just added. And that's great news so, I'm going to show you what this is about and how you can create your own module using Pd.
<br />Since I just talked about [ring modulation](https://n1n4-303.github.io/tutorials/ring-modulation), I'm going to adapt the patch we used on the last tutorial for our example here. 
<br />The carrier is going to be a VCO module from Bogaudio, so we need to tell Pd that we're receiving audio from Prototype and you do that by adding an [adc~]. I'm amplifying the signal by multiplying it by 1. For the modulating signal, we need to receive control data from VCV to change the osc frequency, so we use [r fromRack] and [route K1] to map the control - prototype has 6 knobs (K1, K2, K3.. and so on) - in this case I'm just using one. If you're starting to get lost here and you need the reference to keep up, you can find it in the github repository: there is a file named template.pd in examples. My attempt here is to make a simple guide for your first steps into this.
<br />
![pd-prototype](https://user-images.githubusercontent.com/64982634/88485820-e7c5ad00-cf70-11ea-9b3a-fa570da283c3.jpg)
*Fig.1 - Pd patch and VCV prototype*
<br />
Now that we're done with our patch, let's fire up VCV and add Prototype.
<br />
![drop-down-vcv](https://user-images.githubusercontent.com/64982634/88485851-35dab080-cf71-11ea-8bb4-1ac10053a510.png)
*Fig.2 - Setting up VCV Prototype*
<br />
After adding prototype, you need to “Set Pure Data application” , locate your installed Pure Data application and then ”Load script". Your patch name and Pd version will show up on the display.
<br />
![version-patch](https://user-images.githubusercontent.com/64982634/88485862-51de5200-cf71-11ea-8a10-8fcc276df91e.png)
*Fig.3 - Prototype displays information*
<br />
Then you can add an input and test. The flashing yellow lights indicate that we have signal.
<br />
![module-flashing](https://user-images.githubusercontent.com/64982634/88485874-776b5b80-cf71-11ea-8dea-6b63b92a867c.png)
*Fig.4 - Checking for signal*
<br />
<img src="https://i.makeagif.com/media/4-20-2018/hmsFMZ.gif">
<br />
Another interesting thing is that we have a nice RGB for the L indicators, so we can also add lights. I'm just using one of them, but I added another 3 to show you how you can use different colors. The first variable is for red, second for green and the last is blue. In the L4 message you can see that by adding green and blue I got a nice cyan (is it cyan?) color. This also works for the switches as well but instead of L1, L2, you have to use S1, S2.
<br />
![add-rgb](https://user-images.githubusercontent.com/64982634/88485889-9d90fb80-cf71-11ea-8b2b-6de4c448f325.png)
*Fig.5 - Adding colors*
<br />
![colors-module](https://user-images.githubusercontent.com/64982634/88485897-b4cfe900-cf71-11ea-9dcc-ad1c81c61f97.png)
*Fig.6 - RGB indicators on Prototype.*
<br />
This is all exciting news and I'm still learning and exploring too so I hope this is helpful to anyone out there doing the same thing!
<br />

================================================================================ 
References:

VCV Prototype
https://library.vcvrack.com/VCV-Prototype/Prototype

<br />VCV Prototype source
https://github.com/VCVRack/VCV-Prototype

<br />VCV Community Announcement
https://community.vcvrack.com/t/pure-data-added-to-vcv-prototype/10583

<br />Bogaudio modules
https://library.vcvrack.com/?brand=Bogaudio
