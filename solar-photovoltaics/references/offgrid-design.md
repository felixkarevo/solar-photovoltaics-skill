# Off-Grid System Design: Caravan, Motorhome, Boat, Cabin

Complete walkthroughs for systems with no (or unreliable) grid connection.

## 1. The design sequence (never skip steps)

1. **Energy audit** — table of every load: W × h/day = Wh/day. Include inverter standby, fridge cycling (compressor runs ~30–40% of time: 60 W nameplate ≈ 20–25 W average), and seasonal variations. Typical totals: minimalist van 0.5–1 kWh/day; comfortable caravan 1–2.5; boat with fridge 1–3; family motorhome with inverter loads 2–4; cabin 2–5 (winter heating loads are gas/diesel, not electric).
2. **Reduce before you produce** — LED everywhere, 12/24 V DC loads instead of inverter loads where possible (no inverter losses), gas/diesel for heating/cooking (energy-dense, cheap), top-loading fridges over upright, insulation.
3. **Pick system voltage** — 12 V small (≤~1 kWh/day), 24 V mid (1–3 kWh/day), 48 V large (>3 kWh/day or >2–3 kW inverter). Higher voltage = lower current = thinner wires = less loss.
4. **Size battery** (autonomy × daily ÷ DoD × efficiency) — see battery-storage.md.
5. **Size PV array** for the worst realistic sun month you'll actually use the system: `Wp = daily_Wh ÷ PSH ÷ 0.75`.
6. **Choose converters** — MPPT controller(s), inverter with surge for the worst motor start, DC-DC from alternator/shore charger as backup charge sources.
7. **Wire and protect** — fuse at battery, size cables, disconnects; see §6 and safety-codes.md.
8. **Commission and monitor** — shunt-based battery monitor, log SOC, verify with real weather.

## 2. Worked example: summer caravan (typical European family)

- Loads: 12 V compressor fridge 60 W (24 h, 35% duty) = 500 Wh; LED lights 10 W × 4 h = 40; water pump 100 W × 0.3 h = 30; phones/tablets = 30; inverter for laptop/TV = 200; misc = 100. **Total ≈ 0.9 kWh/day.**
- Battery: 0.9 kWh × 1 day ÷ (0.8 × 0.9) ≈ 1.25 kWh → **12 V 100–110 Ah LFP**.
- PV: 900 ÷ 5 PSH ÷ 0.75 ≈ **240 Wp** (2 × 120 Wp flat, or 2 × 175 Wp for cloudy margin).
- Controller: 20 A MPPT (Isc × 1.25 check); 12 V system.
- Charging backup: DC-DC charger 18–30 A from car while driving; optionally shore charger for campsites.

## 3. Worked example: live-aboard boat

- Loads: fridge 500 Wh, instruments/chartplotter 150, autopilot 300 (sailing days), lights 50, water pump 50, inverter loads (laptop, kettle briefly) 300, misc 150 → **≈1.5 kWh/day**.
- Battery: 1.5 × 2 ÷ (0.8 × 0.9) ≈ 4.2 kWh → **24 V 200 Ah LFP** (or 12 V 400 Ah if 12 V loads dominate).
- PV: 1500 ÷ 4 ÷ 0.75 ≈ **500 Wp**, split as 3–4 panels across stern arch/doghouse each with own MPPT input (dynamic mast/rigging shading).
- Extras: engine alternator as backup (via DC-DC for LFP), shore charger in marinas, windvane/throttle discipline. Marine-specific: everything rated for moisture/salt spray (IP65+ junctions), tinned copper wire, anti-vibration mounts, bonding/galvanic isolation per safety-codes.md.

## 4. Worked example: winter cabin with generator hybrid

- Critical winter load 2 kWh/day; 3-day autonomy → ~8.3 kWh LFP (see battery-storage.md).
- Winter PV at 1 PSH would need 2.7 kWp — unrealistic → **design**: 2 kWp PV for summer/shoulder + 3–5 kW genset recharging from 50% SOC to 95% (genset hours minimized); inverter/charger with genset input; auto-start controller on SOC.
- This "PV + battery + genset" triangle is the standard off-grid architecture; PV does 80–90% of annual energy, genset covers the dark doldrums.

### Heating reality check (mobile & off-grid)
- Space heating on electricity is never an off-grid option: diesel/gas heaters (0.1–0.25 l/h diesel) or wood stoves carry the thermal load; electric heating only with permanent shore power. **2 kW diesel heater is enough for a full-size van (~16 m³)**; its battery-relevant draw is the glow phase at start.
- Cooking on gas (≈2 months per 5 kg bottle for heavy cooks) or diesel spares the battery for real electric loads. Heating is usually the single biggest winter load — keep it out of the kWh audit and onto fuel.

