# DE440s headless assessment for a possible Celestial Navigation 2.9.x

For a future 2.9.x release, the optional, locally installed DE440s ephemeris could improve calculations that still use the plugin's analytical models—most notably predicted Moon altitudes and some Moon–planet lunar distances. The headless comparisons below show a potentially useful improvement, **but only when DE440s is used with a coherent, observer-aware WGS84 reduction**. Simply substituting DE440s positions into the present approximate altitude calculation did not reliably improve Moon results. This is research for 2.9.x; **2.8.5.9 has not been changed** and remains a workable release. Sun–Moon lunars already use DE440s when it is installed.

## Method and meaning of the distance figures

The test harness linked against the 2.8.5.9 code at commit `0dd005e` and used the checksum-pinned DE440s short kernel. It compared airless centre directions with JPL Horizons reference calculations (which report DE441), using archived dated Earth-rotation values where applicable. The altitude grid contains 25 site/date configurations; the tables below select those with a reference altitude between 5° and 85°. The Moon–Mercury/Venus rows are a smaller exploratory set of newly queried geocentric reference positions. References and the existing archived test grid are linked at the end.

The following **equivalents are not measured position errors**:

- For an altitude, 1 arcsecond (1″) corresponds approximately to **30.9 metres, or 0.0167 nautical mile, of single-sight line-of-position intercept**. One altitude sight does not by itself yield a two-dimensional fix. The measured quantity below is the error in a headless *predicted airless centre altitude*, not the error of an end-to-end fix.
- For a lunar distance, the angular difference is divided by that case's predicted lunar-distance rate to obtain a **clock-equivalent difference**. The stated distance is how far longitude along the WGS84 parallel would move *if that difference alone biased recovered UTC while latitude were independently fixed*. A real joint time-and-position solution may behave differently.
- These are model-to-model comparisons, **not claims of metre-level accuracy at sea**. They exclude actual sextant and clock errors, index error, horizon and refraction uncertainty, limb-reading uncertainty, DR error and weak solution geometry. DE440s and the Horizons DE441 reference are closely related ephemerides; their very small residuals are not fully independent proof of absolute accuracy.

## Overview

The entries below are **median / worst** absolute differences within each group.

| Airless predicted altitude | Configurations | Current analytical angular difference | Current intercept equivalent | DE440s + observer-aware WGS84 angular difference | DE440s intercept equivalent |
|---|---:|---:|---:|---:|---:|
| Moon, 5°–85° | 17 | 17.27″ / 31.53″ | 533 m (0.288 NM) / 973 m (0.525 NM) | 0.058″ / 0.123″ | 1.8 m / 3.8 m |
| Sun, 5°–85° | 21 | 0.307″ / 5.95″ | 9.5 m / 184 m (0.099 NM) | 0.011″ / 0.226″ | 0.34 m / 7.0 m |

Crucially, DE440s **with the existing approximate Moon reduction** had a median difference of **17.86″** (about **551 m / 0.298 NM** intercept-equivalent). That did not improve on the present analytical-path median of 17.27″. The gain in the right-hand columns comes from the *complete* observer-aware calculation, not a kernel swap.

## All tested Moon-altitude configurations in the 5°–85° band

| Test case | Current angular difference | Current intercept equivalent | DE440s + WGS84 angular difference | DE440s intercept equivalent |
|---|---:|---:|---:|---:|
| 2010 April | 9.05″ | 279 m / 0.151 NM | 0.001″ | <1 m |
| Before 2016 leap second | 29.29″ | 904 m / 0.488 NM | 0.122″ | 3.8 m |
| After 2016 leap second | 17.27″ | 533 m / 0.288 NM | 0.123″ | 3.8 m |
| 2020 leap day | 19.24″ | 594 m / 0.321 NM | 0.001″ | <1 m |
| March quarter | 1.82″ | 56 m / 0.030 NM | 0.111″ | 3.4 m |
| April conjunction | 17.34″ | 535 m / 0.289 NM | 0.026″ | <1 m |
| June conjunction | 25.23″ | 779 m / 0.420 NM | <0.001″ | <1 m |
| Point Judith | 16.79″ | 518 m / 0.280 NM | 0.058″ | 1.8 m |
| June equator | 18.43″ | 569 m / 0.307 NM | 0.001″ | <1 m |
| June south | 19.84″ | 612 m / 0.331 NM | 0.071″ | 2.2 m |
| June high north | 9.36″ | 289 m / 0.156 NM | 0.116″ | 3.6 m |
| June low Sun | 6.46″ | 199 m / 0.108 NM | 0.005″ | <1 m |
| September opposition | 31.53″ | 973 m / 0.525 NM | 0.002″ | <1 m |
| March 2025 west | 22.50″ | 694 m / 0.375 NM | 0.060″ | 1.8 m |
| March 2025 east | 16.47″ | 508 m / 0.275 NM | 0.094″ | 2.9 m |
| Point Judith, before | 16.75″ | 517 m / 0.279 NM | 0.058″ | 1.8 m |
| Point Judith, after | 16.85″ | 520 m / 0.281 NM | 0.058″ | 1.8 m |

These are 17 **site/date configurations**, not 17 independent real observations: some share an epoch and vary the observing site, while the Point Judith before/after cases test adjacent times.

## Exploratory Moon–planet lunar-distance comparisons

These compare predicted *geocentric centre-to-centre distances*, not a complete topocentric, limb-corrected lunar sight. The “longitude equivalent” is deliberately conditional on a known latitude and a time difference being carried into longitude.

