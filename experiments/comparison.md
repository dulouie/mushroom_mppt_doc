---
title: Comparison of algorithms
layout: post
nav_order: 2
parent: Practical experiments
---

# Comparison of algorithms {#kap:algovergleich}

How the two algorithms from chapter
[6.6](#kap:mpptalgo){reference-type="ref" reference="kap:mpptalgo"} also
behave under shadowed conditions will be clarified in this chapter. For
this purpose, the [pv]{acronym-label="pv" acronym-form="singular+short"}
emulator is used again, but with the shadowed configuration of two
different current sources and the bypass diodes, for this the setting of
the current sources is kept. The time for the experimental frame shall
be $t=10min$ for both algorithms and the settings of the
[pv]{acronym-label="pv" acronym-form="singular+short"} emulator remain
the same, also both algorithms are tested once with and without
shadowing. A logging function is added to both algorithms, seen in
Listing [\[listing:8\]](#listing:8){reference-type="ref"
reference="listing:8"}, which always logs which point on the PV
characteristic is being sampled. In order to better nastand the
progression and search of the algorithms for the
[mpp]{acronym-label="mpp" acronym-form="singular+short"}, the operating
points are shown together with the characteristic curves from Figure
[\[fig:iu-kenn-pvemu1\]](#fig:iu-kenn-pvemu1){reference-type="ref"
reference="fig:iu-kenn-pvemu1"} and
[\[fig:iu-kenn-pvemu2\]](#fig:iu-kenn-pvemu2){reference-type="ref"
reference="fig:iu-kenn-pvemu2"}. The first experiment is performed with
the [po]{acronym-label="po" acronym-form="singular+short"} algorithm and
a unshaded solar module, the red operating points are shown in Figure
[\[fig:iu-kenn-emu-algo1\]](#fig:iu-kenn-emu-algo1){reference-type="ref"
reference="fig:iu-kenn-emu-algo1"}. As expected, the algorithm scans up
to the global [mpp]{acronym-label="mpp" acronym-form="singular+short"},
and oscillates around this point in small steps.

![image](import/pv-emu-perturb.pdf){width="0.8\\linewidth"}
[]{#fig:iu-kenn-emu-algo1 label="fig:iu-kenn-emu-algo1"}

The algorithm can solve this task satisfactorily and shows how easy the
search for the [mpp]{acronym-label="mpp" acronym-form="singular+short"}
can be implemented. However, in another experiment with a shaded solar
module, a weakness of this algorithm becomes apparent.\
\
As seen in Figure
[\[fig:iu-kenn-emu-algo1-verschattet\]](#fig:iu-kenn-emu-algo1-verschattet){reference-type="ref"
reference="fig:iu-kenn-emu-algo1-verschattet"}, the algorithm dwells in
the local [mpp]{acronym-label="mpp" acronym-form="singular+short"} at
$V_{pv}=23V$ and will never find the global [mpp]{acronym-label="mpp"
acronym-form="singular+short"} because its decision making is based on
the slope of the [pu]{acronym-label="pu" acronym-form="singular+short"}
characteristic. The global [mpp]{acronym-label="mpp"
acronym-form="singular+short"} is at $U_{pv}=13V$ and is the much more
powerful operating point.\
Next, the IU scanner algorithm is tested with the normal IU
characteristic of the PV emulator without any shading. As visible in
figure
[\[fig:iu-kenn-emu-algo2-unverschattet\]](#fig:iu-kenn-emu-algo2-unverschattet){reference-type="ref"
reference="fig:iu-kenn-emu-algo2-unverschattet"} at the red operating
points the [mpp]{acronym-label="mpp" acronym-form="singular+short"} of
this characteristic curve is well hit with some small deviations, the
deviations are attributed to smaller measurement deviations and the
heating of the diodes in the PV emulator.

![image](import/pv-emu-perturb_verschattet.pdf){width="0.8\\linewidth"}
[]{#fig:iu-kenn-emu-algo1-verschattet
label="fig:iu-kenn-emu-algo1-verschattet"}

![image](import/pv-emu-iu-scanner-unverschattet.pdf){width="0.8\\linewidth"}
[]{#fig:iu-kenn-emu-algo2-unverschattet
label="fig:iu-kenn-emu-algo2-unverschattet"}

The test with the IU scanner and a shadowing of the
[pv]{acronym-label="pv" acronym-form="singular+short"} emulator shows
that by scanning the characteristic line several times, the global more
powerful [mpp]{acronym-label="mpp" acronym-form="singular+short"} is
easily found. The red operating points from Figure
[\[fig:iu-kenn-emu-algo2-verschattet\]](#fig:iu-kenn-emu-algo2-verschattet){reference-type="ref"
reference="fig:iu-kenn-emu-algo2-verschattet"} coincide well this time
with the global [mpp]{acronym-label="mpp" acronym-form="singular+short"}
of the shaded PV emulator.\
\
In summary, the [po]{acronym-label="po" acronym-form="singular+short"}
algorithm is clearly inferior to the IU scanner algorithm in terms of
the global [mpp]{acronym-label="mpp" acronym-form="singular+short"}. In
return, the [po]{acronym-label="po" acronym-form="singular+short"} can
react faster to short-term shifts of the characteristic curve, because
here the [mpp]{acronym-label="mpp" acronym-form="singular+short"} is not
set for the next 60 seconds.

![image](import/pv-emu-iu-scanner-verschattet.pdf){width="0.8\\linewidth"}
[]{#fig:iu-kenn-emu-algo2-verschattet
label="fig:iu-kenn-emu-algo2-verschattet"}
