---
title: Filter
layout: post
nav_order: 3
parent: Software implementation
---

# Filter

The *ADC* may perform inaccurate measurements due to noise in the
system, which may distort the real value. Applying filters can reduce
the noise and improve the accuracy of the measurements. The *FilterAvg*
class from Listing [\[listing:5\]](#listing:5){reference-type="ref"
reference="listing:5"} provides a simple average filter for
[adc]{acronym-label="adc" acronym-form="singular+short"} samples. It
requires the instance of the *ADC* class and the number of samples to
average. In the *calc()* method, the sum of the samples in a buffer
*buf* is added up and divided by the number of samples at the end. This
calculates the average value and returns it as a filtered value.Ṫhis
class is needed to minimize the noise of the raw data and provide a more
accurate measurement.

::: listing
``` {.python frame="lines" linenos="" xleftmargin="2em"}
class FilterAvg():
    '''Average filter for adc samples'''
    def __init__(self, adc: ADC, samples: int):
        self.buf = 0.
        self.samples = samples
        self.adc = adc

    def calc(self):
        for sample in range(self.samples):
            self.buf += self.adc.read_u16()
        filtered = self.buf/self.samples
        self.buf = 0.
        return(filtered)
```
:::
