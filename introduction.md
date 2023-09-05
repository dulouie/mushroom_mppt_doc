---
title: Introduction
layout: post
nav_order: 2
---

# Introduction

Solar energy is an important and increasingly used renewable energy
source to meet global energy needs and combat climate change. However,
the power generation of an PV-module, hereafter referred to as a solar
module, is highly dependent on environmental conditions such as
temperature, irradiation and shading. Shading in particular can lead to
a significant reduction in power generation, as the current flow through
the affected cells is interrupted and thus the maximum power cannot be
achieved. In order to optimise the power generation of solar modules
even under fluctuating environmental conditions, various
MPPT-algorithms are used. 

A MPPT-algorithm determines the optimal
operating point between the solar module and the connected load. In
doing so, the resistance of the load is adjusted by power adjustment to
such an extent that the maximum power can flow between the solar module
and the load.

Within the scope of this work, a solar module optimiser is to be
developed that is programmable and thus makes it possible to investigate
various MPPT-algorithms with a higher programming
language. The solar module optimiser should thereby increase the
efficiency of the solar cells and thus improve the energy yield.

The use of a higher programming language makes the topic accessible to a
wider circle of developers and enables rapid prototype development. The
objective of the thesis is to implement the programmable solar module
optimiser and to answer the questions arising during the development
process with suitable solution approaches. Furthermore, this work will
also investigate the feasibility of implementing a project with required
real-time capability using the programming language *Mircopython*.
Finally, it will be experimentally investigated which of the selected
MPPT-algorithms
allows the best power generation in the presence of shadowing.

Overall, the development of the programmable solar module optimiser
should contribute to being able to compare different algorithms and
provide a platform for the development of new algorithms.
