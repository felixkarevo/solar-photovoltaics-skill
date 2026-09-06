# Inverters and Power Converters

The electronics between panels, batteries, loads, and grid. This is where "voltage and frequency" decisions become hardware.

## 1. Converter taxonomy

| Device | Direction | Job |
|---|---|---|
| **Charge controller** | DC→DC | Panel → battery: regulate charge, protect battery |
| **DC-DC booster/converter** | DC→DC | Change DC voltage level (12→24 V, alternator→battery) |
| **Inverter** | DC→AC | Battery/panel DC → household AC 230 V/50 Hz |
| **MPPT solar inverter / hybrid inverter** | both | Inverter + charge controller + battery management + grid interface in one |
| **Frequency converter** | AC→AC | Change frequency and/or voltage (50↔60 Hz, 230↔120 V, variable-speed motor drives) |
| **Rectifier / battery charger** | AC→DC | Shore power/generator → battery |
| **Transformer** | AC→AC | Change voltage only, same frequency (heavy, simple, robust) |

## 2. Inverters for AC loads (off-grid)

### Waveform
- **Pure sine**: identical to (or cleaner than) grid power. Safe for everything: induction motors, fridges, microwaves, chargers, medical devices, audio. The default recommendation.
- **Modified sine/square**: ~30–50% cheaper; causes motor heating/buzz, microwave failures, charger noise, possible transformer overheating. Only for resistive loads (heater, incandescent) and robust tools. Avoid unless budget forces it.

### Sizing (the procedure)
1. **Continuous power**: sum of the loads that run simultaneously × 1.25 headroom. Convert to VA using worst power factor: `VA ≥ W / 0.65` for mixed motor loads.
2. **Surge power**: biggest motor/compressor start (2–6× nominal for 1–3 s). Inverter surge spec (typically 2× continuous for seconds) must cover it. Fridges: add `nominal × 3` as a check.
3. **Idle consumption**: self-consumption 5–20 W. A big inverter left on 24/7 wastes 0.1–0.5 kWh/day — on small systems that's the whole fridge. Prefer low-idle ("eco/search mode") inverters for vans/boats, or switch it off when not needed.
4. **Input voltage**: match battery bank (12/24/48 V). Current draw: `I_DC = P_AC / (U_bat × 0.9)` → a 2000 W load at 12 V pulls ~185 A! At 48 V only ~46 A. This is why >1500 W continuous loads demand 24 or 48 V.
5. **Efficiency**: modern inverters 92–96% peak; European-weighted efficiency of good units 96–98% (grid-tie class). Loss becomes heat — mount on non-flammable surface, ventilate.

### Sizing worked example (boat)
Loads: fridge 60 W avg (surge 180 W), water pump 100 W, laptop 65 W, inverter microwave 900 W occasionally. Simultaneous worst case: fridge + pump + microwave ≈ 1060 W → ×1.25 = 1325 W continuous. Surge check: 900 + 180 ≈ 1100 W start — fine. Choose a 1600–2000 VA pure-sine inverter with ≥2× surge, 12 or 24 V input, ≤1 W idle in eco mode.

### Device power reality check (typical household appliances)
MacBook 60–96 W · hand blender 300 W · smoothie maker 600 W · kettle 600–2000 W · coffee machine 800–1200 W · toaster 900–1500 W · hairdryer 900–2000 W · induction hob 2000 W. Quick inverter tiers: 500 W → laptop + small blender; 1500 W → kitchen appliances (not simultaneously); 3000 W → several powerful devices at once. Match the battery too — a small battery + kettle combination makes no sense.

## 3. Charge controllers: MPPT vs PWM

### PWM (pulse-width modulation)
- Effectively connects panel to battery through a fast switch; panel voltage collapses to battery voltage. Surplus panel voltage is wasted as heat in the controller.
- Requires panel Vmpp ≈ battery voltage × 1.3–1.5 (e.g. 36-cell "12 V panel" for 12 V battery).
- Cheap, small, lossless at matching voltages, fine for tiny systems (≤200 W, short cables).

### MPPT (maximum power point tracking)
- DC-DC converter that keeps the panel at its MPP and converts surplus voltage into extra charging current. Yield gain vs PWM: **15–30%** in cold/cloudy weather, big temperature swings, or long/undersized wiring; ~5–10% when everything matches in warm weather.
- Decouples panel voltage from battery voltage: 2 panels in series (e.g. 2 × 40 Vmpp) can charge a 12 V battery efficiently — fewer, thicker, cheaper cables.
- Sizing: `I_controller ≥ Isc × strings × 1.25` (safety factor); check max input voltage with cold-corrected Voc (Voc rises when cold — see pv-modules.md); check min startup voltage; check output current vs battery max charge rate.
- Modern MPPTs add: battery-life algorithms, load-output terminals with low-voltage disconnect, Bluetooth monitoring, multiple tracker inputs (MPP trackers per string) — multiple trackers are the right answer to mixed orientations/shading.

