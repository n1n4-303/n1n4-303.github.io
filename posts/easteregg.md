---
layout: default
title: "Easter egg - Making a Pd sound design tool"
permalink: /tutorials/easter-egg
---

# Easter egg - Making a Pd sound design tool

I was reading an article about the sound of Ghost of Tsushima and the amazing world created by the Sucker Punch sound team and something Josh Lord (Senior Sound Designer) said caught my attention.
<br />While talking about the UI/UX sounds he said a particular tool was very useful: he created a Max/MSP patch for processing the source, something like a "happy accidents" generator that had the ability of printing out something that happened while he was tweaking the sound. I thought it sounded like a really interesting and useful sound design tool so I decided to try making my own Pd tool that would do something similar. I'm going to show you how it looks like and then we'll see a little about what is going on inside.
<br />
<img src="https://user-images.githubusercontent.com/64982634/90643158-26c2e780-e22b-11ea-93b8-dc937d583d9f.png" width="591">
*Fig.1 - Easter egg*
<br />
1 - a way to open my source file
2 - a way to print out "x" seconds from buffer into a file
3 - some fx to manipulate the source
<br />
## OPENING SOURCE FILE

As I mentioned, first I had to create a way to open my source file and store it into an array to work with it, I used [openpanel] and [soundfiler] for that. The left outlet of [soundfiler] will output the number of samples - you need to divide this number by your sample rate to get the original playback speed and feed it to [phasor].
![openpanel-easteregg](https://user-images.githubusercontent.com/64982634/90640439-e1e98180-e227-11ea-87e5-5cde2cefa543.png)
*Fig.2 - Opening your sample*
<br />
I used the phasor rate information and sent it to an HSlider to manipulate playback speed and added a bang to reset to original speed and another one to set it to 0. There is a tutorial by Dr.Rafael Hernandez (cheetomoskeeto) that teaches you something similar, definitely check it out if you are interested or not following this very well - I will add it to the references section.
<br />
![tabread-easter](https://user-images.githubusercontent.com/64982634/90640550-03e30400-e228-11ea-9cfe-0bca66a93c96.png)
*Fig.3 - Reading the table*
<br />
Now that you have set the phasor speed, multiply it by the sample size and read the table. I have an [outlet~] because this is a subpatch. I am graphing the controls to the main patch so everything looks organized and usable.
![gui-openpanel](https://user-images.githubusercontent.com/64982634/90640618-1b21f180-e228-11ea-884b-6e30ede7373e.png)
*Fig.4 - Controls for audio source subpatch*
<br />
The array “original” is in the main patch so I can visualize the waveform.
<br />
![waveform-table](https://user-images.githubusercontent.com/64982634/90640701-38ef5680-e228-11ea-9d0d-e47658ec896f.png)
*Fig.5 - Source waveform*
<br />
After this, I wanted to make an fx chain, so I could have different ways of modifying my audio. I added ring modulation, 2 delays, chorus, reverb, low pass filter and a noise generator. I might add other things to the chain, but for now this allows me to play around quite a bit. The order of effects can be changed in any way you want.

## FX CHAIN

The effects are not the main focus here so I won't be into a lot of the details, however, I will show you how I implemented them. All the effects are subpatches, so you will see an [inlet~] and [outlet~] on them so the audio passes through.
<br />
Here's how the two different delays work:
![delay-subpatch](https://user-images.githubusercontent.com/64982634/90640818-620fe700-e228-11ea-9ee0-b3ac8a9deefd.png)
*Fig.6 - Delay subpatch*
<br />
![slapback-delay](https://user-images.githubusercontent.com/64982634/90640893-76ec7a80-e228-11ea-88ae-d548d7e5c2da.png)
*Fig.7 - Slapback delay*
<br />
For reverb I used [freeverb~], a Schroeder/Moorer reverb external that uses 8 comb filters. We have dry/wet and room size controls, those are freeverb~ messages. For more details, chech the help patch on [freeverb~].
<br />
![reverb-subpatch](https://user-images.githubusercontent.com/64982634/90640985-95527600-e228-11ea-8e5e-6a4eeb78461e.png)
*Fig.8 - Using freeverb~*
<br />
The chorus is produced by reading 3 copies of the delay line at a slightly different pitch and phase than the other. In other words, we have an input and the signal is distributed in 2 ways: one goes directly to the output and a copy goes to the delay line, then I can create 3 different LFO's that will read from a single delay line.
![chorus-sub](https://user-images.githubusercontent.com/64982634/90641065-b0bd8100-e228-11ea-995f-a504b39d7d05.png)
*Fig.9 - Chorus subpatch
<br />
Then I added a simple low-pass filter using [lop~].
![lpf-subpatch](https://user-images.githubusercontent.com/64982634/90641130-c468e780-e228-11ea-9575-309f463530db.png)
*Fig. 10 - Low-pass filter subpatch*
<br />
And ring modulation multiplying the [inlet~] by a modulator [osc~].
![easter-ring](https://user-images.githubusercontent.com/64982634/90641207-dba7d500-e228-11ea-9abe-edec441c3e36.png)
*Fig.11 - Ring modulation*
<br />

## OUTPUT

On my master output I send the signal to a VU meter so I can monitor my levels
<br />
![sendtovu](https://user-images.githubusercontent.com/64982634/90641288-f67a4980-e228-11ea-953c-0ba48d7a9abc.png)
*Fig.12 - Sending levels to VU meter*
<br />
![metering](https://user-images.githubusercontent.com/64982634/90641382-14e04500-e229-11ea-9d42-916ad81d03d7.png)
*Fig.13 - Metering the output levels*
<br />
Finally, this is one of the most important parts of this patch, because it defines how I got the last seconds of audio that I wanted to catch. So I have an [inlet~] that receives signal from the end of the chain and then I have to delay the input by defining a delay line that will be read later before [writesf~]. I used a counter before [makefilename] so I could have an incremental file name: my audio files will look like this “easter-egg0.wav”, “easter-egg1.wav” and so on... Then, I need pd to work a few steps so I used the [trigger] object or as you can see in the patch, [t b b b a] and this helps with the operation order, remember that trigger outputs from right to left so it will: create the file, then read delay line, start recording, wait “x”  seconds and then stop.
<br />
![buttons-catch-done](https://user-images.githubusercontent.com/64982634/90641517-3c371200-e229-11ea-9a81-151bee81c64b.png)
*Fig.14 - Receiving signal*
<br />
![catch-audio-sub](https://user-images.githubusercontent.com/64982634/90641673-67216600-e229-11ea-93a8-8916946c5d1f.png)
*Fig.15 - Subpatch to print out last 15 seconds of audio*
<br />
![catch-contrls](https://user-images.githubusercontent.com/64982634/90641804-8cae6f80-e229-11ea-8617-50e67a412a3a.png)
*Fig.16 - Controls for the subpatch*
<br />
I had a lot of fun doing this and I believe it's very easy to adapt to whatever needs I have in the future. There is still room for a lot of improvements. If you wish to try and use the patch, please feel free to download it from my [github repository](https://github.com/n1n4-303/pd-patches/tree/master/easter-egg). 
<br />
================================================================================ 
References

Crafting Ghost of Tsushima's Tremendous Sound 
<https://www.asoundeffect.com/ghost-of-tsushima-sound/>

Freeverb~ 
<https://puredata.info/downloads/freeverb>

Cheetomoskeeto tutorial 
<https://www.youtube.com/watch?v=boX0v54SqtU&list=PL12DC9A161D8DC5DC&index=24>

Easter egg github 
<https://github.com/n1n4-303/pd-patches/tree/master/easter-egg>

