# KiCad Startup Scenario

## Learning Order

Start with **Schematic Editor**.

1. Project Manager
   - Learn the project files: `.kicad_pro`, `.kicad_sch`, `.kicad_pcb`, `.pretty`, `fp-lib-table`.
2. Schematic Editor
   - Place symbols, wire pins, add net labels, add power symbols, run ERC.
3. Symbol to Footprint Mapping
   - A symbol is the electrical part.
   - A footprint is the physical PCB pad pattern.
   - A net is the named electrical connection between pins.
4. PCB Editor
   - Import schematic changes, place footprints, draw board edges, route tracks, add zones, run DRC.
5. Footprint Editor
   - Use this after the basics, mainly for custom parts or exact mechanical pad layouts.
6. Manufacturing Outputs
   - Export Gerbers, drill files, BOM, and position files.

## Current Project

Project path:

Open the repository root containing `TestDemo.kicad_pro`.

Detected KiCad files:

- `TestDemo.kicad_pro`
- `TestDemo.kicad_sch`
- `TestDemo.kicad_pcb`
- `fp-lib-table`

Current schematic state:

- Symbols: `0`
- Wires: `0`
- Labels: `0`
- Sheets: `0`

This means the right next step is to start the design in **Schematic Editor**, not Footprint Editor.

## KiCad MCP Availability

The local KiCad MCP server is available at:

`http://127.0.0.1:8765/mcp`

It is reachable and supports schematic design automation.

Useful schematic MCP tools available:

- `kicad_schematic_statistics`
- `kicad_list_schematic_symbols`
- `kicad_list_schematic_nets`
- `kicad_search_symbols`
- `kicad_place_symbol_from_template`
- `kicad_add_schematic_wire`
- `kicad_add_schematic_label`
- `kicad_add_schematic_global_label`
- `kicad_add_schematic_junction`
- `kicad_add_schematic_no_connect`
- `kicad_set_symbol_footprint`
- `kicad_annotate_schematic`
- `kicad_run_erc`
- `kicad_update_pcb_from_schematic`

Important limitation:

The MCP GUI bridge is for PCB Editor actions. For Schematic Editor, MCP can edit and validate the saved schematic file, but it does not currently drive the live Schematic Editor GUI directly. After MCP edits the schematic, reload or reopen the schematic in KiCad if the GUI does not update automatically.

## ATmega32U4 Module Startup Plan

Use this order for the Arduino-compatible ATmega32U4 module:

1. Create the schematic first.
2. Add the ATmega32U4 symbol.
3. Add USB Type-C connector symbol.
4. Add CC1 and CC2 5.1k pull-down resistors to GND.
5. Add USB D+ and D- series resistors if needed.
6. Add reset circuit.
7. Add crystal or resonator circuit if using an external clock.
8. Add decoupling capacitors for VCC, AVCC, UVCC, UCAP, and AREF.
9. Add the Bluetooth header: `VCC`, `GND`, `TX`, `RX`, `STATE`, `EN/KEY`.
10. Add Arduino-style headers: `RESET`, `TX0`, `RX1`, `SDA`, `SCL`, `D2`-`D10`, `A0`-`A5`, `USB_DP`, `USB_DM`.
11. Add net labels clearly before routing the PCB.
12. Annotate the schematic.
13. Assign footprints.
14. Run ERC.
15. Update PCB from schematic.
16. Place parts and route in PCB Editor.
17. Run DRC.

## Recommended First Schematic Nets

Use these net names consistently:

- `5V`
- `VCC`
- `GND`
- `RESET`
- `USB_DP`
- `USB_DM`
- `CC1`
- `CC2`
- `TX0`
- `RX1`
- `SDA`
- `SCL`
- `D2` through `D10`
- `A0` through `A5`
- `BT_STATE`
- `BT_EN_KEY`

## Practical Rule

If you are designing the whole board, work in **Schematic Editor** and **PCB Editor**.

Use **Footprint Editor** only when making or fixing a reusable physical part shape.
