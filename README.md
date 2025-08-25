# HeRo-Derived PCB Redesign (EasyEDA + JLCPCB)

**Status:** WIP  
**Upstream Reference:** Based on [`verlab/hero_common`](https://github.com/verlab/hero_common) and its public docs. See **Attribution** below.

---

## Overview

This repository hosts a **hardware redesign** of the HeRo mobile robot electronics. The redesign was performed in **EasyEDA**, prioritizing components stocked for **JLCPCB** assembly (LCSC part numbers), and **splits the original board into two PCBs**:

- **MCU Board** — processing, IO headers, and comms  
- **Power Board** — battery input, charging/regulation, protection, and power distribution

The goals are:
- Add room for **new functions** (see examples below)
- Improve manufacturability with JLCPCB’s SMT assembly flow
- Keep compatibility with the upstream HeRo software/firmware where practical

## Hardware notes

### MCU Board
- Pin headers/ports kept compatible with the upstream ecosystem where possible.
- Provide SWD/UART (or relevant) access for flashing and bring-up.
- Include test points for rails and key signals.

### Power Board
- Battery input (Li-ion/LiPo), charge path, protections, and regulated rails (e.g., 5 V, 3.3 V).
- Consider shunt/INA-type current sense and a fuel-gauge footprint for runtime telemetry.
- Board-to-board connector(s) for robust interconnect with the MCU board.

### Solder mask & LEDs
- Upstream shows **white solder mask** for better LED visibility. You can keep or change it depending on your needs.

---

## CAD → Fabrication (EasyEDA → JLCPCB)

1. **Per board export**
   - **Gerbers** (RS-274X), **BOM (CSV)** with LCSC numbers, **CPL (CSV)** with refdes, package, X/Y/θ, and side.
2. **Order on JLCPCB**
   - Upload Gerbers; attach **BOM** and **CPL** to enable SMT assembly.
3. **Typical fab constraints (adapt to your DRC)**
   - Finished copper: **≥ 1 oz**  
   - Minimum hole size: **0.3 mm**  
   - Minimum trace/spacing: **6/6 mil**
4. **Assembly tips**
   - Prefer single-sided SMT where possible (lower cost).
   - Add three panel fiducials and clear rotation markers.
   - Mark optional parts as **DNP** and document alternatives.
   - Keep tall parts away from panel rails/score lines.

## Acknowledgments

Thanks to the **VeRLab** team for releasing HeRo as an open platform for swarm robotics research and education.