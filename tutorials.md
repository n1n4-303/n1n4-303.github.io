---
layout: default
title: "tutorials"
permalink: /tutorials/
---

# Understanding granular synthesis with pure data
  
<br />Granulation is a technique in which you manipulate a short-duration microacoustic event (typically between 1 to 100ms) known as grain, that can be used on sound design to achieve multiple results, like creating unpredictability, for instance. It may be useful if you're thinking sound as a process and you can take it to many interesting directions. If you are interested in learning more deeply about granular synthesis and its possibilities, refer to ROADS, 2004.
<br />Granular synthesis is behind many fancy plugins or built-in fx you are used to see in your DAW of choice, such as Ableton's Grain Delay. A good way to understand how they're used might be to just try to build a simple granular synthesizer yourself.


## Let's do it!

<br />**The recorder**
<br />So we need a way to record an input. We do that by using an analog to digital converter [adc~]. For the sake of organization, we're going to put it into a subpatch, so our patch will look more clear further on.
<br />
![subpatch-recorder](https://user-images.githubusercontent.com/64982634/83361737-46ace280-a383-11ea-8692-bd982ff0bf39.JPG)
