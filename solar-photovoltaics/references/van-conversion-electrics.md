# Camper Van Conversion Electrics (Deep Dive)

Vehicle-specific practice from real self-builds: house batteries, 12 V installation craft, solar mounting, alternator charging, 230 V shore power, inverters, and heating energy. Read together with `offgrid-design.md` (design flow) and `safety-codes.md` (protection rules).

## 1. House battery for vans

- **Never use the starter battery as a house battery.** Starter batteries are built for short high-current bursts then immediate recharge; deep cycling destroys them within weeks and strands the vehicle. A house battery must be a "deep cycle" type.
- Chemistry choice (van context):
  - **Flooded lead-acid**: unsuitable for vans — maintenance, gassing (must be vented out), not leak-proof, ~50% DoD. Avoid.
  - **Gel**: leak-proof, nearly maintenance-free, tolerates deeper discharge *if promptly recharged*; only ~60% DoD; weak on high current draw (careful with big inverters); poor in cold — advise against for winter use.
  - **AGM**: low internal resistance → fast charging, high surge current (good for inverters); leak-proof, maintenance-free, low self-discharge, short absorption phase; ~60% DoD; slightly shorter life than gel. The reasonable lead choice.
  - **LiFePO₄**: the clear winner for vans — full capacity usable (no 2× oversizing), no maintenance, deep discharge unproblematic, very long life (10–20 a of daily use), fast charging, light. Cost is the only con.
- Price anchors: 100 Ah AGM ≈ 100 €; equivalent-capacity LiFePO₄ ≈ 1000 €; good 200 Ah LiFePO₄ > 2000 €. Lead under daily deep-cycle use dies in 2–3 years → lithium wins economically long-term despite sticker price.
- Size recommendations ladder:
  | Battery | Fits |
  |---|---|
  | AGM/gel 80 Ah | weekend trips: fridge, lights, phone/camera |
  | AGM/gel 150 Ah | multi-week trips with decent charging |
  | AGM ≥230 Ah | weeks-to-months self-sufficient (solar + alternator), small inverter |
  | LiFePO₄ ≥150 Ah | long trips, self-sufficient standing, powerful inverter loads |
- Paralleling batteries: identical type + capacity + age, all fully charged before connecting; never mix old with new (equalizing currents); interconnect with ≥10 mm² vehicle cable; capacities add. Terminal sequence: **plus first, then minus** (after minus, the whole body is live for tools — touching body with the wrench while fitting plus = short). Disconnect in reverse (minus first). Sparks when pressing pole clamps are normal.

## 2. Battery voltages and SoC reading (lead-acid)

- Key voltage set-points (12 V bank): max charge **14.4–14.7 V** (gel/AGM/lithium are damaged if exceeded long-term — set chargers correctly); **float 13.7–13.8 V**; low-voltage cutoff **≈11.8 V** (below = deep discharge, life destroyed).
- **Rest voltage → SoC table** (measure ≥4 h after last charge/discharge; valid for LEAD only — lithium SoC is not readable from voltage, use a shunt monitor):
  | SoC | Flooded | Gel | AGM |
  |---|---|---|---|
  | 100% | 12.70 V | >12.90 V | >12.85 V |
  | 90% | 12.65 V | 12.85 V | 12.80 V |
  | 70% | 12.50 V | 12.60 V | 12.55 V |
  | 60% | 12.40 V | 12.50 V | 12.45 V |
  | 50% | 12.30 V | 12.35 V | 12.30 V |
  | 40% | 12.20 V | 12.20 V | 12.20 V |
  | 25% | 12.00 V | 12.10 V | 12.00 V |
  | 0% | <11.80 V | <11.80 V | <11.80 V |
- Cold reduces capacity and voltage for all chemistries (gel worst); size generously for cold-climate camping.
- Don't rely on one charge source: combine shore (fastest, unlimited), alternator (while driving), solar (autonomy) — they cancel each other's weaknesses.

## 3. 12 V installation craft (van practice)

- **Cable**: only automotive multi-strand wire (FLRY/FLY). Rigid solid-core cable is forbidden in vehicles — vibration fatigues it until it snaps.
- Cross-section guide + fuse limits (the table to memorize):
  | Cross-section | Use | Load capacity | Max fuse |
  |---|---|---|---|
  | 1.5 mm² | LED lighting | 15 A | 10 A |
  | 2.5 mm² | any consumer ≤~50 W (sockets, fridge, pump) | 20 A | 16 A |
  | 6 mm² | multi-consumer runs | 33 A | 25 A |
  | 10 mm² | main feed to fuse holder/main switch | 45 A | 35 A |
