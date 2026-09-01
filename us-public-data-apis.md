# US public data APIs: five ways a 200 does not mean "here is your data"

Measured on **2026-09-01** against the live endpoints of the National Weather Service, NOAA CO-OPS, NDBC, USGS and the FAA. Every figure below is a count, not an estimate.

## 1. NOAA tide predictions return HTTP 200 with an error object

```
GET api.tidesandcurrents.noaa.gov/api/prod/datagetter?product=predictions&station=9999999&...
→ HTTP 200
→ {"error":{"message":"No Predictions data was found. Please make sure the Datum input is valid."}}
```

Station 9999999 does not exist. The status line says 200. A client that checks `response.ok` and then reads `predictions` gets `undefined`, and — depending on how it is written — reports "no tides today" for a station that simply is not real.

The same endpoint will also happily compute predictions for **1 January 1900**, because tide predictions come from harmonic constituents rather than from stored observations. A date being accepted is not evidence that the date is sensible.

## 2. Every NDBC buoy column has missing values, and two are always missing

NDBC realtime data is **fixed-width text, not JSON**, and missing readings are the literal string `MM`:

```
#YY  MM DD hh mm WDIR WSPD GST  WVHT   DPD   APD MWD   PRES  ATMP  WTMP  DEWP  VIS PTDY  TIDE
2026 09 01 00 30   70   5.0 6.0    MM    MM    MM  MM 1017.2  27.7    MM  26.0   MM   MM    MM
```

Across **1,000 rows from 5 buoys** (41008, 46042, 44013, 51001, 42001):

| Column | Missing |
|---|---|
| `VIS` (visibility) | **100%** |
| `TIDE` | **100%** |
| `PTDY` (pressure tendency) | 83.9% |
| `DPD` (dominant wave period) | 67.5% |
| `MWD` (wave direction) | 50.0% |
| `WVHT` (wave height) | 49.8% |
| `APD` (average wave period) | 49.8% |
| `WTMP` (water temp) | 23.8% |
| `ATMP`, `DEWP` | 2.5% |
| `WDIR`, `WSPD`, `GST` | ~1.9% |
| `PRES` | 0.6% |

**Not one column was complete.** If `MM` is coerced with `parseFloat`, you get `NaN`; if it is coerced with `Number(x) || 0`, you get a wave height of zero on a buoy that reported nothing. Half the wave heights on these five buoys were missing.

## 3. The National Weather Service needs two round trips, and the grid cannot be guessed

```
GET api.weather.gov/points/40.7128,-74.0060   → gridId=OKX gridX=33 gridY=42
GET api.weather.gov/gridpoints/OKX/33,42/forecast → the forecast
```

There is no single call from a latitude/longitude to a forecast. We tried `OKX/33,35` — one row away from the real answer — and got **404**. The grid must come from the `/points` response, not from arithmetic.

Coordinates the NWS does not cover return 404 with a readable reason:

```
GET api.weather.gov/points/0.0,0.0
→ HTTP 404  "Unable to provide data for requested point 0,0"
```

That is the correct behaviour, and it is worth preserving: "we do not cover this point" is a different answer from "there is no weather".

## 4. USGS river readings carry a quality code, and the default is provisional

```
GET waterservices.usgs.gov/nwis/iv/?format=json&sites=01646500&parameterCd=00060,00065
→ 00060 (discharge) = 2700, 00065 (gage height) = 2.97
→ qualifiers: ["P"]
```

`P` means **provisional**: the value has not been reviewed and may be revised or removed later. A number copied out of this response without its qualifier looks identical to a reviewed one and is not.

## 5. The FAA airport status feed is XML

```
GET nasstatus.faa.gov/api/airport-status-information → content-type: application/xml
```

Everything else in this note is JSON or fixed-width text. A pipeline that assumes "government API" implies JSON will fail on exactly one of these five.

## Response times we measured

Single requests, from Japan, 2026-09-01:

| Endpoint | Time |
|---|---|
| NWS current observations | 184 ms |
| NWS `/points` | 306 ms |
| FAA airport status | 342 ms |
| NDBC buoy text | 574 ms |
| USGS river | 778 ms |
| NOAA tides (valid station) | 817 ms |
| USGS earthquakes | 1,121 ms |
| **NOAA tides (invalid station)** | **2,055 ms** |

The invalid station was the slowest call of the set — the error path is not the fast path.

## Ready-made versions

We maintain these as hosted Actors on Apify. In all of them, "the source had no data", "that station does not exist" and "the fetch failed" are three **different** rows, and only rows carrying an answer are charged:

- [US Weather Forecast Scraper — NWS hourly and 7-day](https://apify.com/neverempty/us-weather-forecast-api)
- [NOAA Tide Predictions — high and low tide times](https://apify.com/neverempty/noaa-tide-predictions-api)
- [NOAA Buoy Data — wave height, wind, water temperature](https://apify.com/neverempty/noaa-buoy-data-api)
- [US River Water Levels — USGS streamflow gauges](https://apify.com/neverempty/us-river-water-levels)
- [Earthquake Data — USGS live feed](https://apify.com/neverempty/earthquakes-usgs)
- [FAA Airport Delays — ground stops and closures](https://apify.com/neverempty/us-airport-delays)
- [All of our data tools](https://apify.com/neverempty)

## Licence

CC0. Quote the numbers freely; attribution welcome, not required.
