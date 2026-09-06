# Economics & Regulations (German/European Context)

Costs, payback, tariffs, permits, registration. Country specifics change — verify current rules; this file gives the structure, the German defaults, and the right questions.

## 1. Cost structure

- **System cost distribution**: modules ≈ **50%** of total cost; the rest = mounting, wiring, inverters, labor, planning. Craft labor has gotten relatively more expensive while module prices fell sharply (2023/24).
- Total installed cost anchors (2024/25, Germany): single/two-family house "lower five figures" € (≈ typical 5–15 kWp systems); small multi-family "mid-to-upper five figures"; large MFH "lower six figures". Storage and heat pump NOT included.
- Storage: 5,000–8,000 € for a 4–5 kWh unit (2023/24).
- Balcony PV: 1,000–2,000 € all-in for ≤100–200 €/a savings (honest negative-EV case).
- Rural standalone solar home system: ≈ €1000 (battery-dependent) — competitive with a new grid connection where finance is available.
- LCOE must include: construction + maintenance + **inverter and battery replacement** + dismantling/disposal + taxes/fees/insurance/loan interest/meter rent, minus subsidies and feed-in revenue.
- Module prices fell >25% per production doubling (learning rate) — historical trend, not a promise.

## 2. Energy value & payback framework

- Self-consumed PV electricity displaces grid purchase at retail price (Germany: among Europe's highest; expect prices to stay high). Fed-in electricity earns the feed-in tariff — much less. Hence: **self-consumption share drives payback**.
- Degradation 0.5%/a; O&M 1–2% of system price/a; energy payback time of the hardware: **1–2 years**.
- Amortization: compute from (system cost − subsidies) ÷ annual value (self-consumption × retail price + feed-in × tariff − O&M). Typical German rooftop results today: roughly 10–15 years without storage optimization, faster with high self-consumption/EV/heat-pump coupling — always compute for the specific case, never quote generic payback as fact.
- Valuation/lifecycle: 20-year planning horizon, 5%/a straight-line depreciation; residual/market value from remaining life + yield history; property value uplift real but appraisal-dependent.
- Investment check: lifetime yield = specific yield × kWp × years (range-check against irradiation × efficiency × area × years).

## 3. Feed-in tariffs (Germany, systems commissioned through Jan 2025, BNetzA status end-2024)

ct/kWh, part feed-in / full feed-in:
| kWp | part | full |
|---|---|---|
| 10 | 8.03 | 12.73 |
| 40 | 6.95 | 10.68 |
| 100 | 5.68 | 10.68 |

With market premium/direct marketing (part / full):
| kWp | part | full |
|---|---|---|
| 10 | 8.43 | 13.13 |
| 40 | 7.35 | 11.08 |
| 100 | 6.08 | 11.08 |
| 400 | 6.08 | 9.21 |
| 1,000 | 6.08 | 7.94 |

- Tenant-electricity premium: +2.62 ct/kWh @10 kWp → +1.64 @1000 kWp.
- Trend: degression continues, no rising tariffs expected; older systems earned more than new ones will. Subsidy design conflicts exist (e.g. tenant premium pays only on non-stored electricity).
- Market context: PV feeds in with priority; midday spot prices fall with renewable surplus (negative prices occur) — dynamic tariffs and storage shift consumption into cheap hours.

## 4. Regulatory sequence (Germany as template)

Operation of a PV system counts as commercial activity by default (trade office + tax office registration; bookkeeping). Core laws: EEG (feed-in), EnWG (grid/market; §42a tenant price cap ≤75% of basic tariff), MsbG (metering), GEG (building energy), ElektroG (disposal), MaStRV (register), NAV (grid connection). ~9 federal states have PV mandates on new/renovated roofs.

**13-step checklist:**
1. Decision + business case + yield estimate
2. Quotes from specialist firms, compare, award
3. Fine planning with contractor
4. Financing (KfW via house bank, BAFA, Länder programs; portal foerderdatenbank.de), loan application
5. Construction by certified firm
6. Insurance (building-extension PV policy, GDV model conditions BPV 2016: perils fire/weather/theft, operator duties, loss-of-earnings, deductibles)
7. Grid operator registration (by contractor) + meter installation (possibly grid-compatibility check)
8. **Marktstammdatenregister** registration (BNetzA): deadline = commissioning day at earliest, **1 month** at latest; includes balcony PV; lists storage equipment
9. Trade office + tax office registration
10. Acceptance & commissioning with all parties (DIN EN 62446-1), operator briefing, documentation handover
11. Maintenance (yearly/biennial) + cleaning (≥yearly)
12. Revenue settlement + tax returns
13. End of life: certified disposal (ElektroG), sale, or self-consumption operation

- Tax: small systems can be exempt from income tax AND VAT — but then costs are NOT deductible; co-ownership splitting must be genuinely practiced; individual tax advice mandatory.
- State PV mandates: check early for minimum roof area/size rules and exemption procedures (shading report as evidence).
- Tender trigger: 1–20 MWp systems on buildings MUST bid (BNetzA windows 1 Feb/1 Jun/1 Oct).
- Legacy systems post-EEG: support ends after 20 years; continued operation then as self-supply or self-marketing.

## 5. Norms & certificates to reference

- VDE-AR-N 4105: LV grid connection of generators (inverters must comply)
- DIN EN 62446-1 / VDE 0126-23-1: commissioning tests, documentation
- DIN EN 62305-3 / VDE 0185-305-3 suppl. 5: lightning/surge protection with PV
- DIN VDE 0100-712: PV installation practice
- VDE-AR-E 2100-712: DC-side fire safety / emergency services
- VDI 6012 (mounting), VDI 2883 (maintenance); DIN 4102 (fire behavior)
- Collector standard DIN EN ISO 9806 (solar thermal)

## 6. Yield-verification & data sources

- PVGIS (EU), DWD CDC (German weather), BNetzA SMARD (market/grid), NREL NSRDB (US), HTW Berlin planning aids.
- Contractor yield estimate should be backed by on-site measurement/shading analysis for larger roofs.

## 7. Risk catalogue (top items with remedies)

1. Component defects → installer warranty claims
2. Planning errors (shading, undersized wiring) → renegotiate/re-award early
3. Contractor insolvency → new contract; stage payments
4. Price/supply volatility → deadline extensions, fixed-price quotes
5. Degradation beyond spec → warranty (80% @25 a standard)
6. Soiling/moss → cause search, extra cleaning budget
7. Animal damage (rodents on cables) → protection sleeves, insurance
8. Storm/hail/lightning → certified mounting, event inspection, insurance
9. Fire/overheating → certified install, maintenance, pv-brandsicherheit.de context
10. Demand growth → plan spare capacity (meter cabinet, ducts, inverter headroom)
11. New neighbor shading → object BEFORE construction starts
12. Sale/inheritance → valuation, documentation package
13. Grid disputes → Clearingstelle EEG/KWKG
14. Law changes/curtailment (EnWG §14a regime) → flexible design (storage, controllable loads)

## 8. Operating models (buildings)

1. Own + operate (full control/obligation)
2. Rent/lease a system (third party operates; simplest fallback where tenant electricity unviable)
3. Lease out the roof (passive income, building access encumbrances, sale complications)
- Revenue models: full feed-in (fixed tariff or market premium), self-marketing (large volumes only), part feed-in (house power + charging + surplus), tenant electricity (≥40% residential building, ≤75% of basic tariff, metering retrofits, rarely viable <15 apartments).
- Decisions need the right body: owner communities require a formal resolution (WEG); cooperatives board + member assembly.
