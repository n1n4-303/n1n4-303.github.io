---
layout: default
title: "Understanding granular synthesis with pure data"
permalink: /tutorials/granular
---

# Understanding granular synthesis with pure data
  
<br />Granulation is a technique in which you manipulate a short-duration microacoustic event (typically between 1 to 100ms) known as grain, that can be used on sound design to achieve multiple results, like creating unpredictability, for instance. An interesting thing about granular synthesis is that it gives you the ability to control pitch without affecting speed and speed without affecting pitch which gives you a great amount of control. It may be useful if you're thinking sound as a process and you can take it to many interesting directions. If you are interested in learning more deeply about granular synthesis and its possibilities, refer to ROADS, 2004.
<br />Granular synthesis is behind many fancy plugins or built-in fx you are used to see in your DAW of choice, such as Ableton's Grain Delay. A good way to understand how they're used might be to just try to build a simple granular synthesizer yourself.


## Let's do it!

<br />**The recorder**
<br />So we need a way to record an input. We do that by using an analog to digital converter [adc~]. For the sake of organization, we're going to put it into a subpatch, so our patch will look more clear further on.
<br />
![subpatch-recorder](https://user-images.githubusercontent.com/64982634/83361737-46ace280-a383-11ea-8692-bd982ff0bf39.JPG)
*Fig.1 Creating a subpatch*
<br />
The signal coming from your microphone is an analog signal which represents in voltage the changes that happen in air pressure. What the adc does is to translate those into digital domain by capturing periodic snapshots of that voltage and representing those snapshots as discrete numbers.
<br />Later in the patch you'll see that we need a [dac~], a digital-to-analog-converter in order to listen to these numbers back through our speakers.
<br />
![recorder](https://user-images.githubusercontent.com/64982634/83361865-790b0f80-a384-11ea-864a-ae847d533a62.JPG)
*Fig.2 Recorder subpatch*
<br />
The bang is your record button. Note that pd records at whatever sample rate ADC and DAC are running at, this is defined in your audio settings, so be aware of that.
<br />[tabwrite~] will allow us to visualize our waveform and store it. For that to happen, you need to create an array with a matching name.
<br />Here our array is going to be one second long we're going to call it “sampling”.
<br />
![array-properties](https://user-images.githubusercontent.com/64982634/83362038-17e43b80-a386-11ea-8364-cf0d2047492f.JPG)
*Fig.3 Defining array properties*
<br />
<img src="https://user-images.githubusercontent.com/64982634/83753569-6fbec300-a662-11ea-8f58-395a662b93fe.JPG" width="591">
*Fig.4 Waveform recorded into array*
<br />
I added 3 points to the size so that I could use a 44.1 value in my patch. You might want to look up how our [tabwrite4~] object operates to understand interpolation. For a more in depth explanation you can also check chapter 2 of Miller Puckette's book “The theory and technique of electronic music”. We're going to use interpolation here to increase the accuracy of table lookup and read continuosly.
<br />I'm also going to create a way for us to write and read our sample file. Here's how:
<br />
![soundfiler](https://user-images.githubusercontent.com/64982634/83362167-1109f880-a387-11ea-8809-508a4ff3cc96.JPG)
*Fig.5 Soundfiler: read and write soundfiles to arrays*
<br />
→ Why can't I read my file?
<br />A reason you might not be able to read a file from soundfiler is that you must save the patch first so that pd knows what directory to read from. Pd will save your sample to the same directory as the patch.
<br />Lets put a [tabread4~] as I mentioned before to read from our "sampling" array. And we should also add a [dac~] in order to listen to the sample and give it a on and off button.
<br />
![dac-tab](https://user-images.githubusercontent.com/64982634/83399431-1dc73480-a3f9-11ea-8d2d-a6571ccb4115.JPG)
*Fig.6 Table lookup and DAC*
<br />
<br />**The sampler**
<br />Now we're going to have a [phasor~] reading the sample and then a multiplier [\*~] and [+~] initially set to read the entire sample. You'll see where this is going now.
<br />
![phasor-1](https://user-images.githubusercontent.com/64982634/83399821-c4abd080-a3f9-11ea-9ef2-2ab1312f6763.jpg)
*Fig.7 phasor~ - sawtooth signal for table lookup*
<br />
The [\*~] object will allow us to manipulate the amount of the sample we want to playback and the [+~] will set the starting point.
<br />
<img src="https://user-images.githubusercontent.com/64982634/83400407-abefea80-a3fa-11ea-9981-cd69d70748dc.JPG" width="591">
*Fig.8 Patch overview*
<br />
We're going to put the sample size control and starting point control into subpatches to keep things clean.
<br />
![patch-1](https://user-images.githubusercontent.com/64982634/83406180-0478b500-a406-11ea-8ab2-78aecf5ffbd6.JPG)
*Fig.9 Creating sample size control subpatch*
<br />
Now, if you change the 1000 ms to a lower value, you will read just a portion of the array, but it will take an entire second to do it, as defined by phasor speed.
<br />Try changing to 500ms and you'll see that to read at the original speed you will have to increase the phasor speed to 2 Hz.
<br />
![samplesize-subpatch](https://user-images.githubusercontent.com/64982634/83406368-66d1b580-a406-11ea-8518-f5c572b9914c.JPG)
*Fig.10 Sample size control subpatch*
<br />
![starting-point-sub](https://user-images.githubusercontent.com/64982634/83767350-73a81080-a675-11ea-97bc-9fb1a2707885.JPG)
*Fig.11 Starting point control subpatch*
<br />
You might have noticed at this point that something is causing your audio to produce little clicks while you manipulate the values on your number boxes. This is caused by discontinuity on the [tableread4~] object. [line~] will fix it by ramping up the value instead of jumping so we pack the sample size information together with a ramping time for [line~].
<br />Now that we've got everything working, try exploring the possibilities of this patch, you can always add more to it: add filters, delay, reverb, envelope generators, it's up to you really.
<br />This is just an introductory tutorial, but it opens a lot of possibilties to explore this technique in more complex ways. I hope it can give you a better grasp on how granular synthesis works in your computer.
<br />

================================================================================
References:
Roads, Curtis. Microsound. MIT press, 2004.
Puckette, Miller. The theory and technique of electronic music. World Scientific Publishing Company, 2007.
Johannes Kreidler's website <http://www.pd-tutorial.com/english/ch03s07.html>
