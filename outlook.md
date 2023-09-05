---
title: Outlook
layout: post
nav_order: 11
---

# Outlook

The question of how the solar module optimizer behaves with a real solar
cell under partial shading could not be investigated in this work.
However, the PV
emulator shows very similar behavior compared to a real solar cell.
Here, the experimental trial with two same solar cells and the module
optimizers but different algorithms under environmental conditions could
be another research project. In this case, data should be recorded on
the SD card over 24 hours for later comparison.

The programmable solar module optimizer can be used as a platform for
the development of more advanced algorithms. Here, additional sensors
such as the temperature of the solar cell or weather data can be
obtained via a WIFI-connection. Solar cells with a different
technology such as thin-film or perovskite, which have a more complex
characteristic curve to collect, are of interest. In addition, a
connection to a AI
could be established through the serial interface or
WIFI, this would
allow the analysis of much more complicated characteristics.

In addition, the PI controller can be adapted to the extent that the
output voltage is no longer observed, but the output current, this would
probably make the control loop usable again to thus realize a
functioning charge controller, this could then charge a lead battery,
for example. Here the output voltage would always be pulled to the $12V$
of the lead acid battery and the additional energy of the coil, results
not in a higher output voltage, but in a larger charge current.
Different MPP
charge controller algorithms could be investigated.

Furthermore, the *Mircopython* approach allows the platform to be used
for teaching, because it greatly facilitates programming, and through
this, a better understanding of VI-characteristics can be given to MPP and PV. 
