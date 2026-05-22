# ATmega32U4 Arduino-Compatible USB-C Bluetooth Module

This KiCad project is a learning-focused starter design for an ATmega32U4-based Arduino-compatible module. It includes a schematic-first design flow, a PCB layout with placed footprints, a custom module footprint example, and notes for using KiCad MCP automation.

## What This Project Contains

- ATmega32U4 microcontroller schematic connectivity
- USB Type-C female connector wiring
- HC-05 / HM-10 compatible Bluetooth header
- Arduino-style 2.54 mm headers
- Reset circuit
- 16 MHz crystal circuit
- USB-C CC1/CC2 5.1k pull-down support
- Power and decoupling capacitors
- PCB footprints placed in PCB Editor
- Rectangular board outline on `Edge.Cuts`
- Custom example footprint library in `TestDemo.pretty`

## Included KiCad Projects

This community repo now contains multiple KiCad learning projects:

- `TestDemo.kicad_pro` - ATmega32U4 Arduino-compatible USB-C Bluetooth module
- `Card_Reader_Adapter/Card_Reader_Adapter.kicad_pro` - smart-card reader adapter with ISO 7816 contacts and RJ45 connector

## Project Files

```text
TestDemo.kicad_pro     KiCad project file
TestDemo.kicad_sch     Main schematic
TestDemo.kicad_pcb     PCB layout
fp-lib-table           Project footprint library table
TestDemo.pretty/       Project-local footprint library
KICAD_STARTUP_SCENARIO.md  Learning notes and startup scenario
```

Generated reports:

```text
TestDemo.erc.json          ERC report for schematic
TestDemo.validate-drc.json DRC report for PCB
```

Backup files are also present because KiCad MCP write operations were run with backups enabled.

## Recommended Learning Order

Start with **Schematic Editor**, not Footprint Editor.

1. Open the KiCad project.
2. Learn symbols, wires, labels, and nets in Schematic Editor.
3. Assign footprints to schematic symbols.
4. Update PCB from schematic.
5. Place and route footprints in PCB Editor.
6. Use Footprint Editor only when creating or editing one reusable physical footprint.
7. Run ERC and DRC before manufacturing output.

Important distinction:

```text
Symbol          Electrical part in schematic
Footprint       Physical pad pattern for one part
Net             Named electrical connection
PCB layout      Physical board with placed footprints and routed tracks
```

## Opening The Project In KiCad

1. Install KiCad 9.x or newer.
2. Open KiCad.
3. Open this project file:

```text
TestDemo.kicad_pro
```

From the Project Manager:

- Open **Schematic Editor** to see the ATmega32U4 circuit.
- Open **PCB Editor** to see the placed PCB footprints and board outline.
- Open **Footprint Editor** only to inspect project-local custom footprints.

## Viewing The Schematic

Open:

```text
TestDemo.kicad_sch
```

The schematic includes:

- `U1`: ATmega32U4-A
- `J1`: USB-C receptacle
- `J2`: Arduino-compatible digital header
- `J3`: power, analog, and USB breakout header
- `J4`: HC-05 / HM-10 Bluetooth header
- `R1`, `R2`: 5.1k USB-C CC pull-down resistors
- `R3`: reset pull-up
- `SW1`: reset switch
- `Y1`: 16 MHz crystal
- `C1` to `C8`: decoupling, UCAP, AREF, 5V bulk, and crystal load capacitors

Key net labels:

```text
5V
VCC
GND
RESET
USB_DP
USB_DM
CC1
CC2
TX0
RX1
D2_SDA
D3_SCL
D4 to D10
A0 to A5
BT_STATE
BT_EN_KEY
```

## Viewing The PCB

Open:

```text
TestDemo.kicad_pcb
```

The PCB contains placed footprints for:

- ATmega32U4 TQFP-44
- USB-C connector
- Digital, analog, power, USB, and Bluetooth headers
- Resistors and capacitors
- Crystal
- Reset switch
- Four M2 mounting holes
- Board outline on `Edge.Cuts`

