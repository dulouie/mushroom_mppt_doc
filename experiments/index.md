---
title: Practical experiments
layout: post
nav_order: 9
has_children: true
---

# Practical experiments {#kap:experiment}

In this chapter, experimental tests will be carried out to investigate
the properties of the solar module optimizer and compare the performance
of the implemented algorithms. Various measurements are performed and
the results are evaluated to analyze the operation and properties of the
optimizer. The chapter is divided into two main sections. In the first
section, the basic operation of the solar module optimizer is reviewed,
while in the second section a comparison of the algorithms is performed.
The aim is to show the advantages and disadvantages of the different
algorithms in order to identify the optimal method for the application
of the solar module optimizer. For the experiments, an ohmic heating mat
with a resistance of $R_{L}=24\Omega$ is connected to the output of the
module optimizer.

###### Basic PV emulator {#pvbasic} 

![image](../assets/image/pv_emulator1.svg)

In order to keep the experiments comparable and to always have the same
laboratory conditions, no experimental trial with a
PV-module under
environmental conditions is performed, instead a PV emulator based on
the principles of the paper *Simple and Fast Dynamic Photovoltaic
Emulator based on a Physical Equivalent PV-cell Model* by Khawaldeh et
al. is used. The emulator is based on the single-diode
equivalent circuit of a PV-module, here a current source and a
series connection of power diodes are connected together in the flux
direction, and a series and a parallel resistor are also added, as shown
in [Basic PV emulator](#pvbasic). The number of diodes, the maximum current of
the source and the resistor values can be varied to change the
characteristic.

###### Shaded PV emulator {#pvshaded}

![image](../assets/image/pv_emulator2.svg)

For this experimental setup, power devices designed for higher heat
generation are used, such as the power diode *P600D* with a number of
$N=30$ as well as a parallel resistance of $R_{p}=220 \Omega$ and a
series resistance of $R_{s}= 0.4 \Omega$, and active air cooling is also
required. 

Another experiment is to record a VI-characteristic curve from a solar module
under partial shading, but for this the PV emulator must be wired
slightly differently. The partial shading is emulated with an additional
lower current source, which affects only a small part of the series
connection from the diodes. Both current sources are wired according to
[pv emulator shaded](#pvshaded). Also, two bypass diodes must be added to allow
current to flow through the circuit even if some diodes become shaded.
The same diodes are used for this as for the series connection. The PV
emulator should now exhibit very similar behavior to a standard solar
module that is one-third shaded, with an open circuit voltage
$V_{oc}=21V$, the short circuit current of $I_{sc}=5A$, and two bypass
diodes.

###### PV emulator picture

![image](../assets/image/pvemulator.jpg)
