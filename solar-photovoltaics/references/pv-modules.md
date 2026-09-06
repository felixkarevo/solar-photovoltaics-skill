# PV Modules and Cells: Technology, Datasheets, Wiring

## 1. How a solar cell works (enough physics to reason with)

- A solar cell is a semiconductor diode with a light-absorbing role. Light photons with energy ≥ the bandgap (~1.1 eV for silicon) knock out electron–hole pairs; the p-n junction (or equivalent charge-selective contact) separates the charges → voltage builds up, current flows through the load.
- One silicon cell: **Voc ≈ 0.6–0.7 V** under STC, current proportional to area and irradiance (a 15×15 cm cell under 1000 W/m² receives ~10 W → a ~20% efficient cell delivers ~2 Wp).
- **I-V curve parameters** (every datasheet quotes them):
  - **Isc** — short-circuit current (max current, zero voltage)
  - **Voc** — open-circuit voltage (max voltage, zero current)
  - **Impp / Umpp** — current/voltage at the **maximum power point (MPP)**; `Umpp ≈ 0.75–0.9 × Voc`, `Impp ≈ 0.85–0.95 × Isc`
  - **Fill factor FF = (Impp·Umpp)/(Isc·Voc)** — typical 0.75–0.82; measures how "square" the curve is
  - **Efficiency η = P_max / incident power** under STC
- Irradiance response: current scales ~linearly with light; voltage only logarithmically. Half the sun ≈ half the current. In weak light, Voc drops slowly — panels still make useful voltage in dawn/dusk/cloud.
- Temperature response (silicon): **Isc +0.04%/K**, **Voc −0.4%/K**, power **≈ −0.3 to −0.45%/K**. Hot panels lose power; cold sunny panels overproduce. A "440 Wp" module at 60 °C cell temp delivers ~440 × (1 − 0.004 × 35) ≈ 380 W. Size with this in mind; report it to users who complain about summer output.
- Efficiency limits: single-junction silicon theoretical ceiling (Shockley–Queisser) ≈ 33%; best silicon lab cells 26.7%; Carnot-type thermodynamic limits are far higher (~95%) — the real limit is the bandgap physics.

## 2. Cell technologies (what you'll be offered)

| Technology | Lab cell η | Serial module η | Notes |
|---|---|---|---|
| Mono c-Si (PERC/TOPCon/SHJ) | 26–27% | 20–25% | Market standard >90% share |
| Multi c-Si | 24.4% | ~20% | Fading out; ~2027 essentially mono-only |
| a-Si thin film | 14% | ~10% | Niche (watches, calculators) |
| CIGS thin film | 23.4% | ~19% | Flexible modules, less common |
| CdTe thin film | 22% | ~20% | Utility scale (US) |
| Perovskite | 25.2% | emerging | Research/commercialization |
| Perovskite-Si tandem | 29.5% | emerging | The next efficiency jump |
| III-V triple junction | 39.5% | – | Space/drones/concentrators only |

- **Wafer lineage (silicon)**: Al-BSF (~20%, legacy) → **PERC** (~21–22% module era) → **TOPCon** (tunnel-oxide passivated contacts, current mainstream, 21–23% modules) → **SHJ/HJT** (heterojunction, best temperature coefficient, ~22–24%) → back-contact (all contacts on the rear; best module efficiency). n-type wafers are replacing p-type for higher efficiency potential.
- Monocrystalline = single crystal (uniform look, highest efficiency); polycrystalline = cheaper, lower η, being phased out.
- **Bifacial modules** also absorb rear-side light (glass-glass build): +5–30% depending on ground reflectivity and height above surface — best on bright gravel/white membranes/snow, on raised structures.
- **Half-cut cells**: standard now; halves current per cell group, reduces resistive losses and shading sensitivity.
- Purity context: solar silicon is 99.99998% pure; wafers 150–180 µm thick.

## 3. Reading a module datasheet (the fields that matter)

