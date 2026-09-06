# solar-photovoltaics

A skill for planning, sizing, and safely installing solar power (photovoltaic) systems — for homes, apartments, caravans, motorhomes, boats, cabins, and tiny houses. Written for laypeople and professionals alike: jargon is defined on first use, every rule comes with its reasoning, and worked examples show the numbers in action.

## What it covers

- **Scenario classification** — grid-tied, off-grid, or hybrid systems
- **Energy auditing** — the load-first workflow (never size panels before the audit)
- **System voltage choice** — 12/24/48 V for mobile and standalone systems
- **Sizing** — PV arrays, battery storage, charge controllers, inverters (with worked examples for camper, boat, cabin, and home)
- **Power electronics** — MPPT vs PWM, pure-sine inverters, frequency converters (50/60 Hz), DC-DC/B2B chargers, hybrid inverters, anti-islanding
- **Battery storage** — lead-acid vs LiFePO₄ vs NMC, depth of discharge, charge profiles, SoC reading, parallel banks, safety
- **Camper/van conversion electrics** — house batteries, 12 V installation craft, solar roof mounting, alternator charging, 230 V shore power, heating energy
- **Grid-tie specifics** — roof potential, self-consumption, home batteries, balcony PV, metering, feed-in
- **Safety** — DC hazards, fusing, wire sizing, RCDs, grounding, boats, lightning protection, the DIY/professional boundary
- **Economics & regulations** — costs, payback, German feed-in tariffs and the full registration sequence

## Structure

```
solar-photovoltaics/
├── SKILL.md                          # Main workflow: golden rules + 8-step design sequence
├── references/
│   ├── electricity-basics.md         # U/I/P/R, AC vs DC, RMS, three-phase, cos φ, wire math
│   ├── solar-resource.md             # Sun, irradiation, tilt/orientation, shading, seasonality
│   ├── pv-modules.md                 # Cell tech, datasheets, temperature behavior, stringing
│   ├── inverters-converters.md       # MPPT/PWM, inverter sizing, frequency converters, hybrids
│   ├── battery-storage.md            # Chemistries, DoD, charging, sizing, safety
│   ├── offgrid-design.md             # Caravan, boat, cabin — walkthroughs + wiring rules
│   ├── van-conversion-electrics.md   # Camper deep dive: 12 V craft, shore power, heating
│   ├── gridtie-design.md             # Home rooftop, self-consumption, balcony PV
│   ├── safety-codes.md               # Fusing, disconnects, RCD, grounding, lightning, DIY limits
│   └── economics-regulations.md      # Costs, tariffs, permits, German norms
└── evals/
    └── evals.json                    # Test prompts (camper, home, sailboat)
```

## How it works

SKILL.md holds the core decision workflow (~130 lines); each reference file goes deep on one topic. The skill reads only the reference file that matches the question, keeping context lean.

## Defaults

- European/German context (230 V, 50 Hz, German tariffs and norms), with pointers on what to adapt for other regions
- Units: Wp, kWh, Ah, mm², °C
- Battery default recommendation: LiFePO₄ for new systems
