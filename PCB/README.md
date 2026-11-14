# meshnode

A screenless Meshtastic node built around a Seeed Studio XIAO nRF52840 and a Wio-SX1262 LoRa module.

## Hardware

- **U1** — Seeed Studio XIAO nRF52840 (MCU + BLE, handles charging and USB)
- **U2** — Wio-SX1262 LoRa module
- **J1** — 2-pin JST 1.25mm connector for a single-cell LiPo battery
- **SW2** — slide switch, gates power to the LoRa radio only (see below)
- **J5 / J6** — solder pads for a hand-wired bodge to the XIAO's battery pads (see below)

## Repo contents

- `meshnode.kicad_pro` / `.kicad_sch` / `.kicad_pcb` — KiCad 8 project
- `meshnode.step` / `.wrl` — 3D board exports
- `Gerber/` — fabrication outputs (Gerbers + drill files)

## Building

Open `meshnode.kicad_pro` in KiCad. Run ERC and DRC before sending to fab