---
title: Microcontroller
layout: post
nav_order: 8
parent: Hardware implementation
---

# Microcontroller

When choosing a controller, various factors such as the availability of
interfaces, computing power and the number of inputs and outputs must be
taken into account. For the current project the RP2040 microcontroller
from Raspberry Pi is chosen, one reason for using the RP2040 is its
compatibility with *MicroPython*. This makes programming easier and
speeds up the development of a prototype. The RP2040 has at least 4
ADC which are
important for analog signal acquisition, these are used for various
applications such as voltage measurement and current measurement.

Another aspect is the speed of the controller. The RP2040 has a
dual-core architecture and a clock frequency of up to 133 MHz. This
enables it to perform complex calculations quickly and process data in
real time, even though it is programmed with the slow language
*Micropython*.

Another feature of the RP2040 is its PWM capability, which allows fine
control of analog signals. The controller is capable of generating PWM
outputs at a frequency of the required 50 kHz, which is important for
controlling the duty cycle $d$.\
Specifically, the *XIAO RP2040* module from *Seeed Studio* is used, and
the interconnection with the other parts of the project is shown in
Figure [\[fig:rp2040\]](#fig:rp2040){reference-type="ref"
reference="fig:rp2040"}. The two outputs *GPIO6* and *GPIO7* which drive
the gate driver are populated with resistors of
$R_{pwm}=R_{sd}=330\Omega$ to limit the current to
$1mA$ [@datasheet:RP2040].

![image](/assets/image/rp2040.svg)
