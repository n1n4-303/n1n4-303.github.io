---
layout: default
title: "Waveform symmetry and timbre"
permalink: /tutorials/wave-symmetry
---

# Waveform symmetry and timbre

<br />In my introductory tutorial on waveshaping (link) I told you about the possibility of building different waveforms and how that might be musically interesting. For that first tutorial, I used [clip~] to exemplify how waveshaping works, however, there are other ways to produce different transfer functions that you can use for multiple purposes.
<br />In this tutorial I'm going to use [cos~] as a transfer function to demonstrate the relationship between waveform symmetry and tone quality or timbre. What [cos~] does is multiplying its input by 2pi and giving the cosine of the result. An important thing to remember about [cos~] is that it takes its input in cycles, so your input should range from 0 to 1. My patch is based on professor Puckette's UCSD course, so if you're interested, I highly recommend you check that, I'll leave the link on the references section.
<br />
<br />First, I’m going to show you visually the difference between a sine and a cosine function.
