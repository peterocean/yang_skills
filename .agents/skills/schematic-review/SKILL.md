---
name: schematic-review
description: Conduct interactive electronic schematic reviews and resource-allocation comparisons. Use for new-project MCU resource checks or existing-project schematic/code change reviews; not PCB layout-only review.
---

# Schematic Review

Lead an evidence-based conversation. Treat the schematic, code, BOM, datasheet, and user answers as the only sources of truth. Do not invent values, pin functions, nets, operating conditions, package variants, or compliance claims. Ask for only the missing artifact that blocks the next step, and do not modify files unless separately asked.

## Route the review

- **New project:** obtain the new schematic file/directory and exact MCU/SoC ordering code. Obtain a part-number-specific datasheet when the schematic does not establish the exact package and variant. Do not infer pinout or capabilities from the MCU family name alone.
- **Existing-project change:** obtain absolute directories for the original schematic and matching code. Read both read-only, generate the original allocation table, then request the new schematic file/directory.

## New-project MCU resource check

Extract all MCU-connected GPIO/I-O, interrupt, timer/channel, serial interface, ADC/DAC/PWM, identifiable DMA request, clock, reset, boot/configuration strap, power, and debug/programming signals. Generate a new-project resource allocation table with resource type, MCU pin/peripheral/instance, schematic net and reference, intended function, MCU capability evidence, status, and note.

Compare assignments against the exact MCU documentation: package pinout, alternate functions, peripheral count and channels, shared-resource constraints, boot/debug reservations, and electrical limits. Mark a row **auto-confirmed** only when the assignment is directly supported and conflict-free. Put every uncertain or suspect item in a separate customer-confirmation table with `**[REVIEW REQUIRED]**`, issue, resource, schematic location, MCU evidence, impact, recommendation, and `Customer confirmation: Pending`.

Flag unsupported alternate functions, duplicate pin/channel claims, unavailable instances, package-pin mismatch, boot/debug conflicts, missing power/reset/clock connections, voltage-domain uncertainty, and absent evidence. Ask the customer to confirm or clarify only these highlighted rows.

## Existing-project change check

Search the codebase for MCU/SoC configuration, pin definitions, startup code, interrupt handlers, peripheral initialization, and resource claims. Configuration may be in generated files, headers, device-tree files, board-support files, or build settings.

Cross-check original schematic and code for GPIO direction/alternate function, interrupts, timers/channels, buses, ADC/DAC/PWM, DMA, clocks, resets, chip-selects, enables, and external interrupts. Generate an original allocation table with resource type, MCU pin/peripheral/instance, schematic net/reference, code file/symbol, configured role, status, and verification note. Use **auto-confirmed** when schematic and code evidence agree; otherwise use **schematic-only**, **code-only**, **conflict**, or **needs evidence**. Do not request a second confirmation for auto-confirmed rows.

Read the new schematic and produce a separate new-schematic resource table. Keep the original table immutable. Match rows by MCU pin or peripheral instance/channel, then net and role; reference designators are supporting evidence only. Compare for added, removed, remapped, reconfigured, renamed, or uncertain assignments.

Immediately provide a difference table that contains only changes. Prefix every changed row with `**[REVIEW REQUIRED]**` and include original allocation, new allocation, both schematic references, expected software/system impact, recommendation, and `Customer confirmation: Pending`. Call out a changed pin, interrupt source, timer/channel, peripheral instance, voltage domain, or safety-critical default state even where the net name did not change. Do not silently update the baseline or accept a change before customer confirmation.

## Review boundaries

When a diagram is unreadable, ask for a higher-resolution export, relevant crop, or copied pin/net/value data. A schematic review cannot establish PCB layout quality, thermal performance, EMC, safety certification, or production behavior without corresponding evidence.
