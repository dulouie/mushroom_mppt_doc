---
title: Pulse width modulation
layout: post
nav_order: 1
parent: Software implementation
---

# Pulse width modulation

PWM (pulse width modulation) is a technique for generating an analog
signal by a digital control. It involves generating a digital signal at
a specific frequency that alternates between the two states *low* and
*high*. By changing the ratio between the duration of the signal in the
two states, the average signal can be adjusted, which is an effective
method for controlling electronic devices. The ratio is called the duty
cycle and can be controlled by changing the duty cycle and the period of
the signal generation. The function *setDutyCycle()* is a method of the
class *MPPTController* and is used to set the duty cycle of the mosfet
in a percentage for the boost controller. The *duty* input is
interpreted as a percentage of the duty cycle time, where 100% means
full duty cycle time and 0% means full inhibit time. To set the duty
cycle as a 16-bit integer for PWM control, the entered percentage is
first subtracted from 100% to get the lockout time percentage. This
value is then multiplied by 65536 and the result rounded to the nearest
integer to obtain the duty cycle as a 16-bit value. Finally, the PWM
dutycycle is set to the calculated value using the *duty_u16 method()*.

::: listing
``` {.python frame="lines" linenos="" xleftmargin="2em"}
def setDutyCycle(self, duty):
    '''Set mosfet dutycycle for boost converter'''
    self.duty = int(((100 - duty) / 100) * 65536)
    self.pwm.duty_u16(self.duty)
```
:::
