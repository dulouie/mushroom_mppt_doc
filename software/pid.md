---
title: PID Controller
layout: post
nav_order: 4
parent: Software implementation
---

# PID Controller {#kap:pid}

A PID is a method
that comes from control engineering, the controller continuously
determines the deviation between the current value of a process to be
controlled and a specified setpoint. On the basis of this deviation
three components are calculated and added up, the proportional part to
the deviation *$K_{p}$*, the part to the change in relation to the past
*$K_{I}$* and the part to fast change *$K_{D}$*. Through the interaction
of these components, an actuating value is calculated, which in turn
acts on the process to reduce the deviation. The *simple-pid* library is
used in this project to simplify the implementation of the PID
controller to regulate the boost converter output voltage to the
specified setpoint.

In Listing [\[listing:6\]](#listing:6){reference-type="ref"
reference="listing:6"} a simple control loop is implemented, this
controls the output voltage of the boost converter constantly to $25V$.
The controller is additionally limited at its output to the minimum and
maximum duty cycle $0\%$ to $70\%$ of the boost converter.

```python
device.pid.tunings = (1.82, 60.45, 0)
device.pid.output_limits = (0, 70)
device.pid.setpoint = 25.

while(True):
    device.getfilteredADC()
    device.calcADCData()
    duty = device.pid(device.voltage[1])
    device.setDutyCycle(duty)
```

The Ziegler-Nichols method of stability limit is a common method of
adjusting PID controllers based on determining the critical gain and
period at which the system is just at the limit of stability. In this
process, the gain *$K_{P}$* is gradually increased until the system
begins to oscillate. The period of these oscillations is measured with
an oscilloscope, which determines the time constant of the boost
controller, here a critical gain of $K_{u}=4.03$ and a time constant of
$T_{u}=36ms$ is obtained.

In this project, a PI controller is initially
chosen because the control deviation should be kept to a minimum and
overshoot is undesirable. The parameters $K_{p}=1.82$ and $K_{i}=60.45$
for the PI controller are calculated according to table
[3](#table:ziegler){reference-type="ref" reference="table:ziegler"}. For
further optimization, an ordinary PID controller and a controller
without overshoot are also listed
here [@ziegler1942optimum; @simplepid].

| Type         | $K_{p}$     | $K_{i}$              | $K_{d}$            |
|--------------|-------------|----------------------|--------------------|
| PI           | $0.45K_{u}$ | $0.54 K_{u} / T_{u}$ | -                  |
| classic PID  | $0.60K_{u}$ | $1.20K_{u} / T_{u}$  | $0.075K_{u} T_{u}$ |
| no overshoot | $0.20K_{u}$ | $0.40K_{u} / T_{u}$  | $0.066K_{u} T_{u}$ |
