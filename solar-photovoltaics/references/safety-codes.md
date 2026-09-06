# Safety, Wiring Protection, and Codes

Run this checklist before finalizing ANY solar design. The stakes: PV DC cannot be switched off while the sun shines; DC arcs don't self-extinguish; a battery short can deliver thousands of amps; boats/vans add water, vibration, and untrained users.

## 1. The nature of the hazards

- **Panels are always live**: any two conductors of a lit array are at 20–1500 V DC. No switch at the panel. Treat every DC conductor as energized; work at dawn/dusk or cover panels (opaque blanket/cardboard) when servicing.
- **DC arcs**: AC current crosses zero 100×/s (helps extinguish arcs); DC doesn't. DC switches/breakers/fuses must be **DC-rated** — AC-rated parts can burn. An arc from a pulled MC4 under load can sustain and weld.
- **Battery short-circuit current**: a 100 Ah LFP can deliver thousands of amps for seconds — enough to vaporize a wrench. One slipped tool across terminals = fire.
- **Series strings add voltage**: 10 modules × 45 V = 450 V DC — lethal, and higher than the 120 V DC threshold where DC becomes significantly more dangerous than 230 V AC for fibrillation risk.
- **Fire history**: PV caused a three-digit number of building fires over ~30 years — mostly poor workmanship (connectors, DC arcs), not the technology. Certified installation and correct connectors (never mix connector brands!) are the countermeasures.

## 2. Fusing & overcurrent protection (off-grid/mobile)

1. **Main battery fuse** within ~15–20 cm of the battery positive terminal, rated ≥ max continuous current of the system but below cable ampacity. Types: MEGA/midi (bolt-down, 100–500 A), ANL, Class-T for large lithium banks (Class-T handles high DC interruption currents and fast lithium fault currents).
2. **Every branch fused** at its tap point (distribution fuse box), before any load.
3. **PV string fusing**: only needed with ≥3 parallel strings (backfeed into a faulted string) or if the controller requires it; 1–2 strings per MPPT need no string fuse if wire ampacity ≥ max fuse rating of the controller's short-circuit contribution.
4. Fuse placement rule: protect the **wire**, then the device. If the fuse is far from the source, the unfused span is unprotected.
5. DC breakers/switches: must be DC-rated; main battery switch rated for full bank current; PV disconnect on the DC side before the controller/inverter for service.

## 3. Wire sizing (the two constraints)

- **Ampacity** (heat): the wire must carry the current without overheating for its insulation class, bundling, and ambient temperature. Derate for engine rooms, roof heat, conduit fill.
- **Voltage drop**: `ΔU = 2 × L × I × 0.0175 / A` (mm², m, A) — keep ≤2–3% on battery/main circuits, ≤5% on minor loads. At 12 V, 2% = 0.24 V — the tightest constraint in the whole system.
- Quick table (12 V, 2% drop, one-way length): 10 A: 1 m→1.5 mm², 3 m→4 mm², 5 m→6 mm²; 20 A: 1 m→2.5 mm², 3 m→10 mm², 5 m→16 mm². Halve at 24 V, quarter at 48 V.
- Solar cable: use proper PV wire (double-insulated, UV-resistant, 90 °C+, 4–6 mm² typical); never use speaker/crimp household wire on DC power runs.
- Marine/van: tinned (marine-grade) copper wire, adhesive-lined heat-shrink, strain relief at every termination; protect cables from chafe (grommets, conduit).
- Connectors: MC4 (or brand-compatible) for panel strings — **do not intermix brands** of compatible-looking MC4 clones (the classic fire cause); crimp with proper tools only.

## 4. Disconnects & safe servicing

- Provide a way to isolate every source: PV disconnect, battery main switch, inverter DC+AC disconnects. Line them up for a "one-glance-off" state.
- Service sequence: AC loads off → inverter off → battery switch off → PV disconnect off → verify with meter → work. Cover panels for real DC work.
- Lockout habit: nobody should be able to "helpfully" re-energize while you work on a circuit.

## 5. Grounding, bonding, RCDs