## 5. Component selection quick table (off-grid)

| Component | 12 V system | 24 V system | 48 V system |
|---|---|---|---|
| Typical scale | <1 kWh/day | 1–3 kWh/day | >3 kWh/day |
| Inverter | ≤1500 W | ≤3000 W | 3–10 kW |
| Max DC current at 1 kW load | 93 A (!) | 47 A | 23 A |
| Main fuse | 100–150 A | 60–100 A | 32–63 A |
| Charge controller | MPPT ≤30 A typical | MPPT 20–60 A | MPPT 20–100 A / hybrid |
| Battery BMS current | 100 A class | 100–200 A | 100–200 A |

## 6. Wiring rules (off-grid DC)

- **Fuse every positive conductor within ~15–20 cm of the battery** terminal (before any branch). Battery short = fire.
- Cable sizing from the voltage-drop formula (`ΔU = 2 × L × I × ρ / A`, ρ_cu = 0.0175 Ω·mm²/m), keep main runs ≤2–3% drop:
  | Current | 1 m one-way | 3 m | 5 m | 10 m (2% drop @12 V) |
  |---|---|---|---|---|
  | 10 A | 1.5 mm² | 2.5 mm² | 4 mm² | 6–10 mm² |
  | 20 A | 2.5 mm² | 6 mm² | 10 mm² | 16 mm²+ |
  | 50 A | 6 mm² | 16 mm² | 25 mm² | rethink voltage! |
  (12 V basis; halve cross-section need at 24 V, quarter at 48 V.)
- Vehicle practice (campers): only multi-strand automotive cable (FLRY) — solid-core wire cracks under vibration; **no soldered joints** (they crack too) — use crimps/WAGO 221 with ferrules; fuse table: 1.5 mm²→10 A max fuse, 2.5→16 A, 6→25 A, 10→35 A; fuse on plus side close to battery, sized to the consumer not the cable max. See `van-conversion-electrics.md` §3 for the full craft rules.
- Panel-to-controller cables: 4–6 mm² solar cable (2×), MC4 connectors; keep runs short; avoid connectors rated below the current.
- Switch/breaker ratings: DC breakers must be DC-rated (AC breakers arc over on DC); main switch rated for full battery current.
- Shunt-based battery monitor on the negative main; all loads/charges through the shunt for honest SOC.
- 12 V accessory sockets: typically 10–15 A max (120–180 W) — not for kettles.
- Separate circuits + individual fuses per load group; label everything; carry spare fuses.

## 7. Load management and backup logic

- Priority order when battery low: cut inverter/AC loads first (biggest, least critical), keep fridge + water + lights.
- Inverter eco mode / hard off-switch to kill idle draw overnight.
- Backup charge sources: alternator DC-DC (driving), shore/genset charger (marina/campsite), generator hybrid (cabins). Never size battery for the worst week — define the backup instead.
- Monitor: daily SOC pattern reveals sizing errors within one trip.

## 8. Mobile-specific pitfalls (checklist for the user)

- Flexible panels run hotter and delaminate earlier; rigid where possible, tilt brackets in winter, secure for 130 km/h.
- Roof penetrations: marine sealant/Sikaflex, cable glands IP-rated, strain relief.
- Fridge must run while driving: DC-DC or the battery discharges into the car's system (or vice versa) — isolator logic matters.
- Lithium below 0 °C: no charging (BMS blocks) — heated packs or insulation for winter trips.
- Shore power in Europe: 230 V/16 A outlets, polarity/RCD varies by campsite — use an RCD + polarity tester; adapters across countries.
- Frequency/voltage travel: EU appliances (230 V/50 Hz) in 60 Hz countries — only frequency-tolerant devices (universal chargers) work; kettle/heater usually fine on 60 Hz; motors/clocks problematic → see inverters-converters.md §5.
- Boats: galvanic corrosion via shore power → isolation transformer or galvanic isolator; anode checks; everything above bilge waterline.
- Insurance: lithium retrofit in vehicle/boat — notify insurer; certified installs preferred.

## 9. Realism check (the numbers that disappoint people)

- Off-grid usable yield per kWp is only **130–220 kWh/a** (performance ratio 0.07–0.32) because batteries clamp the surplus — a 1 kWp array on a van yields ~0.4–0.6 kWh/day average, not 4–5 kWh like a good rooftop.
- Winter central Europe: ~1 PSH/day → 240 Wp gives ~180 Wh/day. If your winter usage is 900 Wh/day you need shore/genset backup — say so early.
- Standalone solar home systems in developing regions are costed around €1000 (battery-dependent) and compete with grid connections — small budgets are viable if loads are disciplined.
