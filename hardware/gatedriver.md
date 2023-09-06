---
title: Gatedriver
layout: post
nav_order: 3
parent: Hardware implementation
---

# Gatedriver {#kap:gatetreiber}

The mosfet is to
be controlled by a microcontroller with a pwm. The output pin of the microcontroller
has a maximum voltage of $3.2V$, but in order to be able to switch the
power mosfet completely, a voltage of at least $10V$ is required and
thus the mosfet cannot be operated directly with the microcontroller.
For this application, so-called logic-level mosfets exist that switch
through at a gate-source voltage of less than $V_{GS}=5V$. In this work,
however, another way is to be shown, since these logic-level mosfets buy
their properties through a high input capacitance and other
disadvantages. Too high a capacitance at the input would slow down the
switching process. The easiest way to drive this mosfet with the
required voltage is to use a gate driver. This is compatible with the
logic voltage level of the microcontroller and can switch a higher
voltage. A gate driver also makes it possible to provide a very high
current to the gate of the mosfet in a very short time. This allows the
mosfet to be switched much faster. The following questions are asked for
the selection of a gate driver:

-   How many inputs/outputs are required?

-   What is the voltage rating?

-   How much gate current does the mosfet need?

-   Gate voltage of $12V$ possible?

Only one Mosfet is to be switched, so only one input and one output is
needed at the gate driver. The required dielectric strength should be at
least three times higher than the normal operating voltage of the
application, in this case ${V_{max}=3\cdot 12V=36V}$.

The required current of at least ${I_{gate} = 360mA}$ and the associated
switching times were calculated in the [last chapter](mosfet). The
half-bridge driver *IR2104S* from *international Rectifier* is selected,
its characteristics meet the above requirements. 

The dimensioning of the gate resistor $R_{gate}$ is an important aspect
of this circuit. If it is chosen too small, unwanted oscillations can
occur at the gate. On the other hand, the switching process would be
greatly slowed down if the resistor is chosen too large, because too
little current flows into the gate. According to
\eqref{eq:Rgate},
the gate resistor from the E24 series is chosen with
$R_{gate}=37\Omega$.

$$\label{eq:Rgate}
R_{gate} = \frac{V_{12V}}{I_{driver}} = \frac{12V}{360mA} = 33.33\Omega$$

The gate resistor should only limit the current for the rise time,
during the descent time and the discharging process of the gate
capacitance, it should not act. For this reason, a diode $D$ is
connected in parallel to the gate resistor so that the current is not
limited during the descent time. In [figure](#fig:gatedriver) the complete control of the gate is shown.
The [IR2104S](https://www.infineon.com/dgdl/Infineon-IR2104-DS-v01_00-EN.pdf?fileId=5546d462533600a4015355c7c1c31671) is a half-bridge driver where the
high-side connections are not used in this application. These are
connected to ground with an $R_{3}=10k\Omega$ resistor so that there are
no open pins in the circuit. 

$$\label{eq:Rpwm}
R_{1} = R_{2} = \frac{V_{vcc}}{I} = \frac{3.2V}{1mA} = 3.2k\Omega$$

The *PWM* and *SD* signals come from the microcontroller with a $3.3V$
level. The series resistors are calculated according to
\eqref{eq:Rpwm}.
Here the current is limited to $1mA$ to avoid losses.

Another component is the bypass capacitor $C_{bypass}=1\mu F$, its task
is to decouple the chip from the voltage supply, especially in driver
circuits this is an important element. Because higher currents flow very
quickly here and the power supply is more heavily loaded as a
result.

[@IntelligentEnergy p.259] [@datasheet:SLUA618A].

###### Gate driver schematic {#fig:gatedriver}
![image](../assets/image/ir2104.svg)
