# Card Reader Adapter KiCad Project

KiCad project for a smart-card reader adapter inspired by `nkinder/smart-card-removinator`.

The PCB uses ISO 7816 contact pads on the card-reader side and an RJ45 connector on the cable side. The routed core nets are:

- RJ45 pin 1 -> AUX1
- RJ45 pin 2 -> I/O
- RJ45 pin 3 -> CLK
- RJ45 pin 4 -> AUX2
- RJ45 pin 5 -> RST
- RJ45 pin 6 -> VPP
- RJ45 pin 7 -> GND
- RJ45 pin 8 -> VCC

Important fabrication note: order this board as **0.031 inch / 0.8 mm PCB thickness** so it can fit into a smart-card reader slot.

Files:

- `Card_Reader_Adapter.kicad_pro` - KiCad project
- `Card_Reader_Adapter.kicad_sch` - visible schematic with U1 smart-card contacts and J1 RJ45 mapping
- `Card_Reader_Adapter.kicad_sym` / `sym-lib-table` - project-local schematic symbols
- `Card_Reader_Adapter.kicad_pcb` - routed PCB layout
- `Card_Reader_Adapter.pretty/` - project-local footprints
- `reference/` - original SVG schematic and Gerber files from the public reference repository

Validation run with KiCad 9.0.4:

- ERC: 0 violations
- DRC: 0 violations, 0 unconnected items

R1 is included as an optional RJ45 LED resistor footprint. The smart-card adapter core is the eight ISO 7816 signal routes listed above.
