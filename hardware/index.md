---
title: Hardware implementation
layout: post
nav_order: 5
has_children: true
---

# Hardware implementation

This chapter is about putting the theoretical considerations and
concepts from the last chapter
[\[kap:concept\]](#kap:concept){reference-type="ref"
reference="kap:concept"} into practice. This chapter describes how the
hardware for the solar module optimiser is built and which components
are used for it. The individual steps and challenges in the
implementation are described in detail. The goal is to create a
functioning system that is able to determine and maintain the
[mpp]{acronym-label="mpp" acronym-form="singular+short"} of the solar
module. For this purpose, various components such as microcontrollers,
voltage converters, [mosfet]{acronym-label="mosfet"
acronym-form="singular+short"}s and measuring instruments are used,
which are considered in more detail in this chapter. A detailed
description of the implementation will give an insight into the
technical implementation of the solar module optimiser.
