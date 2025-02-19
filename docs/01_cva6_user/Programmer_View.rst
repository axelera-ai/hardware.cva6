﻿..
   Copyright (c) 2023 OpenHW Group
   Copyright (c) 2023 Thales DIS design services SAS

   SPDX-License-Identifier: Apache-2.0 WITH SHL-2.1

.. Level 1
   =======

   Level 2
   -------

   Level 3
   ~~~~~~~

   Level 4
   ^^^^^^^

.. _cva6_programmers_view:

Programmer’s View
=================
RISC-V specifications allow many variations. This chapter provides more details about RISC-V variants available for the programmer.
A global view of the CVA6 family is provided, as well as details for each verified configuration.

RISC-V Extensions
-----------------

CVA6 family
~~~~~~~~~~~

The following extensions are available for the CVA6 family.
Some of them are optional and are enabled through parameters in the SystemVerilog design.

**RV32** denotes RISC-V 32-bit extensions. **RV64** denotes RISC-V 64-bit extensions.

.. csv-table::
   :widths: auto
   :align: left
   :header: "Extension", "Optional", "RV32 (in CV32A6)", "RV64 (in CV64A6)", "Note"

   "I- Base Integer Instruction Set",                                   "No",  "✔", "✔", "Note 1"
   "A - Atomic Instructions",                                           "Yes", "✔", "✔", "Note 1"
   "Zb* - Bit-Manipulation",                                            "Yes", "✔", "✔", "Note 1"
   "C - Compressed Instructions ",                                      "Yes", "✔", "✔", "Note 1"
   "Zcb - Code Size Reduction",                                         "Yes", "✔", "✔", "Note 1"
   "D - Double precision floating-point",                               "Yes", "",  "✔", "Note 1"
   "F - Single precision floating-point",                               "Yes", "✔", "✔", "Note 1"
   "M - Integer Multiply/Divide",                                       "No",  "✔", "✔", "Note 1"
   "Zicount - Performance Counters",                                    "Yes", "✔", "✔", "Note 2"
   "Zicsr - Control and Status Register Instructions",                  "No",  "✔", "✔", "Note 2"
   "Zifencei - Instruction-Fetch Fence",                                "No",  "✔", "✔", "Note 2"
   "Zicond - Integer Conditional Operations(Ratification pending)",     "Yes", "✔", "✔", "Note 2"

Notes:

* Note 1: These extensions have a slightly  different definition between RV32 and RV64. They are therefore denoted with digits (e.g. RV\ **32**\ M).
* Note 2: These extensions do not differ between RV32 and RV64. They are therefore denoted without digits below (e.g. RVZifencei).

*The following tables detail the availability of extensions for the various CVA6 configurations:*

CV32A60AX extensions
~~~~~~~~~~~~~~~~~~~

These extensions are available in CV32A60AX:

.. csv-table::
   :widths: auto
   :align: left
   :header: "Extension", "Available in CV32A60AX"

   "RV32I - Base Integer Instruction Set",                                  "✔"
   "RV32A - Atomic Instructions",                                           "✔"
   "RV32Zb* - Bit-Manipulation (Zba, Zbb, Zbc, Zbs)",                       "✔"
   "RV32C - Compressed Instructions ",                                      "✔"
   "RV32Zcb - Code Size Reduction",                                         "✔"
   "RV32D - Double precision floating-point",                               ""
   "RV32F - Single precision floating-point",                               ""
   "RV32M - Integer Multiply/Divide",                                       "✔"
   "RVZicount - Performance Counters",                                      "✔"
   "RVZicsr - Control and Status Register Instructions",                    "✔"
   "RVZifencei - Instruction-Fetch Fence",                                  "✔"
   "RVZicond - Integer Conditional Operations(Ratification pending)",       "✔"

CV32A60X extensions
~~~~~~~~~~~~~~~~~~~

These extensions are available in CV32A60X:

