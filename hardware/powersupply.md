---
title: Power supply
layout: post
nav_order: 9
parent: Hardware implementation
---

# Power supply

The solar module optimizer is intended to operate without an external
power supply and generate its own operating voltages from the solar
module voltage. The power supply is implemented by using a linear
regulator to regulate the from up to $30V$ input voltage to a constant
$12V$ output voltage for the mosfet. Another linear regulator is used to
provide a constant $3.3V$ voltage for the microcontroller and sensors.
Both linear regulators feature good stability, which ensures that the
generated voltages are stable and reliable.

![image](/assets/image/spannungsversorgung.svg)

The voltage regulators are implemented according to the data sheet, here
additional capacitors are added on input and output side, with component
values $C_{1}=C_{2}=330nF$, $C_{3}=10\mu F$ and $C_{4}=22\mu F$, the
interconnection is shown in figure
[\[fig:versorungung\]](#fig:versorungung){reference-type="ref"
reference="fig:versorungung"} [@datasheet:LM7812].