---
title: Voltage measurement
layout: post
nav_order: 5
parent: Hardware implementation
---

# Voltage measurement {#kap:spannungsmessnung}

For the algorithm of the MPPT controller, the input voltage and the output voltage at the solar module optimiser are required. These voltages are to be measured with a ADC, which is available as a peripheral as
part of the microcontroller. The measurable voltage range of these
ADC is $0V < V_{adc} < 3.3V$ and is thus significantly smaller than the voltages of $0V < V_{in/out} < 50V$ applied to the solar module optimiser. In order to be able to measure the larger voltages with the
ADC, a voltage divider is dimensioned as shown in figure
[\[fig:tiefpass\]](#fig:tiefpass){reference-type="ref"
reference="fig:tiefpass"}, which only passes on a fraction of the high voltage but with the correct ratio to the ADC. The voltage divider ratio between
$R_{1}$ and $R_{2}$ determines this ratio so that the input voltage of $V_{in}= 50V$ corresponds to a measured voltage at the ADC of $V_{adc} = 2.9V$. Some free space is built in here to have protection against overvoltages [@scherzmonk pp.56-57].

![image](import/tiefpass.pdf){width="0.4\\linewidth"} []{#fig:tiefpass
label="fig:tiefpass"}

The resistance values for $R_{1}$ and $R_{2}$ are calculated as follows:

-   A very high input impedance $Z > 100k\Omega$ of the
    ADC is assumed according to the data sheet, so the voltage divider is calculated as
    unloaded.

-   The output voltage can thus be used directly according to:

    $$ U_{out} = U_{in}\frac{R_{2}}{R_{1}+R_{2}} \label{voltageDiv1} $$

-   To prevent the current across the resistors from becoming too large
    and generating unnecessary losses, $R_{2} = 2.2k\Omega$ is chosen.

-   For $R_{1}$ \eqref{voltageDiv1} is transformed to: 

    $$ \label{voltageDiv2}
     R_{1} = R_{2}\frac{V_{in}-V_{out}}{V_{out}} = 2.2k\Omega\cdot\frac{50V-2.9V}{2.9V} = 35.7 k\Omega $$

-   Resistors are selected from the E24 resistor series with
    $R_{1}=36k\Omega$ and $R_{2}=2.2k\Omega$.
