---
title: Boost Converter
layout: post
nav_order: 1
parent: Hardware implementation
---

# Boost converter {#boost-converter}

The mode of operation and the change of the input resistance by the duty
cycle was explained in the chapter
[\[subsec:grund_hochsetzstell\]](#subsec:grund_hochsetzstell){reference-type="ref"
reference="subsec:grund_hochsetzstell"}. For the solar module optimiser
it is important that as wide a range of the input resistance as possible
is covered. However, for the basis of the calculation of the elements of
the boost converter, a limited range shall be used. The minimum input
voltage $U_{in}$ as well as the maximum output voltage $U_{out}$ are
obtained from the specified characteristics. The maximum duty cycle
$d_{max}$ is calculated according to equation
[\[eq:dutymax\]](#eq:dutymax){reference-type="ref"
reference="eq:dutymax"}.

$$\label{eq:dutymax}
d_{max} = 1 - \frac{V_{in}}{V_{out}} = 1 - \frac{15V}{50V} = 0.7$$

Then,
equation [\[eq:dutymin\]](#eq:dutymin){reference-type="ref"
reference="eq:dutymin"} can be used to determine the minimum duty cycle.


$$\label{eq:dutymin}
d_{min} = 1 - \left(\frac{V_{in}}{V_{out}}\right) \cdot (1-d_{max}) = 1 - \left(\frac{30V}{15V}\right) \cdot (1-0,7) = 0,4$$


In order to take into account the different input voltages $V_{in}$, the
calculation of the inductance $L$ is performed with the minimum duty
cycle $d_{min}$ and the maximum input voltage $V_{max}$. The size of the
current ripple $\Delta i_{L}$ is a design decision and is chosen to be
$25\%$ of the maximum input current $I_{in}$. The switching frequency
$f_{s}$ is set to $50kHz$ to keep the size of the inductance small and
to choose a range that is not perceptible to the human ear.

$$\label{eq:induc}
L = \frac{V_{max}d_{min}}{\Delta i_{L} f_{s}} = \frac{30V \cdot 0,4}{2,5A \cdot 50 kHz} = 96 \mu H$$

The equation ([\[eq:induc\]](#eq:induc){reference-type="ref"
reference="eq:induc"}) determines the minimum required inductance $L$
for the boost converter. A toroidal choke with an inductance of
$L=100 \mu H$ and a maximum current carrying capacity of $I_{L}=10A$ is
selected.

To ensure a uniform output voltage, the output voltage delta
$\Delta U_{out}$ shall be $0.1V$ maximum and the output current
$I_{out}$ is fixed at $2A$. The capacitor $C$ on the output side is now
calculated according to [\[eq:Cout\]](#eq:Cout){reference-type="ref"
reference="eq:Cout"}.

$$\label{eq:Cout}
C_{out} = \frac{I_{out}D_{max}}{\Delta V_{out} f_{s}} = \frac{2A \cdot 0,7}{0,1V \cdot 50 kHz} = 280 \mu F$$

The capacitance of the output capacitor should be greater than the
calculated value and is thus chosen to be $C_{out} = 470 \mu F$. The
voltage rating is chosen to be $V_{C_{outmax}}=68V$, as the maximum
output voltage is $V_{out_{max}}=50V$ [@UmanandPower p.212].
