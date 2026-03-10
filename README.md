# Abstract

In safety-critical domains such as the automotive and aircraft industry, critical software
that can endanger human life must be strictly isolated from non-critical software with
limited impact. A microkernel supports this separation; this thesis focuses on the L4Re
microkernel, and, since microkernels are generally less widely used, there are no existing
device drivers for some hardware, including modern Network Interface Cards (NICs).
This also applies to the Intel i225 NIC integrated into the Ecrin aviation computer, which
cannot be used without a suitable device driver. The goal of this thesis is to implement an
i225 NIC device driver for L4Re and to assess how additional NIC device drivers can be
ported to the same framework.
To reduce effort, the initial plan was to port the Linux igc device driver. After comparing
multiple candidate frameworks, ixl was identified as the most suitable choice, but it requires
rewriting the device driver instead of directly porting the existing code, using the Linux igc
device driver only as a conceptual basis. Ixl already supports three Intel NICs, and the
underlying hardware—especially between the igb and igc device driver families—is largely
compatible, so the existing ixl igb device driver was adapted, mainly by changing register
and bit definitions, to implement the ixl igc device driver.
The ixl igc device driver implemented in this thesis currently uses only basic features and
offers substantial potential for advancement, both by enabling further performance-oriented
mechanisms of the i225 and by adding features such as VLAN and TSN that are particularly
interesting for the Real-Time domain. The thesis also identifies the current limitations of
ixl, namely that it only supports PCI NICs and a single Rx/Tx queue, and shows that,
within these constraints, additional device drivers can be integrated: porting further Intel
drivers is straightforward due to shared hardware design, while adapting non-Intel drivers
remains feasible by mapping common NIC functionality onto the ixl interfaces using existing
drivers and datasheets as references.