If footprints are visible in PCB Editor but not in Footprint Editor, that is normal. PCB Editor shows the board. Footprint Editor shows only one reusable footprint from a library.

## Viewing The Custom Footprint

This project also includes a project-local footprint library:

```text
TestDemo.pretty/
```

It is registered by:

```text
fp-lib-table
```

The custom footprint file is:

```text
TestDemo.pretty/ATmega32U4_Arduino_USB-C_BT_Module.kicad_mod
```

To view it in Footprint Editor:

1. Open `TestDemo.kicad_pro` in KiCad.
2. Open **Footprint Editor**.
3. Select the `TestDemo` library from the library tree.
4. Open `ATmega32U4_Arduino_USB-C_BT_Module`.

If the Footprint Editor appears empty, make sure the project was opened from `TestDemo.kicad_pro`, not by opening a single `.kicad_mod` file directly.

## USB-C Connectivity

The schematic uses these USB-C connections:

```text
VBUS   -> 5V
GND    -> GND
Shield -> GND
D+     -> USB_DP
D-     -> USB_DM
CC1    -> 5.1k pull-down to GND
CC2    -> 5.1k pull-down to GND
SBU1   -> no connect
SBU2   -> no connect
```

## Bluetooth Header

The Bluetooth header is intended for HC-05 / HM-10 style modules:

```text
Pin 1  VCC
Pin 2  GND
Pin 3  RX1
Pin 4  TX0
Pin 5  BT_STATE
Pin 6  BT_EN_KEY
```

Check the exact TX/RX direction for your module before manufacturing. Many Bluetooth modules label pins from the module perspective, so MCU `TX0` normally connects to module `RX`, and MCU `RX1` normally connects to module `TX`.

## KiCad Checks

Run ERC from KiCad:

```text
Schematic Editor > Inspect > Electrical Rules Checker
```

Run DRC from KiCad:

```text
PCB Editor > Inspect > Design Rules Checker
```

Command-line examples on macOS with KiCad installed in `/Applications`:

```sh
/Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli sch erc \
  --output TestDemo.erc.json \
  --format json \
  TestDemo.kicad_sch

/Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli pcb drc \
  --output TestDemo.validate-drc.json \
  --format json \
  TestDemo.kicad_pcb
```

## Update PCB From Schematic

After editing the schematic, update the PCB from KiCad GUI:

```text
PCB Editor > Tools > Update PCB from Schematic
```

This step synchronizes footprints, nets, and ratsnest connections from the schematic into the PCB.

Note: the installed `kicad-cli` can run ERC, DRC, exports, and reports, but it does not expose full GUI-equivalent **Update PCB from Schematic** for this setup. Use the KiCad GUI for that step.

## Install KiCad MCP With npm

KiCad MCP lets AI tools inspect and automate KiCad projects. The npm package provides a Node.js launcher for the KiCad MCP server.

Requirements:

- Node.js and npm
- Python 3.10 or newer
- KiCad installed
- `kicad-cli` available or passed with `--kicad-cli`

Check npm package information:

```sh
npm view kicad-mcp version description bin
```

Run KiCad MCP directly with `npx`:

```sh
npx -y kicad-mcp@latest
```

By default this runs MCP over stdio, which is the normal mode for MCP clients.

Run setup explicitly:

```sh
npx -y kicad-mcp@latest --setup
```

Run local HTTP mode:

```sh
npx -y kicad-mcp@latest --http --host 127.0.0.1 --port 8765
```

The HTTP MCP endpoint is:

```text
http://127.0.0.1:8765/mcp
```

Keep the host set to `127.0.0.1` unless you add proper authentication.

Install globally with npm:

```sh
npm install -g kicad-mcp
```

Then run:

```sh
kicad-mcp --help
kicad-mcp --stdio
kicad-mcp --http --host 127.0.0.1 --port 8765
```

Useful options:

