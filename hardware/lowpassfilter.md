---
title: Lowpassfilter
layout: post
nav_order: 6
parent: Hardware implementation
---

# Lowpassfilter {#kap:tiefpass}

The fast switching of the mosfet induces voltages with higher frequencies
in the whole circuit, which can distort the voltage measurement at the
ADC. To filter out
these frequencies and improve the signal, a simple low-pass filter is
placed after the voltage divider, as shown in [figure](#fig:low-pass). The filter should have a cutoff frequency of
about ${f_{c}=75 Hz}$, for this the resistor $R_{filter}=10k\Omega$ is
determined first. Here $R_{filter}$ should be chosen in the same order
of magnitude as the voltage divider, so that the capacitor $C_{filter}$
can be kept small. However, too large a value is also undesirable,
otherwise the ADC
will no longer be able to measure a signal.

$$\label{eq:lowpass}
C_{filter} = \frac{1}{2\pi R_{filter} f_{c}} = \frac{1}{2\cdot\pi\cdot 10k\Omega\cdot 75Hz} = 212.2 nF$$

The capacitor $C_{filter}$ is calculated according to
\eqref{eq:lowpass} and assigned to a suitable value of the E24
series with $C_{filter} = 220 nF$.
<!--[@scherzmonk p.665]-->

###### Lowpass filter {#fig:low-pass}
![image](../assets/image/tiefpass.svg)
