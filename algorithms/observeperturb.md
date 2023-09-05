---
title: Observe & Perturb
layout: post
nav_order: 1
parent: Maximum Power Point Tracking Algorithms
---

# Observe & Perturb

The PO-method is the
most commonly used algorithm for finding the MPP, its operation is explained using the
state diagram from Figure
[\[fig:observeperturb\]](#fig:observeperturb){reference-type="ref"
reference="fig:observeperturb"}. First of all, the voltage $V_{pv}$ and
current $I_{pv}$ at the solar module are measured and processed, then
the current power is calculated, the power delta $P_{pv}$ and the
voltage dela $V_{pv}$ with respect to the previous run. Then it can be
checked whether the power delta has changed positively or negatively. If
the power delta is larger, the next step is to find out if the voltage
delta has also changed, and the reference $V_{ref}$ can be increased or
decreased by the step size $dV$ accordingly. The algorithm runs on the
microcontroller in an infinite loop, continuously optimizing the
performance of the solar panel.

During implementation, it turns out that the PO-algorithm does not work together with the
PI controller from chapter [6.4](#kap:pid){reference-type="ref"
reference="kap:pid"}. When the maximum current flows out of the solar
module, and then the duty cycle of the boost converter is further
increased, the voltage at the solar module collapses because not enough
current can be supplied, but the PI controller continues to increase the
duty cycle to regulate to reference voltage, further worsening the
situation. This leads to an unusable operating state, which the
controller cannot leave by itself. For this reason, the duty cycle $d$
is set directly [@PowerGreenEnergy p.313].

![image](assets/image/observeperturbflow.svg)