Typical modern datasheet (example class, 425–450 Wp):
- `Pmax/Wp` at STC (1000 W/m², 25 °C, AM1.5)
- `Pmax` at **NMOT** (800 W/m², 20 °C ambient, 45 ± 3 °C cell) — the realistic nameplate, ~75–80% of STC
- Voc / Isc / Vmpp / Impp — needed for stringing and controller window
- **Temperature coefficients**: β(Voc) ≈ −0.25 to −0.30%/K, α(Isc) ≈ +0.04–0.06%/K, γ(Pmax) ≈ −0.29 to −0.40%/K (SHJ best ≈ −0.26)
- Max system voltage (typically 1000–1500 V DC; caravan/boat gear often limited to 100 V — check the charge controller, not the module!)
- Dimensions, weight (~20–23 kg for 2 m² glass-frame), efficiency (%)
- **Warranty**: market standard 25 years ≥80% power (some 30 a/87%), 10–12 a product warranty; degradation ~0.5%/a expected
- **Module efficiency = module power ÷ module area**; area per kWp ≈ 4.5–5.5 m² at 18–22%.

## 4. Series and parallel wiring (stringing)

- **Series**: voltages add, current stays that of the weakest element. 60 cells ≈ 60 × 0.6 V ≈ 36 V Voc-class module. Strings of 2–30 modules build 48–1500 V DC for MPPT windows.
- **Parallel**: currents add, voltage stays. Parallel strings need per-string fusing when >2 strings (backfeed current) — check controller spec.
- **Mixed (2S2P etc.)**: common on vans/boats: e.g. 2 panels in series × 2 in parallel.
- Rules:
  1. Keep string Voc (cold-corrected!) below controller max input voltage with ≥10% margin. Cold correction: `Voc_cold = Voc × (1 + 0.0025 × (25 − T_min))` — Voc RISES when cold.
  2. Keep string Vmpp inside the MPPT operating window (e.g. battery voltage +10 V … 150 V).
  3. Match panels in one string (same model/current class); mismatched panels waste power (weakest caps the current).
  4. On 12/24 V battery systems with PWM controllers, panel Vmpp must be ≈1.3–1.5× battery voltage — PWM burns the surplus. MPPT controllers remove this constraint.

## 5. Shading and hot spots

- A shaded cell stops producing but the series current still flows **through** it → the cell becomes a consumer, sees reverse voltage, heats up ("hot spot") → permanent damage over time.
- **Bypass diodes** (3 per typical module, in the junction box) route current around shaded cell groups. Consequences: one shaded third of a module ≈ −33% of that module, but protected from destruction.
- Partial shading of one module in a string drags the whole string's MPP down; the string voltage may fall below the MPPT window and the controller reverts to a worse operating point.
- Mitigations: avoid shading at design time (dominant lever); half-cut cells; bypass diodes; module-level electronics (optimizers/micro-inverters) when shading is unavoidable; per-panel MPPT inputs on boats.
- Inhomogeneous light (half shade) yields less than homogeneous light at the same total flux — shade the whole panel edge-to-edge is still better than a single shadow stripe.

## 6. Degradation and lifetime

- Expected degradation ≈ **0.5%/a**; warranties guarantee 80–87% after 25–30 years.
- Failure/damage modes: hot spots (shading, cracked cells), delamination (moisture ingress), PID (potential-induced degradation — check anti-PID rating), glass breakage (hail ~25 mm rated), connector corrosion, squirrel/rodent damage on DC cables.
- Modules are embedded in polymer under glass ("sandwich") with anodized aluminum frame and junction box; useful life assumed ~25–30 years.
- Second life / disposal: modules are recyclable; legally (EU) disposal is the operator's obligation (ElektroG in Germany).

## 7. Choosing panels — decision guide

| Use case | Recommendation |
|---|---|
| Home rooftop (grid-tie) | Full-size glass-frame modules 420–500 Wp, TOPCon/SHJ, black or black-framed aesthetics; bifacial only on raised/flat roofs with bright ground |
| Van / caravan roof | Rigid monocrystalline 100–200 Wp each, mounted with tilt brackets or glued flat; flexible (semi-flex) only where weight/aerodynamics force it — they run hotter (more degradation) and are puncture-prone |
| Boat | 2–4 × 100–200 Wp rigid panels spread across stern arch/railings/doghouse, each on own MPPT input (dynamic shading); walk-on semi-flex on deck only as compromise |
| Cabin/off-grid | Same as home, wired to MPPT charge controller(s) sized to battery bank |
| Garden shed/tiny | 1–4 panels, 24 V system, MPPT |

- Wp-per-m² sanity: modern modules ≈ 200–220 Wp/m².
- For mobile use, prefer panels with robust junction boxes, pre-drilled frames, and 4–6 mm² lead cables with MC4 connectors.
