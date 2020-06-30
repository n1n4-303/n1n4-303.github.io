---
layout: default
title: "Introduction to waveshaping"
permalink: /tutorials/waveshaping
---

# Introduction to waveshaping

<br />Waveshaping is a distortion technique that allows us to modulate a signal amplitude, controlling the way that the amplifier processes the waveform by using a non-linear transfer function.
<br />An amplifier is used to increase the voltage, current, or power of a signal and amplifiers have a transfer function, which is basically a graph relating the input to the output of a signal. 
<br />A linear transfer function is a straight line and will leave a given signal unchanged, if you for instance increase the amplitude of the input signal by 2 it will double the output signal. However, a deviation from that straight line will introduce distortion. Having control over that amount is musically interesting since waveshaping is an efficient way to create complex timbres. With a non-linear transfer function we can create different waveform shapes by altering the transfer function shape. This will allow you to play around with the spectrum and harmonic content of the waveform.
<br />On pure data, there is an object called [clip~] and what clip does is to pass a signal input to the output, clipping it to lie between two limits (you can check this with details in the help patch), which you will specify by giving it two arguments. [clip~] will pass the input to the output unchanged as long as it stays between the limits we established.