- Fuse **every** circuit: blade (flat) fuses in a holder, on the **plus** side, as close to the battery as possible — the unfused segment is the fire risk. Size the fuse to the *consumer*, below the cable max (e.g. 37 W device = 3 A → 5 A fuse on 2.5 mm² cable, even though 16 A would be permitted).
- **No soldered joints in vehicles** — they are rigid and crack under vibration. Use WAGO 221 lever clamps (stranded wire goes in directly), crimped plug connectors for devices, ring/tube lugs for battery and fuse holders. Crimp ferrules on stranded ends entering clamped terminals (2.5 and 6 mm² typical); strip 0.7–1.0 cm, no bare copper visible. Heat-shrink over lugs (slide on BEFORE crimping).
- Switching: every consumer not on a socket gets a switch in the plus line. 3-terminal rocker switches: two same-color terminals = plus through-path; third (silver) = LED negative, to minus rail (leave unconnected for switch-without-LED).
- Wiring topology: **all loads in parallel** (own circuit per consumer); series-wired loads are a fault (series LEDs dim). Negative distributor bar as common minus. Main battery switch (big red) between battery and fuse holder kills all 12 V at once.
- Grounding: prefer a real black minus cable back to the battery/negative distributor over chassis return for loads (negligible loss, cleaner). Where chassis ground is needed (e.g. alternator charging), make it on bare metal with a rivet nut + steel screw + pole grease against corrosion.
- Routing: empty conduit (Leerrohr) through walls before paneling, with a pull-wire for future cables; never share conduit with 230 V (see §5); label channels.
- Circuit pattern: battery + → red cable → fuse → switch → consumer → black minus → negative distributor → battery.
- 12 V sockets (cigarette type) are a practical way to power loads without dedicated switches; max ~10–15 A each.

## 4. Solar on a van roof

- Panel types for vehicles:
  | Type | Pros | Cons |
  |---|---|---|
  | Solar bag/suitcase (portable) | zero installation, aim at sun | less power, must set out, theft risk |
  | Flexible (glued flat) | light, easiest install, large glue area = secure | runs hotter (shorter life, less yield), removal destroys paint |
  | Rigid (on spoilers/rack) | best yield + life, cool underneath (reduces cabin heat), replaceable | heavier (~10 kg/module), needs spoilers or rack |
- Monocrystalline for vehicles (higher yield per m², low-light performance matters when flat-mounted).
- **Mounting, glued spoiler method**: rigid panels screwed to plastic solar spoilers, spoilers glued to roof with construction adhesive (e.g. Sikaflex 252i; tensile strength ≈3.5 N/mm² — exceeds screw pull-out when done right). Surface sequence: roughen (fine sandpaper) → degrease (silicone remover) → activator → primer → glue. Respect cure times; don't glue in cold; keep vehicle stationary ≈1 week for full cure. Fill roof corrugations with inserts/aluminum plates in the glue zone — panels must NEVER come loose (traffic hazard).
- **Roof rack method**: panels bolted to rack profiles (e.g. Thule SmartClamp on Ducato/Jumper/Boxer). DIY rack = you carry the liability.
- **Flexible glued method**: glue bead along edges or several lines along driving direction; "as much adhesive as necessary, as little as possible"; **leave a small ventilation slit at the rear edge** — trapped air overheats and kills the module.
- **Roof cable gland (Dachdurchführung)**: drill two ~8–10 mm holes, deburr, rust-protect cut edges, seat grommet cap, seal with adhesive (e.g. Sikaflex 221).
- Solar cable: outdoor-rated solar cable, 6 mm² typical for single modules and series strings, MC4 connectors; panels ship with short pigtails — buy extension cable.
- **Series vs parallel on campers: series wins** — voltage adds, current low, thin cables, and MPPT efficiency is markedly better at higher input voltage (especially sun/cloud mix with partial shading). Parallel only for many same-voltage panels that would exceed one controller. Current-matched modules required in series.
- Realistic yield fractions of rated power (empirical, central Europe):
  | Condition | Yield of rated |
  |---|---|
  | Summer full sun | 80–90% |
  | Summer overcast | ~20% |
  | Winter sun | ~60% |
  | Winter overcast | 5–15% |
