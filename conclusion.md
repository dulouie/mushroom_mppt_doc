---
title: Conclusion
layout: post
nav_order: 10
---

# Conclusion

This work has dealt with the various aspects of
MPP in
PV and the basic
implementation of a solar module optimizer. In this regard, attention
was first drawn to the existing problem of shading and then the
technologies for a solution were presented. The concept of power
adjustment and the operation of the boost converter were explained. The
change of the input resistance of the step-up converter by adjusting the
duty cycle was discussed in more detail.

Subsequently, some requirements were elaborated and a concept for the
operation of the solar module optimizer was developed. The idea of the
concept is to feed the continuous measurement of current and voltage at
the solar module to a programmable controller. Based on its programming,
this controller then decides how to set the control variable for the
boost converter in order to find the MPP.\
According to this concept, the development of the hardware and the
related issues were documented in detail. The coil and capacitor were
sized for the boost converter. Solutions for measuring the current and
voltage were developed, and a voltage divider was sized and a
Hall-effect sensor was selected. A suitable
mosfet was
chosen as the switching element and a suitable gate driver was selected
for it. Furthermore, a snubber cicuit was designed to dampen the
unwanted oscillations when switching the mosfet. In addition, a low-pass filter was sized
to reduce noise at the adc. To be able to program the solar module
optimizer later, a microcontroller was selected. Furthermore, the
hardware provides access to an SD card reader.\
\
Next the software was implemented, for this a class was written to
separate the basic hardware access from the MPP algorithm. In addition, various drivers
for the peripherals of the solar module optimizer were developed. Here,
a method was developed to drive the duty cycle for
mosfet of the
boost converter. Conversion functions for current and voltage
measurements were developed. A class for filtering the measurement data
was developed for further removing noise from the
ADC. A
PID was implemented
to control the output voltage to set point and a recording function for
the SD card reader was implemented to record the measurement data for
later analysis. Subsequently, two algorithms were implemented to search
for the MPP, first
the PO which is most
commonly used, and the *VI scanner* algorithm. With the developed
hardware and software, the solar module optimizer was tested for its
basic functionality, the ripple of the output voltage was determined and
a VI-characteristic
curve of a solar module was recorded. For the investigations under
constant laboratory conditions of a vi-characteristic curve of a
PV-module, a
PV-emulator was
developed. This provides constant characteristics of the emulated solar
module in order to compare the algorithms.\
The PV emulator was
then used to investigate and compare both algorithms, once without
shading and once with shading. Here it turned out that the
PO method cannot
find the global MPP
and dwells in a local MPP. The *VI scanner* turns out to be the
more effective algorithm, and finds the global MPP immediately.

One of the research questions was the feasibility of such a project
using the Micropython programming language, the system needs appropriate
real-time capability to reliably set the pwm with the frequency of $50kHz$. There must
also be enough computing power to read the adc, process the data, and respond. The
feasibility was demonstrated with the successful experiment of studying
a VI characteristic.
This has shown how much faster development occurs with *Micropython*
than with a traditional language such as *C++*. The limitations of
*Micropython*, such as significantly slower processing and a limited
functionality of a few functions, are less relevant in the work, because
the project does not require a fast response in the microsecond range. 

The consideration in the concept of the solar module optimizer to use a
PI controller for the output voltage, and to supply it with a reference
voltage from the MPP controller was a mistake. This lengthens
the controlled system by several elements, resulting in unpredictable
oscillations.

Overall, the goal of implementing a solar module optimizer for
PV-modules was
successfully realized, with minor and major challenges that were solved
with good approaches. The final practical test, despite some weaknesses,
highlights the superiority of the *VI-scanner* over the
PO. Setting the
MPP working point
for the next $60$ seconds is one such point, if the characteristic
changes during this time, it results in a loss of performance. A
possible conclusion for this, is to combine both algorithms. Here, the
VI characteristic
could be sampled first, and then the PO-algorithm could be activated in a small
range around the global MPP for the next $60$ seconds. Here, the step
size could be much smaller than the sampling of the VI scanner.
