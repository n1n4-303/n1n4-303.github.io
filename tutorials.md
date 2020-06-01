---
layout: default
title: "tutorials"
permalink: /tutorials/
---

[PURE DATA] [Understanding granular synthesis with pure data](granular.md)

# Understanding granular synthesis with pure data
  
<br />Granulation is a technique in which you manipulate a short-duration microacoustic event (typically between 1 to 100ms) known as grain, that can be used on sound design to achieve multiple results, like creating unpredictability, for instance. It may be useful if you're thinking sound as a process and you can take it to many interesting directions. If you are interested in learning more deeply about granular synthesis and its possibilities, refer to ROADS, 2004.
<br />Granular synthesis is behind many fancy plugins or built-in fx you are used to see in your DAW of choice, such as Ableton's Grain Delay. A good way to understand how they're used might be to just try to build a simple granular synthesizer yourself.


## Let's do it!

<br />**The recorder**
<br />So we need a way to record an input. We do that by using an analog to digital converter [adc~]. For the sake of organization, we're going to put it into a subpatch, so our patch will look more clear further on.
<br />
![subpatch-recorder](https://user-images.githubusercontent.com/64982634/83361737-46ace280-a383-11ea-8692-bd982ff0bf39.JPG)
<br />
The signal coming from your microphone is an analog signal which represents in voltage the changes that happen in air pressure. What the adc does is to translate these into digital domain by capturing periodic snapshots of that voltage and representing these snapshots as discrete numbers.
<br />Later in the patch you'll see that we need a [dac~], a digital-to-analog-converter, in order to listen to these numbers back through our speakers.
<br />
![recorder](https://user-images.githubusercontent.com/64982634/83361865-790b0f80-a384-11ea-864a-ae847d533a62.JPG)
<br />
The bang is your record button. Note that pd records at whatever sample rate ADC and DAC are running at, this is defined in your audio settings, so be aware of that.
<br />[tabwrite~] will allow to us to visualize our waveform and store it. For that to happen, you need to create an array with a matching name.
<br />Here our array is going to be one second long.
<br />
![array-properties](https://user-images.githubusercontent.com/64982634/83362038-17e43b80-a386-11ea-8364-cf0d2047492f.JPG)
<br />
I added 3 points to the size so that I could use a 44.1 value in my patch. You might want to look up how our [tabwrite4~] object operates to understand interpolation. We're going to use it here to read our array continuously.
<br />I'm also going to create a way for us to write and read our sample file. Here's how:
<br />
![soundfiler](https://user-images.githubusercontent.com/64982634/83362167-1109f880-a387-11ea-8809-508a4ff3cc96.JPG)
<br />
