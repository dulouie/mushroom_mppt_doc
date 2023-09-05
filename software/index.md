---
title: Software implementation
layout: post
nav_order: 7
has_children: true
---

# Software implementation

The implementation of the software is the next important step for the
development of the solar module optimizer. In this chapter we will look
at how the software for the module optimizer is developed and
implemented. The software is intended to control the RP2040
microcontroller so that the system is able to sample measurement data,
process it, and be able to control the keying time.

In particular, the
*Micropython* programming language and the required libraries will be
discussed. The implementation is described in sections for the
respective peripherals and the individual functions of the software are
explained. The listings of the *Micropython* code are described in the
text but shown without comments, this is based in the trivial properties
of *Micropython* and the clarity. In order for the algorithm to access
the peripherals of the microcontroller, a class *MPPTController* is
created in Listing [\[listing:1\]](#listing:1){reference-type="ref"
reference="listing:1"} using object-oriented programming. These make it
possible to define various methods and attributes [@micropython].

```python
@singleton
class MPPTController():
    ''' Hardware abtraction layer for MPPTController'''
    def __init__(self):
        self.pwm = PWM(Pin(6, Pin.OUT))
        self.pwm.freq(50000) 
        self.sd = Pin(7, Pin.OUT)
        self.adc1 = ADC(Pin(26, Pin.IN))
        self.adc2 = ADC(Pin(27, Pin.IN))
        self.adc3 = ADC(Pin(28, Pin.IN))
        self.adc4 = ADC(Pin(29, Pin.IN))
        self.filter1 = FilterAvg(adc=self.adc1, samples=150)
        self.filter2 = FilterAvg(adc=self.adc2, samples=150)
        self.filter3 = FilterAvg(adc=self.adc3, samples=150)
        self.filter4 = FilterAvg(adc=self.adc4, samples=150)
        self.filtered = [0.,0.,0.,0.]
        self.voltage = [0.,0.]
        self.current = [0.,0.]
        self.power = [0.,0.]
        self.duty = 0
        self.vRef = 0.
        self.pid = PID(scale='ms')
```

The *MPPTController* class is implemented as a singleton to ensure that
only one instance of this class exists to access the hardware. The
singleton design pattern avoids collisions and inconsistencies when
accessing the hardware resource and improves structure and
maintainability.

In addition, implementation as a singleton provides the
advantage of encapsulation between the peripheral and the algorithm that
contains the logic for finding the MPP. The *MPPTController* class provides a
hardware abstraction layer for the MPPT controller, and the *device*
instance is later created from it. The attributes of this class provide
access to various hardware components such as the
PWM, a shutdown
option *SD*, and four ADC, each of which is associated with a
filter to ensure a noise-free signal.

In addition, the class has
attributes for storing measured quantities such as voltage, current,
power, and duty cycle. The voltage, current, and power are each stored
for the input side and the output side respectively. In addition, a
PID is initialized
to regulate the output voltage to the setpoint *vRef* passed by the MPPT
algorithm [@singleton].
