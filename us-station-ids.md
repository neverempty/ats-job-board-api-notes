# US public data: station IDs that actually answer

Finding a valid station id is the slow part of using the American public data APIs. Every id below was
called on **2026-09-02** and returned data. Nothing here is copied from a documentation page.

- [NOAA tide stations](#noaa-tide-stations-50) - 50
- [NDBC buoys reporting within the last 24 hours](#ndbc-buoys-reporting-within-24-hours-50) - 50
- [NWS observation stations](#nws-observation-stations-50) - 50
- [NWS daily climate report (CLI) stations](#nws-daily-climate-report-cli-stations-50) - 50
- [State codes with zone, county and gauge counts](#state-codes-with-zone-county-and-gauge-counts-50) - 50

## Three things that cost us time

**A 200 is not data.** `api.tidesandcurrents.noaa.gov` answers HTTP 200 with an error object for a station
that does not exist. Check for the payload, not the status.

**Searching a station list by name gives you the wrong station.** NOAA's tide-prediction list holds 3,499
stations, and the closest name match is often not the one people mean. "San Diego" matches four stations -
*South San Diego Bay*, *National City*, *Quarantine Station* and, last by name length, the one you wanted:
*SAN DIEGO (Broadway)* `9410170`. "Boston" also matches *Ebon (Boston) Atoll* in the Marshall Islands.
The list mixes 1,256 harmonic stations with 2,243 subordinate ones, and the two behave differently.
We ended up naming the ids we wanted and checking each against the prediction endpoint - which is what
the table below is.

**The ids are not interchangeable.** A tide station id (`8443970`), a buoy id (`44013`), an observation
station id (`KBOS`) and a CLI code (`BOS`) can all mean "Boston" and none of them substitutes for another.

## NOAA tide stations (50)

Mean range is the average difference between high and low water, from the station's own datums;
tide type is what NOAA classifies the station as.

| Station | Place | Mean range (ft) | Tide | Lat, lon |
|---|---|---|---|---|
| `8443970` | Boston, MA | 9.5 | mixed | 42.354, -71.050 |
| `8518750` | New York (The Battery), NY | 4.5 | mixed | 40.701, -74.014 |
| `8531680` | Sandy Hook, NJ | 4.7 | mixed | 40.467, -74.009 |
| `8534720` | Atlantic City, NJ | 4.0 | mixed | 39.357, -74.418 |
| `8557380` | Lewes, DE | 4.1 | mixed | 38.783, -75.119 |
| `8574680` | Baltimore, MD | 1.1 | mixed | 39.267, -76.578 |
| `8575512` | Annapolis, MD | 1.0 | mixed | 38.984, -76.480 |
| `8594900` | Washington, DC | 2.8 | mixed | 38.873, -77.022 |
| `8638610` | Norfolk (Sewells Point), VA | 2.4 | mixed | 36.943, -76.329 |
| `8658120` | Wilmington, NC | 4.3 | mixed | 34.227, -77.953 |
| `8661070` | Myrtle Beach (Springmaid Pier), SC | 5.0 | mixed | 33.655, -78.918 |
| `8665530` | Charleston, SC | 5.2 | mixed | 32.781, -79.924 |
| `8670870` | Savannah (Fort Pulaski), GA | 6.9 | mixed | 32.035, -80.903 |
| `8720030` | Fernandina Beach, FL | 6.0 | mixed | 30.671, -81.466 |
| `8720218` | Mayport (Jacksonville), FL | 4.5 | mixed | 30.398, -81.428 |
| `8721604` | Port Canaveral (Trident Pier), FL | 3.4 | mixed | 28.416, -80.593 |
| `8722670` | Lake Worth Pier (Palm Beach), FL | 2.7 | mixed | 26.613, -80.034 |
| `8723214` | Miami (Virginia Key), FL | 2.0 | mixed | 25.731, -80.162 |
| `8724580` | Key West, FL | 1.3 | mixed | 24.556, -81.808 |
| `8725520` | Fort Myers, FL | 0.9 | mixed | 26.648, -81.871 |
| `8726520` | St. Petersburg, FL | 1.6 | mixed | 27.761, -82.627 |
| `8726724` | Clearwater Beach, FL | 1.9 | mixed | 27.978, -82.832 |
| `8729108` | Panama City, FL | 1.3 | diurnal | 30.150, -85.664 |
| `8729840` | Pensacola, FL | 1.2 | diurnal | 30.404, -87.211 |
| `8761724` | Grand Isle, LA | 1.0 | diurnal | 29.263, -89.957 |
| `8771450` | Galveston (Pier 21), TX | 1.0 | diurnal | 29.310, -94.793 |
| `8775870` | Corpus Christi, TX | 1.3 | diurnal | 27.580, -97.217 |
| `9410170` | San Diego, CA | 4.0 | mixed | 32.716, -117.177 |
| `9410230` | La Jolla, CA | 3.7 | mixed | 32.867, -117.257 |
| `9410660` | Los Angeles, CA | 3.8 | mixed | 33.720, -118.272 |
| `9410840` | Santa Monica, CA | 3.8 | mixed | 34.008, -118.500 |
| `9411340` | Santa Barbara, CA | 3.7 | mixed | 34.405, -119.692 |
| `9413450` | Monterey, CA | 3.5 | mixed | 36.609, -121.891 |
| `9414290` | San Francisco, CA | 4.1 | mixed | 37.806, -122.466 |
| `9435380` | Newport (South Beach), OR | 6.3 | mixed | 44.625, -124.045 |
| `9439040` | Astoria, OR | 6.8 | mixed | 46.207, -123.768 |
| `9444900` | Port Townsend, WA | 5.3 | mixed | 48.111, -122.760 |
| `9447130` | Seattle, WA | 7.7 | mixed | 47.603, -122.339 |
| `9452210` | Juneau, AK | 13.7 | mixed | 58.299, -134.411 |
| `9455920` | Anchorage, AK | 26.2 | mixed | 61.237, -149.890 |
| `1612340` | Honolulu, HI | 1.3 | mixed | 21.303, -157.865 |
| `1615680` | Kahului (Maui), HI | 1.6 | mixed | 20.895, -156.469 |
| `1617760` | Hilo, HI | 1.7 | mixed | 19.730, -155.056 |
| `8452660` | Newport, RI | 3.5 | mixed | 41.504, -71.326 |
| `8454000` | Providence, RI | 4.4 | mixed | 41.807, -71.401 |
| `8447930` | Woods Hole, MA | 1.8 | mixed | 41.524, -70.671 |
| `8449130` | Nantucket, MA | 3.0 | mixed | 41.285, -70.097 |
| `8418150` | Portland, ME | 9.1 | mixed | 43.658, -70.244 |
| `8413320` | Bar Harbor, ME | 10.6 | mixed | 44.392, -68.204 |
| `8570283` | Ocean City Inlet, MD | 2.1 | mixed | 38.328, -75.092 |

Endpoint: `api.tidesandcurrents.noaa.gov/api/prod/datagetter?product=predictions&interval=hilo&datum=MLLW&units=english&time_zone=lst_ldt&format=json&date=today&station=<id>`

## NDBC buoys reporting within 24 hours (50)

NDBC lists 1,352 active stations. Every buoy below had a realtime file whose newest row was less than
24 hours old when we read `ndbc.noaa.gov/data/realtime2/<id>.txt`; the list is capped at three per state.
Owner matters: an NDBC buoy and a university-run buoy publish different columns.

| Buoy | Place | Lat, lon | Owner |
|---|---|---|---|
| `41004` | EDISTO - 41 NM Southeast of Charleston, SC | 32.502, -79.099 | NDBC |
| `41008` | GRAYS REEF - 40 NM Southeast of Savannah, GA | 31.400, -80.866 | NDBC |
| `41009` | CANAVERAL 20 NM East of Cape Canaveral, FL | 28.508, -80.185 | NDBC |
| `41013` | Frying Pan Shoals, NC | 33.436, -77.764 | NDBC |
| `41024` | Sunset Nearshore, NC (SUN2) | 33.837, -78.477 | CORMP |
| `41025` | Diamond Shoals, NC | 35.026, -75.380 | NDBC |
| `41029` | Capers Nearshore, SC (CAP2) | 32.803, -79.624 | CORMP |
| `41033` | Fripp Nearshore, SC (FRP2) | 32.279, -80.406 | CORMP |
| `41043` | NE PUERTO RICO - 170 NM NNE of San Juan, PR | 21.090, -64.864 | NDBC |
| `41053` | San Juan, PR | 18.474, -66.099 | Caribbean Integrated Coastal Ocean Observing System (CarICoos) |
| `41056` | Vieques Island, PR | 18.261, -65.464 | Caribbean Integrated Coastal Ocean Observing System (CarICoos) |
| `41068` | Fort Pierce, FL (FTP) | 27.593, -80.189 | CORMP |
| `41069` | Ponce de Leon Inlet, FL (PNC) | 29.289, -80.803 | CORMP |
| `42001` | MID GULF - 180 nm South of Southwest Pass, LA | 25.922, -89.638 | NDBC |
| `42002` | WEST GULF - 207 NM East of Brownsville, TX | 25.950, -93.780 | NDBC |
| `42012` | ORANGE BEACH - 44 NM SE of Mobile, AL | 30.061, -87.547 | NDBC |
| `42035` | GALVESTON,TX - 22 NM East of Galveston, TX | 29.235, -94.410 | NDBC |
| `42084` | Southwest Pass Entrance W, LA (256) | 28.988, -89.649 | SCRIPPS |
| `44007` | PORTLAND - 12 NM Southeast of Portland,ME | 43.525, -70.140 | NDBC |
| `44009` | DELAWARE BAY 26 NM Southeast of Cape May, NJ | 38.460, -74.692 | NDBC |
| `44011` | GEORGES BANK 170 NM East of Hyannis, MA | 41.088, -66.546 | NDBC |
| `44013` | BOSTON 16 NM East of Boston, MA | 42.346, -70.651 | NDBC |
| `44014` | VIRGINIA BEACH 64 NM East of Virginia Beach, VA | 36.603, -74.837 | NDBC |
| `44025` | LONG ISLAND - 30 NM South of Islip, NY | 40.258, -73.175 | NDBC |
| `44027` | Jonesport, ME - 20 NM SE of Jonesport, ME | 44.284, -67.301 | NDBC |
| `44042` | Potomac, MD | 38.033, -76.335 | Chesapeake Bay Interpretive Buoy System (CBIBS) |
| `44058` | Stingray Point, VA | 37.567, -76.257 | Chesapeake Bay Interpretive Buoy System (CBIBS) |
| `44062` | Gooses Reef, MD | 38.556, -76.415 | Chesapeake Bay Interpretive Buoy System (CBIBS) |
| `44063` | Annapolis, MD | 38.963, -76.448 | Chesapeake Bay Interpretive Buoy System (CBIBS) |
| `44065` | New York Harbor Entrance - 15 NM SE of Breezy Point , NY | 40.368, -73.701 | NDBC |
| `44072` | York Spit, VA | 37.201, -76.266 | Chesapeake Bay Interpretive Buoy System (CBIBS) |
| `44084` | Bethany Beach, DE (263) | 38.537, -75.044 | SCRIPPS |
| `44085` | Buzzards Bay, MA (260) | 41.387, -71.032 | Woods Hole Group/NERACOOS |
| `44091` | Barnegat, NJ (209) | 39.772, -73.769 | U.S. Army Corps of Engineers |
| `44097` | Block Island, RI (154) | 40.967, -71.124 | SCRIPPS |
| `44098` | Jeffrey's Ledge, NH (160) | 42.800, -70.169 | University of New Hampshire |
| `45178` | 1 NM SE of Valcour Island, NY | 44.603, -73.394 | SUNY Plattsburgh Center for Earth and Environmental Science/Lake Champlain Research Institute |
| `46001` | WESTERN GULF OF ALASKA - 175NM SE of Kodiak, AK | 56.296, -148.027 | NDBC |
| `46002` | WEST OREGON - 275NM West of Coos Bay, OR | 42.560, -130.523 | NDBC |
| `46005` | WEST WASHINGTON - 300NM West of Aberdeen, WA | 46.147, -131.077 | NDBC |
| `46006` | SOUTHEAST PAPA - 600NM West of Eureka, CA | 40.730, -137.420 | NDBC |
| `46011` | SANTA MARIA - 21NM NW of Point Arguello, CA | 34.937, -120.999 | NDBC |
| `46013` | BODEGA BAY - 48NM NW of San Francisco, CA | 38.235, -123.317 | NDBC |
| `46015` | PORT ORFORD - 15 NM West of Port Orford, OR | 42.754, -124.839 | NDBC |
| `46035` | CENTRAL BERING SEA - 310 NM North of Adak, AK | 57.034, -177.468 | NDBC |
| `46041` | CAPE ELIZABETH - 45NM NW of Aberdeen, WA | 47.353, -124.739 | NDBC |
| `46050` | STONEWALL BANK - 20NM West of Newport, OR | 44.679, -124.535 | NDBC |
| `46060` | WEST ORCA BAY - 8NM NW of Hinchinbrook Is., AK | 60.571, -146.795 | NDBC |
| `46087` | Neah Bay - 6 NM North of Cape Flattery, WA (Traffic Separation Lighted Buoy) | 48.493, -124.727 | NDBC |
| `51000` | NORTHERN HAWAII ONE - 245NM NE of Honolulu HI | 23.534, -153.752 | NDBC |

## NWS observation stations (50)

| Station | Airport | Elevation (ft) | Lat, lon |
|---|---|---|---|
| `KJFK` | New York JFK Airport, NY | 10 | 40.639, -73.764 |
| `KLGA` | New York LaGuardia, NY | 20 | 40.779, -73.880 |
| `KEWR` | Newark Liberty, NJ | 16 | 40.682, -74.169 |
| `KLAX` | Los Angeles International, CA | 125 | 33.938, -118.389 |
| `KORD` | Chicago O'Hare, IL | 666 | 41.980, -87.904 |
| `KMDW` | Chicago Midway, IL | 617 | 41.784, -87.755 |
| `KATL` | Atlanta Hartsfield-Jackson, GA | 1027 | 33.640, -84.427 |
| `KDFW` | Dallas-Fort Worth, TX | 541 | 32.897, -97.022 |
| `KDAL` | Dallas Love Field, TX | 476 | 32.854, -96.855 |
| `KIAH` | Houston Intercontinental, TX | 89 | 29.984, -95.361 |
| `KHOU` | Houston Hobby, TX | 46 | 29.637, -95.282 |
| `KDEN` | Denver International, CO | 5404 | 39.847, -104.656 |
| `KSFO` | San Francisco International, CA | 10 | 37.620, -122.366 |
| `KSJC` | San Jose Mineta, CA | 59 | 37.359, -121.924 |
| `KOAK` | Oakland International, CA | 9 | 37.721, -122.221 |
| `KSEA` | Seattle-Tacoma, WA | 427 | 47.445, -122.314 |
| `KLAS` | Las Vegas Harry Reid, NV | 2180 | 36.072, -115.163 |
| `KPHX` | Phoenix Sky Harbor, AZ | 1115 | 33.428, -112.003 |
| `KMIA` | Miami International, FL | 10 | 25.791, -80.316 |
| `KFLL` | Fort Lauderdale, FL | 13 | 26.079, -80.162 |
| `KMCO` | Orlando International, FL | 89 | 28.418, -81.324 |
| `KTPA` | Tampa International, FL | 26 | 27.961, -82.540 |
| `KBOS` | Boston Logan, MA | 20 | 42.361, -71.011 |
| `KPHL` | Philadelphia International, PA | 7 | 39.873, -75.227 |
| `KDCA` | Washington Reagan National, DC | 13 | 38.848, -77.034 |
| `KIAD` | Washington Dulles, VA | 312 | 38.935, -77.448 |
| `KBWI` | Baltimore-Washington, MD | 135 | 39.173, -76.684 |
| `KCLT` | Charlotte Douglas, NC | 726 | 35.208, -80.961 |
| `KRDU` | Raleigh-Durham, NC | 394 | 35.892, -78.782 |
| `KDTW` | Detroit Metro, MI | 636 | 42.231, -83.331 |
| `KMSP` | Minneapolis-St. Paul, MN | 840 | 44.883, -93.229 |
| `KSTL` | St. Louis Lambert, MO | 604 | 38.752, -90.374 |
| `KMCI` | Kansas City International, MO | 1024 | 39.297, -94.731 |
| `KCLE` | Cleveland Hopkins, OH | 774 | 41.406, -81.852 |
| `KCMH` | Columbus, OH | 807 | 39.991, -82.877 |
| `KPIT` | Pittsburgh International, PA | 1203 | 40.485, -80.214 |
| `KIND` | Indianapolis International, IN | 790 | 39.725, -86.282 |
| `KBNA` | Nashville International, TN | 597 | 36.119, -86.689 |
| `KMEM` | Memphis International, TN | 253 | 35.056, -89.986 |
| `KMSY` | New Orleans Louis Armstrong, LA | 3 | 29.993, -90.251 |
| `KAUS` | Austin-Bergstrom, TX | 486 | 30.183, -97.680 |
| `KSAT` | San Antonio International, TX | 807 | 29.533, -98.464 |
| `KSAN` | San Diego International, CA | 13 | 32.734, -117.183 |
| `KPDX` | Portland International, OR | 20 | 45.596, -122.609 |
| `KSLC` | Salt Lake City, UT | 4226 | 40.771, -111.965 |
| `KABQ` | Albuquerque Sunport, NM | 5351 | 35.042, -106.615 |
| `KOKC` | Oklahoma City Will Rogers, OK | 1293 | 35.389, -97.600 |
| `KTUL` | Tulsa International, OK | 676 | 36.197, -95.886 |
| `PHNL` | Honolulu Daniel K. Inouye, HI | 10 | 21.328, -157.943 |
| `PANC` | Anchorage Ted Stevens, AK | 144 | 61.174, -149.996 |

Endpoint: `api.weather.gov/stations/<id>/observations/latest`

## NWS daily climate report (CLI) stations (50)

The CLI product carries yesterday's high, low, precipitation, snow and degree days, with record and normal
values beside them. The issuing office is the forecast office that writes the product.

| Code | City | Issuing office |
|---|---|---|
| `NYC` | New York, NY | KOKX |
| `LAX` | Los Angeles, CA | KLOX |
| `ORD` | Chicago, IL | KLOT |
| `IAH` | Houston, TX | KHGX |
| `PHX` | Phoenix, AZ | KPSR |
| `PHL` | Philadelphia, PA | KPHI |
| `SAT` | San Antonio, TX | KEWX |
| `SAN` | San Diego, CA | KSGX |
| `DFW` | Dallas-Fort Worth, TX | KFWD |
| `AUS` | Austin, TX | KEWX |
| `JAX` | Jacksonville, FL | KJAX |
| `SJC` | San Jose, CA | KMTR |
| `CMH` | Columbus, OH | KILN |
| `CLT` | Charlotte, NC | KGSP |
| `IND` | Indianapolis, IN | KIND |
| `SFO` | San Francisco, CA | KMTR |
| `SEA` | Seattle, WA | KSEW |
| `DEN` | Denver, CO | KBOU |
| `OKC` | Oklahoma City, OK | KOUN |
| `BNA` | Nashville, TN | KOHX |
| `DCA` | Washington, DC | KLWX |
| `ELP` | El Paso, TX | KEPZ |
| `LAS` | Las Vegas, NV | KVEF |
| `BOS` | Boston, MA | KBOX |
| `DTW` | Detroit, MI | KDTX |
| `PDX` | Portland, OR | KPQR |
| `SDF` | Louisville, KY | KLMK |
| `MEM` | Memphis, TN | KMEG |
| `BWI` | Baltimore, MD | KLWX |
| `MKE` | Milwaukee, WI | KMKX |
| `ABQ` | Albuquerque, NM | KABQ |
| `TUS` | Tucson, AZ | KTWC |
| `FAT` | Fresno, CA | KHNX |
| `SAC` | Sacramento, CA | KSTO |
| `ATL` | Atlanta, GA | KFFC |
| `MCI` | Kansas City, MO | KEAX |
| `MIA` | Miami, FL | KMFL |
| `RDU` | Raleigh-Durham, NC | KRAH |
| `OMA` | Omaha, NE | KOAX |
| `MSP` | Minneapolis-St. Paul, MN | KMPX |
| `TPA` | Tampa, FL | KTBW |
| `MSY` | New Orleans, LA | KLIX |
| `CLE` | Cleveland, OH | KCLE |
| `HNL` | Honolulu, HI | PHFO |
| `ANC` | Anchorage, AK | PAFC |
| `SLC` | Salt Lake City, UT | KSLC |
| `STL` | St. Louis, MO | KLSX |
| `PIT` | Pittsburgh, PA | KPBZ |
| `MCO` | Orlando, FL | KMLB |
| `BUF` | Buffalo, NY | KBUF |

Endpoint: `api.weather.gov/products/types/CLI/locations/<code>`

## State codes with zone, county and gauge counts (50)

Warnings are issued per forecast zone, not per state, so the zone count is the real size of a state-wide
alert query. The gauge count is active USGS gauges answering on 2026-09-02.

| State | Code | NWS forecast zones | Counties | Active USGS gauges |
|---|---|---|---|---|
| Alabama | `AL` | 71 | 67 | 210 |
| Alaska | `AK` | 119 | 30 | 126 |
| Arizona | `AZ` | 74 | 15 | 211 |
| Arkansas | `AR` | 92 | 75 | 182 |
| California | `CA` | 209 | 58 | 540 |
| Colorado | `CO` | 85 | 64 | 362 |
| Connecticut | `CT` | 13 | 8 | 76 |
| Delaware | `DE` | 4 | 3 | 38 |
| Florida | `FL` | 127 | 67 | 613 |
| Georgia | `GA` | 168 | 159 | 354 |
| Hawaii | `HI` | 43 | 4 | 109 |
| Idaho | `ID` | 47 | 44 | 231 |
| Illinois | `IL` | 106 | 102 | 249 |
| Indiana | `IN` | 95 | 92 | 258 |
| Iowa | `IA` | 99 | 99 | 187 |
| Kansas | `KS` | 105 | 105 | 217 |
| Kentucky | `KY` | 120 | 120 | 218 |
| Louisiana | `LA` | 88 | 64 | 329 |
| Maine | `ME` | 33 | 16 | 70 |
| Maryland | `MD` | 30 | 24 | 155 |
| Massachusetts | `MA` | 26 | 14 | 139 |
| Michigan | `MI` | 91 | 83 | 238 |
| Minnesota | `MN` | 98 | 87 | 146 |
| Mississippi | `MS` | 85 | 82 | 142 |
| Missouri | `MO` | 115 | 115 | 253 |
| Montana | `MT` | 83 | 56 | 235 |
| Nebraska | `NE` | 95 | 93 | 150 |
| Nevada | `NV` | 26 | 17 | 155 |
| New Hampshire | `NH` | 15 | 10 | 58 |
| New Jersey | `NJ` | 30 | 21 | 163 |
| New Mexico | `NM` | 65 | 33 | 203 |
| New York | `NY` | 88 | 62 | 328 |
| North Carolina | `NC` | 116 | 100 | 291 |
| North Dakota | `ND` | 58 | 53 | 156 |
| Ohio | `OH` | 89 | 88 | 312 |
| Oklahoma | `OK` | 82 | 77 | 204 |
| Oregon | `OR` | 56 | 36 | 307 |
| Pennsylvania | `PA` | 78 | 67 | 386 |
| Rhode Island | `RI` | 8 | 5 | 40 |
| South Carolina | `SC` | 60 | 46 | 242 |
| South Dakota | `SD` | 78 | 66 | 160 |
| Tennessee | `TN` | 102 | 95 | 137 |
| Texas | `TX` | 298 | 254 | 791 |
| Utah | `UT` | 38 | 29 | 180 |
| Vermont | `VT` | 20 | 14 | 54 |
| Virginia | `VA` | 115 | 133 | 246 |
| Washington | `WA` | 68 | 39 | 320 |
| West Virginia | `WV` | 68 | 55 | 175 |
| Wisconsin | `WI` | 74 | 72 | 273 |
| Wyoming | `WY` | 58 | 23 | 112 |

Endpoints: `api.weather.gov/alerts/active?area=<code>`, `api.weather.gov/zones?area=<code>&type=forecast`,
`waterservices.usgs.gov/nwis/iv/?format=json&stateCd=<code>&parameterCd=00065&siteStatus=active`

## If you would rather not maintain this

The same data, kept current and returned as rows, runs on Apify:
[tide predictions](https://apify.com/neverempty/noaa-tide-predictions-api),
[buoy observations](https://apify.com/neverempty/noaa-buoy-data-api),
[current conditions](https://apify.com/neverempty/us-weather-observations),
[daily climate reports](https://apify.com/neverempty/us-climate-reports),
[active alerts](https://apify.com/neverempty/us-weather-alerts) and
[river levels](https://apify.com/neverempty/us-river-water-levels).
