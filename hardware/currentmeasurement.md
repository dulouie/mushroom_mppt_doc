---
title: Current measurement
layout: post
nav_order: 7
parent: Hardware implementation
---

# Current measurement {#kap:strommessung}

For the measurement of the current, a different method is required than
for the voltage measurement. The current can only ever be measured
indirectly, either via a voltage drop across a shunt resistor and Ohm's law $I=V_{shunt}/R_{shunt}$ or via the generated magnetic field of a current-carrying conductor. In this paper, the latter will be demonstrated by the implementation of a Hall-effect sensor chip. The TMCS1108 chip from Texas Instruments is chosen because it meets the following requirements:

-   voltage range $\pm100V > 50V$ of the solar module optimizer.

-   Supply voltage of $V_{vs}=3.2V$ possible

-   Wide current measurement range in different configurations up to
    $\pm 46A$.

-   Low error of $\pm1\%$

-   Analog output voltage $0V<V_{out}<3.3V$ matching the
    ADC of the microcontroller

The following assumptions are made for the design:

-   $I_{in} = 10A$ current to be rated

-   $V_{vs,nom} = 3.2V$ Normal supply voltage

-   $V_{vs,min} = 3.1V$ minimum supply voltage

-   $Swing_{vs} = 0.2 V$ fluctuations of supply voltage

The chip is available in different variants with different sensitivities $S$. When choosing, it should be noted that the sensitivity should not be chosen too small, otherwise the connected ADC can no longer measure the voltage changes, for the selection proceed as follows:

-   Should the current be measured unidirectionally or bidirectionally?
    The current flows only in one direction, so a variant of type
    $(A1U-A4U)$ is chosen for unidirectional.

-   Output voltage at $I_{in} =0A$ is:
    $V_{out,0A}= 0.1 \cdot V_{vs} = 0.32V$

-   The transfer function is calculated according to \eqref{eq:tmcs1108trans} 
    
    $$ \label{eq:tmcs1108trans} V_{out} = I_{in} \cdot S + V_{out,0A}$$

-   To maximize sensitivity over the desired linear measurement range,
    the maximum linear output voltage range
    \eqref{eq:tmcs1108linaussteuer} is calculated:

    $$ \label{eq:tmcs1108linaussteuer}
            V_{out,max} - V_{out,0A} = V_{vs,min} - Swing_{vs} - 0.1 \cdot V_{vs,min} $$

The design parameters for the calculated output range are shown in the
[table](#tab:design).

###### Design Parameters {#tab:design}

| **Design parameter**         | **Value** |
|------------------------------|-----------|
| $Swing_{vs}$                 | $0.20V$   |
| $V_{out,max}$                | $2.90V$   |
| $V_{out,0A}~at~V_{vs,min}$ | $0.31V$   |
| $V_{out,max} - V_{out,0A}$   | $2.58V$   |

The parameters show a maximum positive linear voltage step of $2.58V$. In order to select the appropriate sensitivity that fully utilizes this linear range, the maximum current is calculated according to \eqref{eq:ibmax}, where $S$ are the different sensitivity variants of the sensor.

$$ \label{eq:ibmax}
I_{B,max} = \frac{V_{out,max} - V_{out,0A}}{S} $$

The choice falls on the [TMCS1108A3U](https://www.ti.com/lit/ds/symlink/tmcs1108.pdf?ts=1694006955334&ref_url=https%253A%252F%252Fwww.google.com%252F) because it
covers a measuring range of ${0A \rightarrow +12.9A}$ at a supply
voltage of ${V_{vcc}=3.2V}$ with a sensitivity of $S = 200mV/A$, which
corresponds to the highest triggering for the range
${0A \rightarrow +10A}$ of the solar module optimizer.\
\
The output voltage of the chip $VOUT$ should be as free of noise as
possible to reduce measurement errors. Therefore, a low-pass filter with
a cutoff frequency of $f_{c}=75Hz$ is also used here as shown in chapter
[lowpassfilter](lowpassfilter).
The maximum voltage at the ADC is equal to the supply voltage
$V_{vs}=3.2V$ of the chip, so the whole range of the
ADC is used.

[Figure](#fig:tmcs1108) shows how the chip is wired up, this involves routing the high current to be measured through two input pins and two output pins, any heat generated is dissipated through generous copper areas and vias. Another important element is the bypass capacitor $C_{bypass}=0.1\mu F$ of the chip's power supply, it compensates voltage fluctuations and decouples the chip from the rest of the components, without the bypass capacitor the measurement error of the current measurement would be significantly larger. Its placement should be as close as possible to the pin *VS* of the supply voltage. 

###### Schematic TMCS1108 {#fig:tmcs1108}
![image](../assets/image/tmcs1108.svg)