| Test case | Body | Current → DE440s angular difference from reference | Current clock equivalent | Current conditional longitude equivalent |
|---|---|---:|---:|---:|
| 1982 Pacific | Mercury | 2.82″ → 0.004″ | 6.6 s | 2.12 km / 1.15 NM |
| 1982 Pacific | Venus | 2.03″ → 0.005″ | 4.6 s | 1.48 km / 0.80 NM |
| 2010 April | Mercury | 3.46″ → <0.001″ | 5.9 s | 2.74 km / 1.48 NM |
| 2010 April | Venus | 3.83″ → 0.007″ | 7.3 s | 3.39 km / 1.83 NM |
| March quarter | Mercury | 3.50″ → 0.004″ | 7.6 s | 3.21 km / 1.73 NM |
| March quarter | Venus | 3.20″ → 0.010″ | 6.7 s | 2.82 km / 1.52 NM |
| Point Judith | Mercury | 0.76″ → 0.062″ | 1.9 s | 0.67 km / 0.36 NM |
| Point Judith | Venus | 0.91″ → 0.074″ | 2.1 s | 0.72 km / 0.39 NM |
| March 2025 west | Mercury | 2.53″ → 0.002″ | 4.7 s | 2.07 km / 1.12 NM |
| March 2025 west | Venus | 16.60″ → 0.001″ | 28.2 s | 12.35 km / 6.67 NM |

The last Venus row illustrates why the analytical-versus-DE440s difference is worth investigating. It **does not** show that a real fix would improve by 6.67 NM. These astronomy-test sites were not selected as feasible sextant sessions: the Moon is below the horizon in the 1982 case, and the other cases have substantial daylight. Their geometry is useful for comparing ephemerides, not establishing practical sight accuracy. Across these ten rows, the DE440s residuals translate to roughly 0–59 m by the same conditional formula; that is **not an operational accuracy claim**.

For context, the 17 distinct-epoch Sun–Moon *geocentric* distance comparisons had a current analytical median/worst difference of **2.51″ / 4.10″** against the reference, versus approximately **0.001″** for DE440s. But the plugin **already uses DE440s for Sun–Moon lunars** when installed, so that result is a validation check, not a proposed new feature.

## Implication for 2.9.x

The clearest candidate is an **optional, fully observer-aware Moon-altitude calculation**, using the locally installed DE440s, WGS84 observer geometry and appropriate Earth-rotation data together. Moon–Mercury and Moon–Venus lunars are promising next candidates, but need complete topocentric, limb and multi-sight inverse tests using *observable* reference geometries before any claim about fix accuracy. Moon–star results need an independently validated star catalogue and apparent-place treatment; Jupiter and Saturn need their actual planet centres, not an unexamined substitution of planetary-system barycentres.

I would keep the present 2.8.5.9 behaviour unchanged while developing and testing these as 2.9.x options. DE440s would remain an **optional offline data pack**; the analytical calculation should remain available when it is absent or a sight falls outside the short kernel's 1850–2150 coverage. The five new planet-reference dates should be frozen as reproducible test fixtures before implementation.

## References

1. [Archived headless accuracy grid and test-site definitions, at the tested source commit](https://github.com/pob220/celestial_navigation_pi/blob/0dd005e05216e851794eec319b55ad24911f1878/validation/engine-lab/accuracy-grid.json).
2. [Archived Horizons response manifest, including query parameters and hashes](https://github.com/pob220/celestial_navigation_pi/blob/0dd005e05216e851794eec319b55ad24911f1878/validation/engine-lab/references/accuracy-20260909/manifest.json).
3. [Archived dated Earth-rotation (DUT1) values](https://github.com/pob220/celestial_navigation_pi/blob/0dd005e05216e851794eec319b55ad24911f1878/validation/engine-lab/references/dut1-20260909/manifest.json).
4. [JPL Horizons manual](https://ssd.jpl.nasa.gov/horizons/manual.html) and [Horizons API documentation](https://ssd-api.jpl.nasa.gov/doc/horizons.html).
5. [NASA/NAIF planetary SPK index, including `de440s.bsp`](https://naif.jpl.nasa.gov/pub/naif/generic_kernels/spk/planets/) and [NAIF's distinction between planetary centres and barycentres](https://naif.jpl.nasa.gov/pub/naif/toolkit_docs/C/req/naif_ids.html).
6. [JPL's DE440/DE441 description and paper](https://ssd.jpl.nasa.gov/doc/de440_de441.html).
7. [US Naval Observatory: celestial-navigation data and altitude corrections](https://aa.usno.navy.mil/data/celnav).
8. [Example direct Horizons query: Venus geocentric apparent position on 5 March 2025](https://ssd.jpl.nasa.gov/api/horizons.api?format=json&COMMAND=%27299%27&EPHEM_TYPE=%27OBSERVER%27&CENTER=%27500%40399%27&START_TIME=%272025-03-05+15%3A00%3A00%27&STOP_TIME=%272025-03-05+15%3A00%3A59%27&STEP_SIZE=%271m%27&QUANTITIES=%272%27&APPARENT=%27AIRLESS%27&ANG_FORMAT=%27DEG%27&EXTRA_PREC=%27YES%27&CSV_FORMAT=%27YES%27). The other new Mercury/Venus rows used the same settings with the listed dates and body IDs 199/299.

*Headless assessment run 17 September 2026 against source commit `0dd005e`. No plugin source, installed plugin, or catalogue package was changed.*
