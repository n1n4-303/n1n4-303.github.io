---
layout: default
title: "Ring modulation - exterminate, exterminate!"
permalink: /tutorials/ring-modulation
---

# Ring modulation - exterminate, exterminate!

<br />EXTERMINATE! If you like Doctor Who, you've heard this before. I'm going to talk about the effect behind a Dalek's voice: ring modulation, also known as balanced modulation. Ring modulation is a signal processing function, a type of amplitude modulation (AM) that takes its name from the shape formed by the diodes on its analog circuit implementation. It was originally used for analog telephony.
<br />
<a title="No machine-readable author provided. Gablin assumed (based on copyright claims). / CC BY-SA (http://creativecommons.org/licenses/by-sa/3.0/)" href="https://commons.wikimedia.org/wiki/File:Ring_Modulator.PNG"><img width="512" alt="Ring Modulator" src="https://upload.wikimedia.org/wikipedia/commons/c/cd/Ring_Modulator.PNG"></a>
*Fig.1 - Ring modulator schematic*
<br />
In ring modulation, the carrier signal is multiplied by the modulating signal. If the modulating frequency is within the audio range, it will produce sidebands that correspond to the sum and difference between the frequencies of each oscillator at the output. This effect can be used to modify sounds and produce robotic voices and metalic, inharmonic chaotic tones, as I will demonstrate.
<br />Let me show you what I mean by that: we're going to multiply two [osc~] objects and take a look at the spectrum produced as a result.
<br />
<img src="https://user-images.githubusercontent.com/64982634/87941907-bd1cb580-ca93-11ea-814f-e246b70f35de.jpg" width="591">
*Fig.2 - Sidebands produced by ring modulation*
<br />
Since we're using 2 sine wave oscillators, the spectrum produced has 2 sideband frequencies. And as you can see neither of the original frequencies are present in the output spectrum.
<br />You can use a microphone input to get that robot voice I initially told you about - your voice will be the carrier in this case. Let's add an [adc~] and amplify the signal [\*~ 10] and then multiply it by our modulator.
<br />
![ring-mic-patch](https://user-images.githubusercontent.com/64982634/87942022-e76e7300-ca93-11ea-8d8e-12ddda8e54fd.JPG)
*Fig.3 - Using a microphone as input*
<br />
<iframe width="560" height="315" src="https://www.youtube.com/embed/QRWfme9x4-Y" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />
If the oscillators frequencies are harmonically related, ring modulation will produce harmonic partials. Let's change our patch a little bit by adding another [osc~] and creating that relation to see what happens.
<br />
![harmonics-ring-3](https://user-images.githubusercontent.com/64982634/87942131-0b31b900-ca94-11ea-8200-7b163880df55.JPG)
*Fig.4 - Adding harmonic partials*
<br />
I set Carrier A to MIDI note 30, which is equivalent to 46,25Hz (F#0) and Carrier B is twice the frequency, hence 1 octave up, 92,5 Hz (F#1). The modulator (M) is set to 4x 46,25Hz or 185Hz.
<br />Now, I'll take a break to explain something important if you're not that familiar with Pd yet: in Pd, the cold inlet (the second one) doesn't take effect until you change the value in the first inlet, so if I change the modulator frequency it won't take effect until I change the carrier frequency. The way you fix that is by using [t b f] so that any time you change the modifier it will also send a bang to the first inlet, forcing the multiplication to happen.
<br />That being said, let's take a look at the spectrum:
<br />
<img src="https://user-images.githubusercontent.com/64982634/87942414-72e80400-ca94-11ea-9124-6376c82087bf.JPG" width="591">
*Fig.5 - Spectrum analysis of the product*
<br />
What we have here are 4 partials:
1st: B-M = 92,5Hz (F#1)
2nd: A-M = 138,75Hz (C#2)
3rd: A+M =231,25Hz (A#2)
4th: B+M = 277,5Hz (C#3)
<br />
Video demonstration
<iframe width="560" height="315" src="https://www.youtube.com/embed/iqZgfjoLVmo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />
I encourage you to try ring modulation and see what kind of sounds you can produce just by using this effect, try using different waveshapes and see how you can produce complex spectra, like in the example below.
<br />
<img src="https://user-images.githubusercontent.com/64982634/87942700-e7bb3e00-ca94-11ea-8284-0fbc554ecf25.JPG" width="591">
*Fig.6 - Using a sawtooth as carrier*
<br />
<img src="https://user-images.githubusercontent.com/64982634/87942786-01f51c00-ca95-11ea-85f9-051ffd4ff56e.JPG" width="591">
*Fig.7 - Complex spectrum produced by ring modulation*
<br />
If you want to learn more about ring modulation check the references section, lots of great resources!
<br />

================================================================================ 

References:
Puckette, Miller. The theory and technique of electronic music. World Scientific Publishing Company, 2007.
Strange, Allen. Electronic music: systems, techniques, and controls. William C Brown Pub, 1983.
Aikin, Jim. Power tools for synthesizer programming: the ultimate reference for sound design. Backbeat Books, 2004.
FLOSS Manuals - http://write.flossmanuals.net/pure-data/amplitude-modulation/
Wikipedia page - https://en.m.wikipedia.org/wiki/Ring_modulation
