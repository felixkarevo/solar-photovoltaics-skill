# Solar Resource: Sun, Radiation, Site Analysis

Everything about how much sun your panels will actually see.

## 1. The sun as a source

- Sun surface temperature ≈ 5800 K; the sun radiates from its surface only (photosphere).
- **Solar constant (extraterrestrial)**: ≈ **1367 W/m²** (±1% over the year) on a surface facing the sun outside the atmosphere (WRC reference). Sometimes quoted ≈1360 W/m² — same thing.
- Annual solar input on Earth's surface: ~1.5 × 10¹⁸ kWh — thousands of times world energy demand (2022 primary energy ≈ 179,000 TWh ≈ 0.11‰ of it).
- Only ~53% of extraterrestrial radiation reaches the ground (scattering, absorption); global ground maximum ≈ **1000 W/m²** — the STC reference value.
- Spectrum (extraterrestrial): UV 0.25–0.38 µm, visible 0.38–0.78 µm, near-IR 0.78–2.5 µm. ~48% of intensity in the visible, ~46% near-IR.

## 2. Air Mass (AM) — how much atmosphere the light passes

- `AM = 1 / cos(zenith angle)`. AM 1 = sun at zenith; AM 1.5 = zenith ≈ 48.2° (1.5× path length); AM 2 = sun 30° above horizon.
- **AM1.5** is the standard terrestrial spectrum — used in STC (with 1000 W/m² and 25 °C cell temperature) and in all efficiency tables.
- Attenuation causes: Rayleigh/Mie scattering (air, water, dust) and absorption (O₃, H₂O, CO₂).
- Morning/evening and winter sun → higher AM → less usable light for panels; panels still produce, but weakly.

## 3. Direct, diffuse, global

- **Direct (beam)**: from the solar disc, direction-focused. Needed by concentrators and by bifacial rear sides.
- **Diffuse**: scattered, comes from the whole sky dome.
- **Global = direct + diffuse** — what flat panels receive.
- Diffuse share of global radiation: Central Europe ≈ **55% on average** (cloudy climates); Mediterranean ≈ 30%.
- Consequence: in central Europe roughly half your annual energy comes from cloudy-sky diffuse light. That is why panels produce on overcast days (weakly) and why light-grey/bright surroundings help bifacial and vertical installations.

## 4. Sun geometry (for tilt & seasonal planning)

- Declination δ: +23.45° (21 June) → 0° (21 Mar / 23 Sep) → −23.45° (21 Dec). Cooper formula from day-of-year n.
- Maximum elevation at solar noon: `α_s,max = 90° − latitude + δ`. For latitude 48° (e.g. south Germany): 65.4° in June, 42° at equinox, **18.5° in December**.
- Hour angle ω = 15°/h (solar time). Morning negative, afternoon positive.
- Practical consequences:
  - Winter sun is low → steep surfaces (50–60°+) or vertical south facades do relatively better in winter.
  - Fixed flat roofs at 20–30° are a good compromise: near-optimal annual yield, self-cleaning by rain.
  - Tracking gains ~20–40% annually but adds cost, moving parts, and winter-irrelevant surplus — rare on small systems.

## 5. Tilt & orientation — quantitative

| Configuration (Germany/EU-central) | Annual yield vs. optimum |
|---|---|
| South, 30–35° tilt | 100% (optimum) |
| South, 0° (flat) | ~88–93% |
| South, 60° | ~90% |
| East or West, 30° | ~75–80% |
| East or West, 10–20° | ~80–90% |
| NNE–NNW (avoid) | <60% |

- **Usable window in Germany**: tilt 20–40°, azimuth ±45° from south — losses stay small inside it. This is the flexibility that lets a real roof work.
- East–west split over both roof slopes shifts production into morning/evening — often better for self-consumption than a single south array (see gridtie-design).
- North-facing slopes: only worth it with very bright reflecting surroundings; check against expectations.
- Germany-wide horizontal irradiation anchors: South ≈ 1200, North ≈ 1000, Helsinki ≈ 700, Sicily ≈ 2000 kWh/m²·a. Residential planning range: 950–1300 kWh/m²·a; Central Europe ~1000; Sahara ~2350.
- Sunshine hours: ~2000 h/a in central Europe (fewer in the north).

