---
title: Maximum Power Point Tracking Algorithms
layout: post
nav_order: 8
has_children: true
---

# Maximum Power Point Tracking Algorithms {#kap:mpptalgo}

[mppt]{acronym-label="mppt" acronym-form="singular+short"}-algorithms
are the control methods to be used for this solar panel optimizer to
extract the maximum power from a solar panel. The idea behind these
algorithms is to monitor the output voltage and current of the solar
panel and change the duty cycle of the boost converter to deliver the
maximum power to the load.\
There are several algorithms for [mppt]{acronym-label="mppt"
acronym-form="singular+short"}, including the [po]{acronym-label="po"
acronym-form="singular+short"} method, the *Incremental Conductance*
method, and the *Fractional Open Circuit Voltage* method. The algorithms
operate continuously to adapt to changing conditions and maximize solar
panel performance. In this work, two methods will be selected for
further investigation.