```sh
kicad-mcp --setup
kicad-mcp --install-codex-skill github
kicad-mcp --python /path/to/python3
kicad-mcp --venv /path/to/venv
kicad-mcp --kicad-cli /Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli
```

## MCP Client Configuration

Example MCP client configuration using `npx`:

```json
{
  "mcpServers": {
    "kicad": {
      "command": "npx",
      "args": ["-y", "kicad-mcp@latest"]
    }
  }
}
```

Example HTTP startup command:

```sh
npx -y kicad-mcp@latest --http --host 127.0.0.1 --port 8765 \
  --kicad-cli /Applications/KiCad/KiCad.app/Contents/MacOS/kicad-cli
```

## Install The Codex Skill

The npm package can install the Codex skill from GitHub:

```sh
npx -y kicad-mcp@latest --install-codex-skill github
```

This installs the skill to:

```text
~/.codex/skills/kicad-mcp
```

After restarting Codex, use:

```text
$kicad-mcp
```

Example prompt:

```text
Use $kicad-mcp to inspect this KiCad project, run ERC/DRC, and report the current schematic and board status.
```

## KiCad MCP Safe Workflow

Recommended automation order:

1. Find project files: `.kicad_pro`, `.kicad_sch`, `.kicad_pcb`.
2. Run read-only checks first: project summary, schematic statistics, board statistics.
3. Before write operations, run `dry_run=true` when supported.
4. Keep `create_backup=true` for edits.
5. After schematic edits, run ERC.
6. After PCB edits, run DRC.
7. Report changed files, generated reports, and backup paths.

Useful KiCad MCP task examples:

```text
kicad_find_project_files
kicad_project_summary
kicad_schematic_statistics
kicad_list_schematic_symbols
kicad_list_schematic_nets
kicad_run_erc
kicad_board_statistics
kicad_list_board_footprints
kicad_validate_board
kicad_run_drc
kicad_export_bom
kicad_export_gerbers
kicad_export_drill_files
```

## KiCad GUI Bridge

Some KiCad MCP GUI actions require the PCB Editor bridge.

To use it:

1. Open KiCad PCB Editor.
2. Open the target board.
3. Run:

```text
Tools > External Plugins > KiCad AI MCP
```

The GUI bridge normally listens locally at:

```text
http://127.0.0.1:8766/status
```

If the bridge is not running, MCP can still edit saved KiCad files, but live GUI actions such as selecting, zooming, and moving visible PCB items will not work.

## Suggested Beginner Workflow For This Project

1. Open `TestDemo.kicad_pro`.
2. Open Schematic Editor and study the net labels.
3. Run ERC.
4. Open PCB Editor.
5. Run **Update PCB from Schematic**.
6. Inspect the placed footprints.
7. Route `USB_DP` and `USB_DM` carefully as a short pair.
8. Route power and ground.
9. Add a ground zone.
10. Run DRC.
11. Generate fabrication outputs only after DRC is clean.

## Manufacturing Outputs

When the board is ready, generate files from PCB Editor:

```text
File > Fabrication Outputs > Gerbers
File > Fabrication Outputs > Drill Files
File > Fabrication Outputs > Component Placement
```

You can also use KiCad MCP or `kicad-cli` for exports after the board is finalized.

## Notes

- This is a starter learning design, not a certified Arduino product.
- Review the ATmega32U4 datasheet before manufacturing.
- Confirm USB-C footprint compatibility with the exact connector part number.
- Confirm Bluetooth module pin direction and voltage level requirements.
- Route USB data lines carefully and keep them short.
- Add or tune PCB design rules before ordering boards.

## Credits And Contact

Created by Ieng Pho.

- GitHub: [iengphogit](https://github.com/iengphogit)
- Facebook: [ieng.pho](https://www.facebook.com/ieng.pho/)
- LinkedIn: [Ieng Pho](https://www.linkedin.com/in/ieng-pho-7a4328189/)
- Email: [iengpho@gmail.com](mailto:iengpho@gmail.com)