## 6. Seasonal behavior — the mismatch problem

- Daily global irradiation in South Germany: July ≈ 5 kWh/m²·d, March ≈ 3.5, January ≈ 1.
- **Summer PV yield ≈ 10× winter yield** in central Europe.
- Household demand is opposite: **winter ≈ 2× summer** (lighting, hot water, cooking).
- Structural consequence: a fixed array hits its theoretical peak output only briefly once per day. Plan storage or sector coupling (hot water, EV, heat pump) if winter autonomy or high self-consumption matters. Winter also = the "cold dark doldrums" design case for off-grid.

## 7. Site factors

- **Shading**: the yield killer. Sources: chimneys, ventilation, dormers, trees, adjacent buildings, planned construction (object BEFORE neighbor builds — afterwards legally almost impossible), mountains, satellite dishes. A shaded cell in a series string caps the whole string's current (see pv-modules.md for bypass diodes and partial-shading behavior).
  - Screen every candidate roof with a horizon/obstruction analysis; a professional shading report is cheap insurance on big roofs.
  - Micro-inverters or per-module power optimizers rescue shaded or mixed-orientation arrays (also see inverters-converters.md).
- **Soiling**: dust, pollen, leaves, bird droppings, moss (low tilt angles). Budget cleaning at least once a year; expect extra when construction/agricultural dust, wildfire smoke, or snow-with-dirt events occur.
- **Snow**: slides off at >30° tilt; snow-covered panels produce ~nothing; weight class and sliding zone matter for mounting.
- **Temperature**: hot roofs cost yield (temperature coefficient, see pv-modules.md). Ventilated rear sides beat roof-integrated ones in hot climates by a few percent.
- **Wind load**: flat-roof and facade systems need ballast or mechanical anchoring per structural calculation; high-rise roofs typically require anchored substructure, not ballast alone.

## 8. Yield estimation — the numbers to use

- **Specific yield**: 750–1250 kWh/kWp·a (central Europe, roof-mounted, decent orientation); modern optimal grid-tied installations reach ≥1000; poor orientation/shading drops toward 750–900.
- Off-grid systems without backup generator only achieve 130–220 kWh/kWp·a of *usable* energy (batteries clamp excess) — plan accordingly.
- **Performance ratio (PR)** = actual yield ÷ (module efficiency × in-plane irradiation × area). Grid-tied central Europe: **PR ≈ 0.78** (typical 0.7–0.85). Island systems: PR 0.07–0.32 — high security is bought with unused potential.
- Quick formula: `Annual yield [kWh] = kWp × specific yield [kWh/kWp·a]`.
- Lifetime yield check (both should agree before you trust a plan):
  1. Irradiation [kWh/m²·a] × module efficiency × area [m²] × lifetime [a]
  2. Specific yield × kWp × lifetime [a]
- Public data sources for site analysis: PVGIS (EU, free), DWD CDC (German weather service), BNetzA SMARD (market/grid data), NREL NSRDB (US).
- Sanity anchor: 1 kWp ≈ 5 m² of modern modules (≈20% efficiency) produces ≈ 950–1100 kWh/a in central Europe at good orientation — about what a washing machine + dishwasher + lighting use in a year.

## 9. Off-grid / mobile radiation notes (caravan, boat)

- Summer travel (central/southern Europe, moderate tilt on a horizontal roof): expect 4–6 PSH/day in the south, 3–5 in the north at midsummer.
- Winter camping in central Europe: 0.5–1 PSH/day — panels sized for summer won't carry winter loads; plan gas/diesel backup or shore-power charging.
- Horizontal mounting loses ~10% annual vs. optimal tilt (also more soiling) — acceptable on vehicles/boats for simplicity.
- Shading on boats is brutal and dynamic (mast, rigging, dinghy on deck): favor multiple smaller panels wired to separate controller inputs or per-panel MPPTs over one big series string.
