---
layout: default
title: "Waveform symmetry and timbre"
permalink: /tutorials/wave-symmetry
---

# Waveform symmetry and timbre

<br />In my introductory tutorial on [waveshaping](https://n1n4-303.github.io/tutorials/waveshaping) I told you about the possibility of building different waveforms and how that might be musically interesting. For that first tutorial, I used [clip~] to exemplify how waveshaping works, however, there are other ways to produce different transfer functions that you can use for multiple purposes.
<br />In this tutorial I'm going to use [cos~] as a transfer function to demonstrate the relationship between waveform symmetry and tone quality or timbre. What [cos~] does is multiplying its input by 2pi and giving the cosine of the result. An important thing to remember about [cos~] is that it takes its input in cycles, so your input should range from 0 to 1. My patch is based on professor Puckette's UCSD course, so if you're interested, I highly recommend you check that, I'll leave the link on the references section.
<br />
<br />First, I’m going to show you visually the difference between a sine and a cosine function.
<br />
<img src="https://user-images.githubusercontent.com/64982634/87284086-e5ce0980-c4ed-11ea-9c06-15c6f1f53967.png" width="297">
*Fig.1 Sine function symmetry*
<br />
![image_2020-07-10_16-34-03](https://user-images.githubusercontent.com/64982634/87284164-f7171600-c4ed-11ea-9a20-78a193fcfdea.png)
*Fig.2 Cosine function symmetry*
<br />
<br />As you can see, the "sin" function graph, is symmetric with respect to the origin - if you flip the x to negative x you still have the same y value and the “cosine” graph is symmetric to the y-axis.
<br />A sine function will produce only odd harmonics whereas a cosine function will produce even harmonics. In other words, a sine function will repeat the exact same thing for its subsequent cycles and a cosine function will do one thing for half the cycle and then do the same thing backwards for the other half, like a mirror image. This symmetric relationship is important when it comes to musical intention, since sonically this will produce different results as odd and even harmonics have different tone qualities.
<br />
<img src="https://user-images.githubusercontent.com/64982634/87284270-1615a800-c4ee-11ea-9479-71ed83c96bb8.JPG" width="591">
*Fig.3 Sine transfer function spectrum analysis*
<br />
<img src="https://user-images.githubusercontent.com/64982634/87284340-29287800-c4ee-11ea-917d-82f2c2fd2917.JPG" width="591">
*Fig.4 Cosine transfer function spectrum analysis*
<br />
<br />Note that because of its symmetry, the cosine fuction will double the frequency that we hear. What I did here was using an [osc~] to read from these two different tables and observe the results. I created an Index control and made the signal range from 1 to 100 by multiplying by 50 and then adding 51 and used [tabread4~] to read the table. How I'm drawing these functions to the table here is not relevant to the point I'm making at the moment since we're going to use [cos~] later.
<br />
<img src="https://user-images.githubusercontent.com/64982634/87286005-2d559500-c4f0-11ea-91e5-52e221c3d651.JPG" width="591">
*Fig.5 Sine function waveform*
<br />
<img src="https://user-images.githubusercontent.com/64982634/87286065-42322880-c4f0-11ea-8e2c-8e54a3d547cb.JPG" width="591">
*Fig.6 Cosine function waveform*
<br />
<br />As you can see, the transfer function determines your control over the shape and harmonic content of the waveform. Remember that the harmonics are what makes us differentiate between two different instruments playing the same pitch.
<br />
<iframe width="560" height="315" src="https://www.youtube.com/embed/K55meFGz0Yo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />
Now I will show you how to add some extra control to your patch, because you can transform the symmetry of the function. There is a help patch that uses the same technique in a different way, E07.evenodd.pd. And this time we won't need to read from a table, we're just using the [cos~] object instead.
<br />
<img src="https://user-images.githubusercontent.com/64982634/87286143-6130ba80-c4f0-11ea-91fe-4b55bebf695f.JPG" width="591">
*Fig.7 - Offset control*
<br />We're using a non-linear transfer funcion - [cos~] - and we're adding an offset control, so you will basically have an even/odd control and transform the symmetry of the waveform, because you are changing the point from where you start reading.
<br />Let's take a look at the amount of control you can have over timbre with this technique.
<br />
<iframe width="560" height="315" src="https://www.youtube.com/embed/K4JNFZS_74E" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
<br />You definitely don't have to know this to make electronic music, however, this kind of knowledge can save you a lot of time in expressing your ideas because it becomes easier to understand how to reach that sound you have in your head.

================================================================================ 
References:
Russ, Martin. Sound synthesis and sampling. Taylor & Francis, 2004.
Dodge, Charles, and Thomas A. Jerse. Computer music: synthesis, composition and performance. Macmillan Library Reference, 1997.

Links to UCSD course: 
https://podcast.ucsd.edu/watch/wi16/mus171wi16/2/screen
http://msp.ucsd.edu/syllabi/171.16w/index.htm

