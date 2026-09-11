# meshnode

A screenless Meshtastic node built around a Seeed Studio XIAO nRF52840 and a Wio-SX1262 LoRa module.

## Hardware

- **U1** — Seeed Studio XIAO nRF52840 (MCU + BLE, handles charging and USB)
- **U2** — Wio-SX1262 LoRa module
- **J1** — 2-pin JST 1.25mm connector for a single-cell LiPo battery
- **SW2** — slide switch, gates power to the LoRa radio only (see below)
- **J5 / J6** — solder pads for a hand-wired bodge to the XIAO's battery pads (see below)

## Power design

The XIAO nRF52840's charge circuit connects to the battery through two solder pads
(`BAT+` / `BAT-`) on the underside of the module. Seeed's own KiCad footprint for this
part doesn't expose those pads as routable copper, so they aren't reachable through
normal PCB routing once the module is soldered down.

To get battery power onto the board:

1. Drill a small hole through the carrier PCB under the XIAO, positioned to reach the
   module's `BAT+` pad from below.
2. Solder a short wire from that pad down through the hole to the `J5` pad on the
   carrier board (net `POS IN`, wired straight to the battery connector's positive pin).
3. Do the same for `BAT-` to `J6` (net `NEG IN` / ground).

Strain-relieve both joints (hot glue/epoxy) — these are small SMD lands with no
mechanical reinforcement and can lift if the wire flexes.

**Battery+/− go straight to the XIAO's charge pads with no switch in that path**, so
charging over USB-C always works regardless of switch position. `SW2` instead sits
between the XIAO's `3V3_OUT` pin and the Wio-SX1262's power input (`3V3` → `SW2` →
`R3V3`), so flipping it off only cuts power to the radio — the dominant current draw —
while charging is unaffected.

## Repo contents

- `meshnode.kicad_pro` / `.kicad_sch` / `.kicad_pcb` — KiCad 8 project
- `meshnode.step` / `.wrl` — 3D board exports
- `Gerber/` — fabrication outputs (Gerbers + drill files)

## Building

Open `meshnode.kicad_pro` in KiCad. Run ERC and DRC before sending to fab. Remember the
manual bodge wire described above — it's physical, not part of the netlist, and has to
be done by hand on every assembled board.