### Rule summary
- Small system, panel matched to battery voltage → PWM acceptable.
- Anything larger, longer cables, mixed panels, cold climate, or expansion plans → MPPT.

## 4. Hybrid / all-in-one inverters (home storage systems)

- One box: MPPT solar inputs + battery connection + AC in/out + grid feed-in + backup relay.
- **AC-coupled vs DC-coupled**: DC-coupled (panel → controller → battery → inverter) is more efficient for battery charging; AC-coupled (existing grid inverter → AC bus → hybrid inverter recharges battery) retrofits easily into existing PV. Off-grid retrofits of grid-tie systems are typically AC-coupled with frequency-shift control.
- **Backup/UPS function**: backup relay isolates the house from grid on failure (anti-islanding) and powers the backup circuit from battery. Check: backup power rating, switchover time (<20 ms for electronics), peak loads.
- Sizing the hybrid: PV input current/voltage windows per tracker, battery current limits (charge/discharge), continuous/peak AC output, 1-phase vs 3-phase, grid-code compliance for your country (e.g. VDE-AR-N 4105 in Germany).

## 5. Frequency converters (why they exist, when you need one)

- Change AC frequency and/or voltage: 50↔60 Hz, 230↔120/100 V, or variable output for motor speed control (variable-frequency drives).
- Traveling cases: European camper taking 230 V/50 Hz appliances to the Americas (60 Hz); Japanese boat equipment (50/60 Hz split country); US boat with 120 V/60 Hz shore power in a 230 V/50 Hz European marina.
- Motor loads care most: 50 Hz fans/pumps/compressors run ~17% fast on 60 Hz (and vice versa — slower, hotter); clocks misbehave; transformers are usually tolerant (60 Hz-rated iron overheats on 50 Hz).
- Modern frequency converters are power-electronic (rectifier → DC link → inverter); buy quality units, mind the input current distortion and the continuous/surge ratings like any inverter.
- Alternative that often wins for travelers: buy dual-voltage/dual-frequency appliances (universal switch-mode chargers, 100–240 V 50/60 Hz laptops) and avoid the converter for electronics entirely.

## 6. DC-DC chargers (vehicle alternator charging)

- Charges the house battery from the starter battery/alternator while driving. Mandatory in modern vehicles: "smart" alternators vary voltage and the engine-off management can't charge a lithium bank properly — a DC-DC charger provides a proper charge profile and isolates the banks.
- Features to demand: settable charge profile (LiFePO₄), current limit matched to alternator capacity (protect the alternator: ≤30–60 A typical), ignition/remote enable, optional solar input or combined units.
- Sizing rule of thumb: charge current ≤ alternator spare capacity; for LiFePO₄ in a car/van, 20–40 A units are common.

## 7. Grid-tie inverter specifics (home)

- Must synchronize to grid voltage (e.g. 230 V ±10%) and frequency (50 Hz ±0.2 Hz typical windows), feed with power factor ≈ 1 (adjustable under grid code), and **anti-island**: disconnect within ~2 s if grid fails (protects utility workers). Modern units additionally ride through short voltage/frequency dips (fault-ride-through) to avoid mass shutdowns.
- Efficiency: European weighted 96–98%; efficiency at part load matters more than peak (select an inverter whose DC/AC ratio keeps it near full load much of the day).
- **DC/AC ratio**: oversize PV vs. inverter (1.1–1.3× typical) to flatten the production curve — the inverter clips only brief midday peaks; annual energy still rises.
- Micro-inverters (one per module, AC at the module) vs. string inverter: micro = shading/mixed-orientation robust, per-panel monitoring, more cost/W and more failure points on the roof; string = cheap, simple, one box. Optimizers = middle ground (DC per module, central inverter).
- Redundancy: one string inverter = single point of failure; consider inverter replacement in 10–15 years in the lifecycle budget.

## 8. Standby and control logic (off-grid)

- Low-voltage disconnect (LVD): inverter/controller must disconnect loads before the battery is damaged (lead-acid ~11.8 V/12 V bank rested; LFP per BMS ~10 V/cell bank bottoming, typically set at 2.5–2.8 V/cell → 10.0–11.2 V for 4S).
- Load-shedding priorities: big inverter off first, keep fridge and monitoring alive; generators start on SOC threshold (e.g. 50% LFP) and stop at ~95%.
- Generator hybridization: any off-grid design above ~3 kWh/day should define a backup source (genset, shore power, DC-DC) — batteries sized for the doldrums get absurd.
