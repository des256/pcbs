# AMOS Board Layout Guide

## Board summary

4-layer, 1.6 mm, JLCPCB JLC04161H-7628 stackup.  
Function: 19 V power input → servo power (12 V + 5 V) + USB power (5 V) + 3V3/1V1 for logic;
USB 3.1 Gen 2 hub (TUSB8041); 4-channel RS-485 servo bus (CH344Q + SP3485).

---

## Layer roles

| Layer | Role |
|-------|------|
| L1 F.Cu | Components + signals + high-current power traces |
| L2 In1.Cu | **Solid GND plane** — unbroken, reference for all signals and switcher returns |
| L3 In2.Cu | Power distribution pours (5V\_USB, 3V3) + secondary signal routing |
| L4 B.Cu | Signal routing + secondary components |

**Never split L2.** No moats, no slot cuts. Every switching and digital circuit shares one return reference.

---

## Board regions (left → right)

```
┌─────────────────┬──────────────────┬─────────────────────┐
│   HIGH POWER    │  5V_USB BUCK     │     USB ISLAND      │
│  (power edge)   │  (bridge)        │  (data edge)        │
│                 │                  │                     │
│ XT30 input      │  TPS54560        │ TUSB8041  USB-C     │
│ LM74700         │                  │ HD3SS3220 USB-A ×3  │
│ LM5145 12V buck │                  │ TLV62569 (3V3+1V1)  │
│ LM5145 5V buck  │                  │                     │
├─────────────────┴──────────────────┴─────────────────────┤
│  Servo bus (opposite edge to power)                      │
│  CH344Q  │  SP3485+SN74LVC2G241 ×4  │  B3B/B4B-EH ×4   │
└──────────────────────────────────────────────────────────┘
```

---

## Placement order

### 1. Connectors — fix these first
All connectors are mechanical anchors. Place and lock before anything else.

| Connector | Edge | Notes |
|-----------|------|-------|
| XT30 power input | Power edge | Close together; short trace to fuse |
| Jetson 19 V passthrough (CN202) | Power edge | Adjacent to XT30 |
| USB-C upstream | Data edge | HD3SS3220 immediately behind it |
| USB-A downstream ×3 | Data edge | Group together |
| Servo bus JST (B3B/B4B-EH ×4) | Servo edge | Spread evenly |

### 2. High-power cluster — near the power-edge connectors
- LM74700 + 470 µF electrolytic + TVS (SMBJ24A) + fuse — immediately behind XT30
- LM5145 **12 V servo buck** (+ CSD18532Q5B MOSFET + inductor + caps) — tight next to main power
- LM5145 **5 V servo buck** (same topology) — adjacent

**Critical:** keep the switching loop compact: `input cap → MOSFET drain → switch node → inductor → output cap`. The switch-node copper is the noisiest point; minimise its area and keep it on L1 only, not fanned to inner layers.

### 3. 5 V USB buck (TPS54560) — midboard bridge
Sits between the high-power zone and the USB island. Feeds TUSB8041, USB ports, and the 3V3/1V1 bucks.

### 4. USB island — near the data-edge connectors
- HD3SS3220 CC controller — immediately behind the USB-C connector
- TUSB8041 — as close as possible to the USB-C upstream and three USB-A connectors; minimise SuperSpeed trace length
- TLV62569 (3V3 + 1V1 bucks) — immediately next to TUSB8041
- USB-A ESD (USBLC6-2SC6, TPD4E) + power switch (TPS2553) — right behind each USB-A connector

### 5. CH344Q servo bus controller — bridge zone
This IC bridges USB (from TUSB8041) and 4× UARTs to the servo buses. Place it between the USB island and the servo bus connectors, on the same 3V3 island as the hub. It does not need to be near the high-power section.

### 6. Servo bus drivers — at their connectors
One SP3485 + SN74LVC2G241 per channel, placed directly at the B3B/B4B-EH connector they serve.

---

## Switching loop discipline (LM5145 bucks)

The two LM5145 bucks carry the most current and generate the most EMI. Bad loops will noise up the USB SuperSpeed signals regardless of routing.

1. Input caps (bootstrap cap) as close as possible to MOSFET drain pin.
2. Inductor oriented so the switch-node end points away from the USB island.
3. Output caps immediately at the inductor output node.
4. GND pour on L1 under the switcher tied to L2 with a cluster of vias — not a single via.
5. Feedback resistors on the quiet side of the output cap (not the switch-node side).

---

## USB routing rules (TUSB8041 SuperSpeed, 10 Gbps)

- Route on L1 (or L4) over unbroken L2 GND — never cross a pour edge or plane split.
- Differential pairs: length-match within 5 mil per pair; no 90° bends; no stubs.
- Target impedance: 100 Ω differential (JLCPCB: with 0.1 mm prepreg and εr ≈ 4.5, pair width ≈ 0.175 mm, gap ≈ 0.20 mm — request impedance control when ordering).
- No switching-node copper within 3 mm of any SuperSpeed trace.

---

## JLCPCB 4-layer design rules (minimum / recommended)

| Parameter | Min | Recommended |
|-----------|-----|-------------|
| Trace width | 0.09 mm | 0.127 mm |
| Trace clearance | 0.09 mm | 0.127 mm |
| Via drill | 0.2 mm | 0.3 mm |
| Via pad | 0.4 mm | 0.6 mm |
| Through-hole drill | 0.2 mm | 0.3 mm |
| Annular ring (via) | 0.1 mm | 0.15 mm |
| Annular ring (PTH) | 0.13 mm | 0.2 mm |
| Board edge clearance | 0.3 mm | 0.5 mm |
| Silkscreen stroke | 0.15 mm | 0.15 mm |
| Silkscreen text height | 0.8 mm | 1.0 mm |

Board finish: **ENIG** recommended (fine-pitch QFN pads, USB connectors).

---

## Stackup (JLC04161H-7628)

| Layer | Type | Thickness |
|-------|------|-----------|
| F.SilkS / F.Mask | — | 0.01 mm |
| F.Cu | copper 1 oz | 0.035 mm |
| Prepreg 7628RC49% | dielectric | 0.100 mm |
| In1.Cu | copper 0.5 oz | 0.0175 mm |
| Core FR4 | dielectric | 1.265 mm |
| In2.Cu | copper 0.5 oz | 0.0175 mm |
| Prepreg 7628RC49% | dielectric | 0.100 mm |
| B.Cu | copper 1 oz | 0.035 mm |
| B.Mask / B.SilkS | — | 0.01 mm |
| **Total** | | **≈ 1.6 mm** |
