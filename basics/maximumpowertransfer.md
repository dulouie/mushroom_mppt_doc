---
title: Maximum Power Transfer
layout: post
nav_order: 2
parent: Basics
---

# Maximum power transfer {#sec:leistungsanpassung}

Power matching in a solar cell describes a process in which the load is matched to the source. If the
load is not properly matched to the cell, this can lead to a loss of
energy as the maximum possible current does not flow. To maximise the
power of a solar cell, the load must be matched to the internal
resistance of the cell. The resistance depends on the electrical
properties of the cell and varies with sunlight intensity, temperature
and other factors. When the load is optimally matched to the internal
resistance of the cell, the solar cell can deliver its maximum power.

![image](assets/image/konzept1.png)

If a variable load resistor is connected to the solar cell, as shown in
figure [\[fig:leistanpass\]](#fig:leistanpass), the dark red characteristic curve of the
resistor can be entered in the diagram
[\[fig:ui-leist\]](#fig:ui-leist) as the consumer. The dark blue characteristic
curve of the solar cell is the generator in this case. If this load
resistor is adjusted, the characteristic curve of the resistor changes
and thus also the intersection of source and consumer. In figure
[\[fig:leistanpass\]](#fig:leistanpass) the adjusted load resistances are visible
at the *dashed* characteristic curves. The intersection of the
characteristic curve of the solar module and a characteristic line of
the load resistance is the operating point. The area of current and
voltage under this operating point is the power to be maximised. By
changing the load resistance, the operating point on the characteristic
curve of the solar module can therefore be adjusted. In order to be able
to use the concept of power adjustment for the solar module optimiser, a
circuit is therefore needed that can continuously change its input
resistance in order to be able to adjust the point of power and thus
maximise the energy transport, such a circuit is presented in the next
section [3.3](#kap:hochsetz) [@büttner p.37].

TODO p5js