- Sizing method (Ah-based): daily Ah demand × 12 V = Wh/day → required Wp = Wh/day ÷ realistic sun hours. Example: 230 Ah AGM used to 50% = 115 Ah/day = 1380 Wh → 172 Wp (at 8 h) to 276 Wp (at 5 h). Budget 5–7 h for summer travel.
- MPPT controller: PWM is "not very suitable in Europe" (loses in cool/temperate climates); MPPT gives ~10–30% more. Decode the naming: **"100/20" = 100 V max input, 20 A output**. Quick guide: 75/15 → ≤~230 Wp; 100/20 → 230–360 Wp; 150/35 → bigger camper roofs.
- Install sequence (order matters): **connect battery to controller first** (detects system voltage) → then solar → then load output. Cover panels or wire in darkness while plugging (arcing risk); never let plus/minus touch. Midi fuse in the controller→battery plus line sized to the controller (20 A controller → 40 A fuse). Bluetooth monitoring (Victron class) shows live voltage and lets you tune charge voltages per chemistry.

## 5. Alternator charging (driving charge)

- Two device classes between starter and house battery:
  | Device | Pros | Cons |
  |---|---|---|
  | **Split-charge relay (VSR)** | cheap, simple; automatic type senses voltage (no D+ wire needed) | inefficient; never fully charges the house battery (wrong voltages); long charge times; **unsuitable for lithium**; incompatible with smart alternators (Euro 5+); needs fat cables |
  | **B2B booster (battery-to-battery charger)** | adapts voltage per charge curve → full, fast, battery-friendly; selectable profiles (gel/AGM/lithium); thinner cables OK; works with smart alternators (internal engine-running detection) | pricier |
- D+ signal = alternator's "engine running" wire; hard to find on modern vehicles → prefer automatic relay or a booster with built-in detection.
- **Booster sizing rules**: charge current ≤ **30% of battery capacity** (100 Ah lithium → max 30 A; 200 Ah → 50 A OK); booster draw ≤ **60% of alternator output** (vehicle loads need headroom); 30 A is the safe default. Too-high current makes the battery prematurely "full" → damage.
- Example unit: Victron Orion-Tr Smart 12|12-30 — no D+ needed, Bluetooth config/monitoring, selectable algorithms, temperature derating, no fan. Install: near house battery; fuse **both** plus lines with Midi fuses as close as possible to each battery (60 A for a 30 A unit); 10 mm² cable typical (verify manual); configure profile + voltage limits, verify with engine running.
- The booster transforms alternator voltage up to the required 14.4–14.7 V so the house battery truly fills.

## 6. 230 V shore power in a camper (professional work!)

- Two ways to get 230 V in a van: **shore power via charger** (cheap, unlimited power, independent of battery/inverter) or **inverter** (battery-limited). A combi inverter/charger does both with internal shore priority.
- Governing rules (Germany): VDE 0100 — parts -610 (testing/acceptance by certified electrician), -410 (shock protection), -708 (campsite/caravan installations). Since 2020 a separate acceptance inspection ("VDE-Prüfung") of the 230 V install is mandatory (needed for motorhome registration anyway). Stance to convey: 12 V may tingle, **230 V can kill** — only with real competence; external electrician inspection strongly recommended even without registration (≈50 €).
- The non-negotiable rules:
  1. **Never run 12 V and 230 V in the same conduit**; label duct ends; different colors help.
  2. Grommets/strain relief at every penetration; conduit for full runs.
  3. **RCD (FI, 30 mA) on every 230 V circuit**; FI/LS combined breaker directly after the shore inlet, and after the inverter output if it feeds more than one socket.
  4. Shore inlet: **CEE only** — a Schuko plug is polarity-reversible (180° flip) and can leave N/L swapped in the van. CEE wiring is polarity-safe: plug side clockwise from earth = L (brown) then N (blue); coupler side mirrored (N then L).
  5. Cable: only **H07RN-F rubber-sheathed** multi-strand — ≥2.5 mm² for the shore feed, ≥1.5 mm² inside the van.
  6. **PE rail bonded to the vehicle chassis** (green/yellow): the chassis is touchable metal; if a cable chafes onto the body, the RCD only trips when body = PE potential. This bonding is what makes the RCD effective.
  7. Main switch that kills ALL 230 V circuits at once (emergency off).
  8. **Electrical wiring never enters the gas box** — keep power and gas strictly separated.
