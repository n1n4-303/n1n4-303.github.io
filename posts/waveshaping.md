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
<br />
![clip-object](https://user-images.githubusercontent.com/64982634/86159622-8988e400-bb02-11ea-9a27-68573b490612.png)
*Fig.1  Giving arguments to [clip~]*
<br />
![waveshaping-vs-linear](https://user-images.githubusercontent.com/64982634/86159715-a1606800-bb02-11ea-8571-fef5f1876dbc.JPG)
*Fig.2  Difference between an unchanged signal and a clipped signal.*
<br />
The new shape you will create on your output depends on different things:
 - transfer function
 - shape of the incoming wave
 - amplitude of the incoming signal 
<br />
<br />The amplitude of the incoming waveform is called the waveshaping index. The index provides continuous control of the spectrum making possible dynamic spectra through time variation. A small index will generally introduce little distortion, as the index is increased the spectrum becomes richer, see Puckette, 2007.
<br />
<br />I'll show you how you can observe this with pd:
<br />
<img src="https://user-images.githubusercontent.com/64982634/86159745-a8877600-bb02-11ea-95bc-86128911fc5a.JPG" width="591">
*Fig.3 Waveshaping vs linear*
<br />
<br />Video demonstration
<iframe width="560" height="315" src="https://www.youtube.com/embed/q3vaxSWWWg8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />

================================================================================ 
References
Puckette, Miller. The theory and technique of electronic music. World Scientific Publishing Company, 2007.
Dodge, Charles, and Thomas A. Jerse. Computer music: synthesis, composition and performance. Macmillan Library Reference, 1997.
Russ, Martin. Sound synthesis and sampling. Taylor & Francis, 2004.
