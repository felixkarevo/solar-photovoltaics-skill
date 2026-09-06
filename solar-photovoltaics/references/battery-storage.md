# Battery Storage: Chemistries, Sizing, Charging, Care

Battery storage is the difference between "solar when the sun shines" and "solar power you own". This file covers choosing, sizing, charging, and protecting batteries.

## 1. What a battery actually stores

- Batteries store energy chemically; only capacitors and coils store electricity directly (and only for seconds). Cell voltage varies with state of charge (SOC), temperature, and current (internal resistance) — that's why discharge curves slope and why "12 V" is really 10.5–14.6 V depending on chemistry and load.
- **Series** connection adds voltage (a "12 V" lead-acid = 6 × 2 V cells; LiFePO₄ 12.8 V = 4 × 3.2 V "4S"). **Parallel** adds capacity (Ah). Battery banks = series strings in parallel; keep cells matched (same age/model).
- Capacity in Ah is meaningless without the voltage: 100 Ah at 12 V = 1200 Wh; at 24 V = 2400 Wh. Think in kWh.

## 2. Chemistry comparison (the table you'll reuse)

| Property | Lead-acid (flooded/gel/AGM) | NiMH | LiFePO₄ (LFP) | NMC/NCA |
|---|---|---|---|---|
| Nominal cell voltage | 2.0 V | 1.2 V | 3.2 V | 3.6–3.7 V |
| Practical specific energy | 25–40 Wh/kg | 60–120 | 100–180 | 150–300 |
| Energy density | 40–100 Wh/L | 140–300 | 200–400 | 430–900 |
| Round-trip efficiency | ~70–75% | ~70% | ~95% | ~95% |
| Self-discharge | 2–3%/month | 20–30%/month | <1%/month | <1%/month |
| Usable depth of discharge | ~50% (deep discharge beyond ~80% depth is damaging) | ~60–70% | 80–100% | ~80% |
| Cycle life (typ.) | 300–800 @50% DoD | 500–1000 | 3000–6000 @80% DoD | 1000–2000 @80% |
| Max realized cell capacity | ~125 Ah (large industrial higher) | ~12 Ah | >300 Ah | >120 Ah |
| Charging | staged: bulk → absorption → float | simple CC/CV | CC/CV to 3.45–3.65 V/cell, then STOP (no float) | CC/CV, BMS mandatory |
| Safety | robust; hydrogen venting (flooded) | mild | very safe (thermally stable), BMS needed | energy-dense, thermally sensitive |
| Weight for 5 kWh usable | ~150–250 kg | – | ~35–60 kg | ~25–45 kg |
| Cost per usable kWh | low upfront, high lifetime | – | medium, best lifetime cost | higher |
| Cold charging | OK if derated (frozen electrolyte at very low T) | – | **FORBIDDEN below 0 °C** (plating) | forbidden-ish below 0 °C |

- Market reality: Li-ion (mostly LFP) long ago overtook lead-acid in German home storage (by 2024 ≈ 60× the installed capacity) — LFP is the default recommendation for new systems. NMC is common in EVs; for stationary use LFP's safety and cycle life win.
- Lead-acid subtypes: flooded (maintenance, venting, best for engine starting), **AGM** (absorbed glass mat, sealed, good high-current — starter batteries), **gel** (deep-cycle, slower charge acceptance, temperature-sensitive charging voltage). Engine starting = AGM/flooded starter battery; house storage = deep-cycle type.
- Lithium for the same energy as diesel weighs ~66× more and takes ~30× the volume — irrelevant for a boat/home, prohibitive for aviation; fine for mobile use at car scale.

## 3. Depth of discharge (DoD) — the concept that saves batteries

- **Nominal vs usable capacity**: usable = nominal × allowed DoD. Lead-acid rated at C20 nominal: use only ~50% → a "100 Ah" lead-acid gives ~600 Wh of real service. LFP rated with ~full DoD: "100 Ah" gives ~1200 Wh.
- Deep discharge below the chemistry's limit **permanently damages**: lead-acid sulfates; lithium cells can be destroyed below ~2.5 V/cell (BMS's job to prevent).
- Aging rules of thumb: shallow cycling extends life; heat accelerates aging (every +10 °C roughly halves calendar life); lithium prefers mid-SOC storage (store at ~50%, not full, not empty); lead-acid prefers being kept full.
- Health criterion: a healthy battery keeps **≥80% of original capacity**.

## 4. Charging profiles

### Lead-acid (bulk / absorption / float)
1. **Bulk (CC)**: constant current up to ~80% SOC; voltage rises.
2. **Absorption (CV)**: constant voltage (e.g. 14.4 V for 12 V flooded; 14.1–14.4 gel; 14.6–14.8 AGM — follow datasheet!) until current tapers to ~2–5% of C. Van practice: max charge 14.4–14.7 V for all types; exceeding it long-term damages gel/AGM/lithium.
3. **Float**: ~13.5–13.8 V maintenance forever (fine for lead; PV systems live in float most of the time).
- Temperature compensation: −3 to −5 mV/°C/cell; never charge a frozen battery.
- Undercharge is the classic killer in solar (chronic partial charge → sulfation): size panels to actually complete absorption.
- **SoC from rest voltage (lead only)**: measure ≥4 h after charge/discharge: 100% ≈ 12.70 V (flooded) / >12.85 V (AGM); 50% ≈ 12.30 V; 25% ≈ 12.00 V; 0% <11.80 V. Low-voltage cutoff ≈ 11.8 V. Lithium SoC is NOT readable from voltage — use a shunt monitor.

