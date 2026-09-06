# Grid-Tied System Design: Home Rooftop & Building PV

For homes, apartment buildings, and any system connected to the public grid.

## 1. Quick planning numbers (central Europe)

- Roof area: **~10 m² per kWp** (≈20% module efficiency); 1 kWp ≈ 5–5.5 m² of actual module surface including gaps.
- Specific yield: **750–1250 kWh/kWp·a**; modern good installations ≥1000.
- Typical home systems: 4–10 kWp single-family house; multi-family buildings 10–100+ kWp.
- Optimum: south, ~30° tilt; usable window tilt 20–40°, azimuth ±45° (see solar-resource.md).
- Seasonality: summer yield ≈ 10× winter; winter demand ≈ 2× summer → storage + sector coupling, or accept feed-in surplus.
- Degradation 0.5%/a; planning horizon 20 years; O&M 1–2% of system price per year.

## 2. Sizing the array

Two directions, then reconcile:
1. **Roof-limited**: usable area × 1 kWp/10 m² (check orientation/shading first — a 20 m² north roof is not 2 kWp of value).
2. **Demand-limited**: aim for annual PV ≈ annual consumption (or self-consumption-optimized ~30–60% of consumption for economics without huge feed-in).
- Future loads: heat pump (+2000–4000 kWh/a), EV (+2000–4000 kWh/a at 15,000 km/a), electric hot water — plan ducts, meter cabinet space, and spare inverter capacity up front; cheap retrofits need foresight.
- Shading screen first: chimneys, vents, dormers, trees, neighbor buildings, **planned construction** (object before it starts — afterwards legally almost impossible). Use a horizon analysis or professional shading report for big roofs.

## 3. Inverter selection (grid-tie)

- Sizing ratio DC/AC 1.1–1.3 (flatten curve, more annual energy; brief midday clipping OK).
- String design: match strings to MPPT inputs; mixed orientations → separate MPPTs or optimizers/micro-inverters.
- Three-phase balance for >5 kWp: distribute across phases; 3-phase inverters feed symmetrically.
- Grid code compliance is mandatory (Germany: VDE-AR-N 4105); the inverter must include anti-islanding (disconnect when grid fails), reactive-power capability per grid operator, and remote-controllable feed-in limits where required.
- European-weighted efficiency 96–98%; part-load efficiency matters (pick inverter power so it runs near full load for much of the day).
- Single point of failure: budget inverter replacement (10–15 a) into the lifecycle.

## 4. Self-consumption strategy (the economic core)

- PV production peaks midday in summer; household demand peaks evening in winter — structural mismatch. Self-consumed electricity is worth ~2–3× the feed-in tariff (German scale), so every point of self-consumption is money.
- Increase self-consumption (in order of leverage):
  1. **Battery storage** (4–5 kWh for a 4-person home; ~1–1.5 kWh per kWp) — shifts midday to evening.
  2. **Hot water / heating support**: PV surplus → heat pump or heating element in the DHW tank (cheap thermal storage).
  3. **EV charging** at home midday; bidirectional charging (V2H) turns the EV's 40–100 kWh into house storage.
  4. **Appliance scheduling**: dishwasher/washing machine midday (timers).
  5. **East–west array split**: production shaped toward morning/evening demand.
- Larger system share ⇒ lower self-consumption percentage (roof rarely matches demand profile). Typical modern outcomes: ~30–50% self-consumption without storage, ~60–80% with battery for a well-matched home.
- Smart metering: dynamic tariffs reward charging when cheap; the grid operator can control/curtail controllable loads (heat pumps, wallboxes, storage) on overload risk (German EnWG §14a regime) — design so curtailment doesn't ruin your concept.
- Emergency/backup: standard grid-tie systems shut down with the grid (anti-islanding). Backup power needs a hybrid inverter with battery + defined backup circuits.

## 5. Home battery sizing (grid-tied)

- Default: **4–5 kWh for a 4-person household** (5,000–8,000 € at 2023/24 prices).
- Or rule: **1–1.5 kWh per kWp** of PV.
- Bigger only for: EV/heat-pump shifting, backup power requirements, or dynamic-tariff arbitrage.
- Battery is a consumable: expect one replacement within 20 years — include in the business case. Storage usable efficiency < cell efficiency (conversion + electronics); capacity fades (health criterion ≥80%).
- Chemistry: LFP standard for home storage (safety, cycle life, no float).

## 6. Balcony PV / plug-in solar (apartments, renters)

- Reality check (German 2024/25 context): savings realistically **≤100–200 €/a** against a total outlay of 1,000–2,000 € (unit + electrical retrofits + disposal) — a slow-payback proposition; worth it mainly for symbolic value/testing/long tenancy.
- Not plug-and-play in the strict sense: standard household sockets are **not rated for feed-in** — use a special feed-in socket installed by an electrician; the meter may need upgrading to a bidirectional meter.
- Registration is mandatory: grid operator **and** Marktstammdatenregister (same as any system). Landlord consent required. Indoor storage batteries are excluded for safety reasons.
- Balconies get only ~3–6 h of sun/day; don't shade neighbors (rent-reduction claims); plan removal when moving.

## 7. Multi-family buildings & tenant electricity (Mietstrom)

- Business model choice: (1) own & operate; (2) rent/lease the system (third party operates, you take full feed-in — simplest viable fallback); (3) lease out the roof (least work, third party profits, building encumbrances).
- Tenant electricity constraints (Germany): building ≥40% residential; price ≤75% of local basic-supply tariff; separate metering usually requires meter-cabinet retrofit; usually **not** viable below ~15 apartments; only non-stored electricity gets the tenant-premium subsidy.
- House/common-area power (lights, elevators, pumps) is the easy baseline self-consumption. House power may not be used for EV charging.
- Large systems ≥1 MWp trigger mandatory BNetzA tender participation (4–6 MFH can reach 1 MWp) — watch the threshold.

## 8. Metering & grid connection (Germany as template)

- Grid operator installs **bidirectional metering** (feed-in and consumption measured separately); smart meter with control box for controllable loads.
- Feed-in must be registered before/with commissioning; payments settle periodically (see economics-regulations.md for tariffs and the full registration sequence).
- Grid-stability context: frequency must stay near 50 Hz (protection thresholds 47.5/49/49.8/50.2 Hz); your inverter's ride-through/disconnect behavior is part of grid security. Negative spot prices (renewable surplus) increasingly shape when feeding in earns money — another argument for storage + flexible loads.

## 9. Commissioning & operation checklist

1. Acceptance test per DIN EN 62446-1 with installer, operator, grid operator.
2. Documentation handover: wiring diagrams, datasheets, certificates, protocols — keep for insurance/tax/sale.
3. Monitoring: inverter portal / smart-meter data; benchmark against PVGIS expectation; investigate anomalies early.
4. Maintenance contract: yearly/biennial service; wear parts included? storage replacement terms? emergency response times? event-based inspection after hail/lightning.
5. Cleaning: at least yearly, professional (safety/insurance); extra after dust storms, construction, wildfire ash, leaf fall, low-tilt moss.
6. Risk watchlist: degradation, soiling, animal damage (rodents on DC cables), storm/hail, theft, demand changes, neighbor shading, law changes, curtailment.