- **RCD/GFCI (30 mA)** on all AC circuits that people can touch — inverter output, shore power, workshop. On boats/vans this is not optional; campsites/marinas have dirty power, so carry your own RCD adapter.
- **Equipotential bonding** (grounding): bond module frames, inverter chassis, mounting rails to a proper earth (house: per installation code; van: chassis bond; boat: DC negative bonded to engine block/battery negative, shore-power earth handled via isolation transformer or galvanic isolator to prevent galvanic corrosion).
- Boats + shore power: **isolation transformer or galvanic isolator** protects the hull's anodes and your metals; RCD always; polarity tester before plugging into foreign marinas.
- **Camper 230 V installation (VDE 0100 rules)**:
  1. Never run 12 V and 230 V in the same conduit; label duct ends.
  2. RCD (FI, 30 mA) on **every** 230 V circuit; FI/LS combined breaker directly after the CEE shore inlet, and after the inverter output if it feeds >1 socket.
  3. Shore inlet: **CEE only** (Schuko is polarity-reversible — N/L can end up swapped); CEE is polarity-safe when wired correctly.
  4. Only rubber-sheathed H07RN-F cable: ≥2.5 mm² shore feed, ≥1.5 mm² inside.
  5. **PE rail bonded to the vehicle chassis** — without this bonding the RCD cannot see a chafed-cable-to-body fault.
  6. Main switch killing all 230 V at once (emergency off).
  7. Electrical wiring never enters the gas box.
  8. 230 V work in vehicles is electrician territory + acceptance inspection (Germany: VDE 0100-610/-410/-708; mandatory "VDE-Prüfung" since 2020, needed for motorhome registration).
- Vans: AC inverter output and shore charger output should share a bonded neutral-earth arrangement per the charger/inverter design — follow the manufacturer's bonding diagram; wrong bonding of an inverter neutral is a classic shock hazard.
- Ground-fault context (large systems): string inverters monitor isolation resistance (Riso) and refuse to start below limits — never bypass.

## 6. Batteries — installation safety

- Secure mounting (vibration, 1.5 g+ in vehicles/boats), terminal covers, nothing metal on top.
- Ventilation for flooded lead-acid (hydrogen, explosive); AGM/gel minimal; lithium sealed but keep cool and dry.
- Temperature limits: charge LFP only above 0 °C (BMS blocks below — heated packs for winter); lead-acid never frozen; all chemistries: avoid >35 °C long-term placement.
- Battery room: no sparks/switches above the battery (hydrogen stratifies), smoke detector, extinguishing access, spill containment for flooded types.
- BMS communication: only one BMS per bank; paralleling prebuilt packs = only same-model, same-age, fused per pack.
- Replacement/disposal: batteries are hazardous waste — certified disposal (EU: ElektroG context).

## 7. Lightning & surge protection (rooftop)

- Norm chain (Germany): DIN EN 62305-3 / VDE 0185-305-3 supplement 5 covers PV in lightning protection systems; DIN VDE 0100-712 covers PV installation practice; VDE-AR-E 2100-712 covers DC-side fire/emergency-service safety.
- Principles: keep PV DC loops small, surge protection (SPD) on DC and AC sides per norm class, equipotential bonding of frames/rails, air-termination distances respected. External lightning protection + PV must be coordinated by design — not DIY.
- Vehicles/boats: not code-driven but practice: keep panel cables short, surge protection at the controller, avoid long unshielded antenna-like runs.

## 8. Firefighter & building safety (rooftop systems)

- Certified specialist installation is the norm and often legally required (insurance + fire rules); no flammable materials near the system; walking paths and access for the fire brigade maintained (VDE-AR-E 2100-712 concepts: DC isolation markers/switches).
- Roof fire barrier interfaces (DIN 4102 material classes) and mounting-system fire behavior matter for flat roofs.
- Insurance: building insurance extension per GDV model conditions (Germany); document everything (see economics-regulations.md).

## 9. DIY vs. professional (honest line, Germany-flavored)

- Generally acceptable DIY: panel mounting (mechanics), plug-together low-voltage DC systems (12/24 V caravan/boat DC loads with fusing), monitoring.
- Electrician territory: anything on the 230 V AC side, grid connection, meter cabinet work, feed-in sockets (balcony PV!), fixed home systems, battery integration in building systems, three-phase work.
- Grid-tie: grid operator registration, VDE-AR-N 4105 compliance, and commissioning measurement (DIN EN 62446-1) are effectively professional-only; a DIY-built grid inverter is not certifiable.
- The skill's stance: explain the physics and the wiring rules so users can *understand and check* any professional plan — and keep them inside safe, legal DIY boundaries for anything energized above 50 V or AC.

## 10. Emergency notes worth telling users

- If a PV DC connector melts/arcs: kill the inverter DC switch if safely reachable, cover the panels, do NOT pull under-load connectors by hand; call the electrician/fire service; document for insurance.
- Lithium pack that was over-discharged below BMS cutoff: do not charge blindly — have it checked (possible internal damage).
- After hail/lightning: event-based inspection before re-energizing (maintenance contract should include this).