### Lithium (LiFePO₄, CC/CV)
1. **CC**: constant current to ~3.45 V/cell (12.8 V bank: 13.8–14.2 V charging voltage typical).
2. **CV**: hold voltage until current tapers to ~5% C, then **stop** — no float needed (float ages lithium); if the system forces float, set it low (13.5 V/4S) or let the BMS idle.
3. **BMS (battery management system)** is mandatory: cell balancing, over/under-voltage cut-off, over-current, temperature. Charge current limit at cold (<0 °C) — buy BMS/heated packs for winter use.
- C-rate: charge/discharge current as multiple of capacity. Lead-acid comfortable ≤0.2–0.3C; LFP typically 0.5–1C continuous (check pack rating). A 100 Ah LFP at 1C takes/puts 100 A.
- Charging from 20→100% takes ~2 h at 0.5C; the last 10% is the slow CV tail — don't size systems to need 100% every day.

## 5. Sizing batteries (worked examples)

### Formula
`kWh_battery = daily_Wh × autonomy_days ÷ (DoD × efficiency)`
- efficiency: ~0.9 (round trip + inverter) for LFP, ~0.7 for lead-acid systems.

### Example A — caravan, LFP
2 kWh/day, 1 day autonomy, DoD 0.8, eff 0.9: 2000 × 1 ÷ (0.8 × 0.9) ≈ **2.8 kWh** → 12 V 220 Ah LFP (≈2.8 kWh nominal). Panels: 2 kWh ÷ 4 PSH ÷ 0.75 ≈ 670 Wp (≈4–5 × 160 Wp modules).

### Example B — home with battery (grid-tied)
4-person house (≈12 kWh/day), PV 8 kWp. Rule of thumb: **4–5 kWh storage for a 4-person household**, or ~1–1.5 kWh per kWp. Cost anchor 2023/24: 5,000–8,000 € for 4–5 kWh units. Grid-tied batteries optimize self-consumption (evening loads), not winter autonomy — winter needs the grid or sector coupling.

### Example C — winter cabin (harsh)
2 kWh/day critical load, 3 days autonomy, DoD 0.8: 2000 × 3 ÷ (0.8 × 0.9) ≈ **8.3 kWh** LFP. Winter PV at 1 PSH: 2000 ÷ 1 ÷ 0.75 ≈ 2700 Wp — often unrealistic on a cabin → add generator: batteries cover 2–3 days, genset recharges at 50% SOC.

### Battery vs load sanity anchors
- 12 V × 100 Ah = 1.2 kWh (~6h of a 200 W load)
- EV packs: 40–100+ kWh usable — with V2H/bidirectional charging an EV can double as home storage (check charger/inverter capability)
- House battery chemistry efficiency: usable system efficiency < cell efficiency (electronics + conversion); measure, don't assume 100%.

### Paralleling batteries
- Only identical type + capacity + age; charge all to 100% before connecting; never mix old with new (equalizing currents); interconnect with ≥10 mm² cable in 12 V vehicle banks. Terminal sequence: **plus first, then minus** (after minus is connected, the body is live for tools); disconnect in reverse.

## 6. Battery safety and installation

- **Fusing**: main fuse as close to the battery positive as physically possible; cable cross-section rated for the fuse. Battery = thousands of amps available in a short.
- Ventilation: flooded lead-acid vents hydrogen (explosive!) — vented compartments; AGM/gel minimal venting; lithium sealed.
- Temperature: batteries lose capacity cold (LFP ~−20% usable at −10 °C); keep them above 0 °C when charging (heated compartments for vans in winter); avoid >35 °C long-term.
- Mounting: secure against movement (boats/vans!); terminals insulated; no tools on top; keep away from water ingress paths; bilge/under-floor mounting only with rated enclosures.
- Boats: battery switching, bilge-safe mounting, and bonding per boat standards; lithium on boats demands certified packs with marine BMS.
- Transport/storage: store lithium at ~50% SOC, cool; lead-acid stored full, recharge every few months.
- Fire behavior: LFP failure mode is much milder than NMC, but any lithium fire is hard to extinguish — smoke detector in the battery bay, extinguishing access, insurance notification if required.
- Replacement planning: batteries are consumables — budget replacement inside a 20-year system life (PV modules last 25–30 a; inverter 10–15 a; LFP battery 10–15 a; lead-acid 3–7 a).

## 7. Home-storage specifics (grid-tied)

- Lithium-type; capacity = storable energy; power limits = charge/discharge currents; **usable** efficiency < cell efficiency (conversion losses, depends on SOC/temperature/age).
- Sizing anchors: 4–5 kWh for a 4-person home; or 1–1.5 kWh per kWp PV. Bigger only if EV/heat-pump loads are shifted deliberately or backup power is a goal.
- Storage raise total cost and will likely be replaced once within the 20-year horizon — include in the business case.
- Backup-power capable hybrids: define which circuits are on the backup bus (fridge, lights, sockets, water pump; not the oven/heat pump unless sized for it).
- Subsidy/program conflicts: e.g. German tenant-electricity subsidies pay only on non-buffered electricity — storage-heavy concepts may lose subsidies; check current rules.
