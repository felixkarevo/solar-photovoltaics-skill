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

## When to use it

The skill activates automatically whenever a conversation turns to solar power — no explicit invocation needed. Typical triggers:

- **Sizing questions** — "How many panels do I need for my van?", "What battery for a cabin?", "Is 10 kWp too much for my roof?"
- **Component choices** — MPPT vs PWM controller, LiFePO₄ vs AGM, inverter vs frequency converter, hybrid inverter selection
- **System design** — planning a new grid-tied, off-grid, or hybrid system from scratch; auditing consumption before sizing
- **Wiring and safety** — fuse sizing, cable cross-sections, grounding, RCD requirements, boat/damp-room electrics
- **Regulations and economics** — German registration steps (Marktstammdatenregister, Netzbetreiber), feed-in tariffs, payback calculations, balcony PV rules
- **Troubleshooting** — weak yields, shading problems, SoC drift in parallel battery banks, charge profile issues

It is *not* a substitute for a certified electrician: the skill explicitly flags which work (e.g. grid connection, 230 V distribution board changes) must stay professional.

## How to use it

The repo follows the open [Agent Skills](https://agentskills.io) format (`SKILL.md` + frontmatter), so any compatible agent can load it:

1. **Copy the skill folder** into your agent's skills directory, e.g.:
   - Claude Code: `~/.claude/skills/solar-photovoltaics/` (user-wide) or `.claude/skills/` (per project)
   - opencode: `~/.config/opencode/skill/solar-photovoltaics/` or `.opencode/skill/` (per project)
   - Other agents: wherever their skill/plugin folder lives
2. **That's it.** The agent reads the frontmatter `description` and loads the skill on its own when a relevant question comes up.
3. **Or invoke it explicitly** if your agent supports it: `/solar-photovoltaics How big must my camper battery be for a week off-grid?`

Best results come from giving the agent the real constraints up front — location/roof or vehicle, daily consumption (or appliance list), grid vs off-grid, and budget. The skill's 8-step workflow then drives the rest: load audit first, sizing second, safety and regulations throughout.

To try it without installing, run the prompts in [`solar-photovoltaics/evals/evals.json`](solar-photovoltaics/evals/evals.json) — they cover the three canonical scenarios (camper conversion, German family home, off-grid sailboat) and the expected answer shape for each.

## Defaults

- European/German context (230 V, 50 Hz, German tariffs and norms), with pointers on what to adapt for other regions
- Units: Wp, kWh, Ah, mm², °C
- Battery default recommendation: LiFePO₄ for new systems