.. csv-table::
   :widths: auto
   :align: left
   :header: "Extension", "Available in CV32A60AX"

   "RV32I - Base Integer Instruction Set",                                  "✔"
   "RV32A - Atomic Instructions",                                           ""
   "RV32Zb* - Bit-Manipulation (Zba, Zbb, Zbc, Zbs)",                       "✔"
   "RV32C - Compressed Instructions ",                                      "✔"
   "RV32Zcb - Code Size Reduction",                                         "✔"
   "RV32D - Double precision floating-point",                               ""
   "RV32F - Single precision floating-point",                               ""
   "RV32M - Integer Multiply/Divide",                                       "✔"
   "RVZicount - Performance Counters",                                      ""
   "RVZicsr - Control and Status Register Instructions",                    "✔"
   "RVZifencei - Instruction-Fetch Fence",                                  "✔"
   "RVZicond - Integer Conditional Operations(Ratification pending)",       ""


RISC-V Privileges
-----------------

CVA6 family
~~~~~~~~~~~

CVA6 supports these privilege modes:

.. csv-table::
   :widths: auto
   :align: left
   :header: "Mode"

   "M - Machine"
   "S - Supervior"
   "U - User"

Note: The addition of the H Extension is in the process. After that, HS, VS, and VU modes will also be available.

*The following tables detail the availability of privileges modes for the various CVA6 configurations:*

CV32A60AX privilege modes
~~~~~~~~~~~~~~~~~~~~~~~~

These privilege modes are available in CV32A60AX:

.. csv-table::
   :widths: auto
   :align: left
   :header: "Privileges", "Available in CV32A60AX"

   "M - Machine",                   "✔"
   "S - Supervior",                 "✔"
   "U - User",                      "✔"

CV32A60X privilege modes
~~~~~~~~~~~~~~~~~~~~~~~~

These privilege modes are available in CV32A60X:

.. csv-table::
   :widths: auto
   :align: left
   :header: "Privileges", "Available in CV32A60X"

   "M - Machine",                   "✔"
   "S - Supervior",                 ""
   "U - User",                      ""


RISC-V Virtual Memory
---------------------

CVA6 family
~~~~~~~~~~~

CV32A6 supports the RISC-V **Sv32** virtual memory when the ``MMUEn`` parameter is set to 1 (and ``Xlen`` is set to 32).

CV64A6 supports the RISC-V **Sv39** virtual memory when the ``MMUEn`` parameter is set to 1 (and ``Xlen`` is set to 64).

By default, CV32A6 and CV64A6 are in RISC-V **Bare** mode. **Sv32** or **Sv39** are enabled by writing 1 to ``satp[0]`` register bit.

When the ``MMUEn`` parameter is set to 0, CV32A6 and CV64A6 are always in RISC-V **Bare** mode; ``satp[0]`` remains at 0 and writes to this register are ignored.

Notes for the integrator:

* The virtual memory is implemented by a memory management unit (MMU) that accelerates the translation from virtual memory addresses (as handled by the core) to physical memory addresses. The MMU integrates translation lookaside buffers (TLB) and a hardware page table walker (PTW). The number of instruction and data TLB entries are configured with ``InstrTlbEntries`` and ``DataTlbEntries``.

* The MMU will integrate a microarchitectural optimization featuring two levels of TLB: level 1 TBL (sized by ``InstrTlbEntries`` and ``DataTlbEntries``) and a shared level 2 TLB. The optimization has no consequences on the programmer's view.

* The addition of the hypervisor support will come with **Sv39x4** virtual memory that is not yet documented here.

*These are the addressing modes supported by the various CVA6 configurations:*

CV32A60AX virtual memory
~~~~~~~~~~~~~~~~~~~~~~~

CV32A60AX integrates an MMU and supports both the **Bare** and **Sv32** addressing modes.


CV32A60X virtual memory
~~~~~~~~~~~~~~~~~~~~~~~~

CV32A60X integrates no MMU and only supports the **Bare** addressing mode.


Memory Alignment
----------------
CVA6 **does not support non-aligned** memory accesses.

*This is applicable to all configurations.*

Harts
-----
CVA6 features a **single hart**, i.e. a single hardware thread.

Therefore the words *hart* and *core* have the same meaning in this guide.

*This is applicable to all configurations.*