- Materials: small distribution board with PE rail on DIN rail, combined FI/LS 30 mA, CEE inlet + plug, H07RN-F, hollow-wall boxes, Schuko sockets (L/N to outer contacts, PE to center), 4 mm² green/yellow earth cable, ferrules, conduit.
- Stealth option: skip the exterior inlet, route the shore cable out through the door rubber gap — never crush the cable.
- IP ratings: 2-digit dust/water protection (6 = dust-tight, 7 = survives immersion). Campers see dust + moisture — choose robustly rated components.

## 7. Inverter installation in a van

- Pure sine mandatory for anything complex (modified sine may not run electronics at all). Sizing tiers:
  | Inverter | Covers |
  |---|---|
  | 500 W | laptop charging + occasional small blender |
  | 1500 W | kitchen appliances, but not simultaneously |
  | 3000 W | several powerful devices (induction + coffee machine) |
- Device power reality check: MacBook 60–96 W; hand blender 300 W; smoothie maker 600 W; kettle 600–2000 W; coffee machine 800–1200 W; toaster 900–1500 W; hairdryer 900–2000 W; induction hob 2000 W. High-watt devices drain a van battery extremely fast — small battery + kettle = nonsense; match inverter to battery and vice versa.
- Install: mount in electrics box; **battery↔inverter cable max ~100 cm** (losses + unprotected span); fuse the plus line as close to the battery as possible; **cable cross-section from surge (inrush ≈ 2× rating)**: 500 W unit → 1000 W peak → 83 A → **25 mm²**. Cross-section/current ladder: 10 mm²=45 A, 16=61, 25=83, 35=103, 50=132, 70=165 A. Hydraulic crimper (~30 €) for tube lugs ≥6 mm².
- Bond the inverter chassis to the body with **≥4 mm² green/yellow** (fault-current path if the unit fails internally).
- 230 V side: FI/LS after the inverter output when serving >1 socket. Combi unit avoids a separate shore-priority relay (internal detection of shore vs battery feeding).
- Idle draw: inverters consume power at no load — switch off when unused; 10–15% conversion loss belongs in the energy audit of every 230 V load.

## 8. Heating energy (the other half of winter autonomy)

- Options: wood stove, gas, **diesel (Standheizung)**, electric. Self-builders mostly diesel; factory motorhomes mostly gas.
- **Diesel air heater** (e.g. Autoterm/Planar Air 2D): fuel 0.1–0.25 l/h from the vehicle tank (no extra bottle weight, fuel available worldwide); electrical draw at **start** (glow phase) is the battery-relevant moment; louder at start than gas; burns poorly above ~1500 m (height kit available); E-approved versions need no TÜV/registration and keep warranty with self-install (shop install often >1000 €).
- Sizing: **2 kW is fully sufficient for most campers** (~16 m³ interior; a large L4H3 van ≈ 16 m³). 4 kW for full-time/winter regions. Oversized = short-cycling, dirty combustion, shortened life; run at full load ~20 min/month to keep it clean.
- Gas heater: quiet, standard in factory builds; 11 kg bottle ≈ 22 kg with spare; lasts only days in cold; bottle exchange abroad complicated; TÜV every 2 years; leak risk. Gas for cooking only: ~2 months per 5 kg for heavy cooks.
- **Electric heating: never plan it off-grid.** Regardless of battery size, electric heat only works with permanent shore power. Say this clearly to anyone dreaming of an all-electric van.
- Emergency heat: run the engine. Energy strategy insight: heating/cooking on fuel + electricity for everything else is the rational split (energy density + it spares the battery for real electric loads).
- Winter cautionary note: heating + ventilation prevent moisture damage; batteries lose capacity in cold (gel worst) — oversize or keep batteries warm.

## 9. What it costs (real self-build, 2022-ish)

- A documented complete self-build (vehicle incl.): ≈2,318 € electrical setup —
  - 12 V: AGM 230 Ah 350 €; B2B 30 A ≈ 275 €; LED lights, conduit, cables, connectors ≈ 390 €; main switch/sockets/fuses/distributors ≈ 100 €
  - 230 V: 500 W inverter 210 € + remote; 25 mm² cable; H07RN-F; CEE; FI/LS box ≈ 130 €; electrician inspection 50 €
  - Solar: 2 × 170 W mono 240 €; MPPT 100/20 ≈ 145 €; spoilers, cable, gland, Sikaflex system ≈ 220 €
- Heating: diesel heater kit + install help ≈ 854 €. Compressor coolbox ≈ 360 €.
- Whole camper build (incl. 5,000 € vehicle): ≈ 15,841 €. Use these as ballparks, not quotes.
