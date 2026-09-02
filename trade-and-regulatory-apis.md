# Trade and regulatory data: what the official APIs actually return

Measured on **2026-09-02** against the live endpoints of the US International Trade Commission, the EU's TED
procurement portal, openFDA and the USGS. Every number is a count that came back from a request, not an estimate.

## 1. US import tariffs (USITC HTS)

**The heading-only query returns nothing.** `exportList?from=9503&to=9503` answers HTTP 200 with an empty
array; `from=9503&to=9503.99.99.99` returns 11 rows. Seven of the 67 headings we checked behaved that way
(toys, cocoa beans, beer, tomatoes, raw cotton, bicycles, perfumes), so a client that queries a bare 4-digit
heading reports "no tariff lines" for products that have plenty. The 50 below are the ones we then kept.

**Rates are not all percentages.** Of 50 headings, **27 carry a general rate of `Free`** and
**9 carry a specific duty** in cents per kilogram or per litre. Some are compound and long enough to break
a fixed-width column - the general rate on the first line of cane and beet sugar (heading 1701) reads
*"3.6606¢/kg less 0.020668¢/kg for each degree under 100 degrees…"*. A schema that types the duty rate as a number is wrong before it ships.

| Heading | Product | Official description (start) | First tariff line | General rate on 2026-09-02 |
|---|---|---|---|---|
| `0901` | Coffee | Coffee, whether or not roasted or decaffeinated | `0901.11.00` | Free |
| `0902` | Tea | Tea, whether or not flavored | `0902.10.10` | 6.4% |
| `1801` | Cocoa beans | Cocoa beans, whole or broken, raw or roasted | `1801.00.00` | Free |
| `1806` | Chocolate | Chocolate and other food preparations containing cocoa | `1806.10.05.00` | Free |
| `2204` | Wine | Wine of fresh grapes, including fortified wines | `2204.10.00` | 19.8¢/liter |
| `2203` | Beer | Beer made from malt | `2203.00.00` | Free |
| `1509` | Olive oil | Olive oil and its fractions, whether or not refined, but not | `1509.20.20` | 5¢/kg on contents and container |
| `0406` | Cheese | Cheese and curd | `0406.10.02.00` | 10% |
| `1701` | Cane and beet sugar | Cane or beet sugar and chemically pure sucrose, in solid for | `1701.12.05.00` | 3.6606¢/kg less 0.020668¢/kg for each… |
| `1006` | Rice | Rice | `1006.10.00.00` | 1.8¢/kg |
| `1001` | Wheat | Wheat and meslin | `1001.11.00.00` | 0.65¢/kg |
| `0201` | Fresh beef | Meat of bovine animals, fresh or chilled | `0201.10.05` | 4.4¢/kg |
| `0203` | Pork | Meat of swine, fresh, chilled, or frozen | `0203.11.00.00` | Free |
| `0207` | Poultry meat | Meat and edible offal, of the poultry of heading 0105, fresh | `0207.11.00` | 8.8¢/kg |
| `0306` | Shrimp and prawns | Crustaceans, whether in shell or not, live, fresh, chilled,  | `0306.11.00` | Free |
| `0302` | Fresh fish | Fish, fresh or chilled, excluding fish fillets and other fis | `0302.11.00` | Free |
| `0803` | Bananas | Bananas and plantains, fresh or dried | `0803.10.10.00` | Free |
| `0804` | Avocados and dates | Dates, figs, pineapples, avocados, guavas, mangoes and mango | `0804.10.20` | 13.2¢/kg |
| `0702` | Tomatoes | Tomatoes, fresh or chilled | `0702.00.20` | 3.9¢/kg |
| `0808` | Apples and pears | Apples, pears and quinces, fresh | `0808.10.00` | Free |
| `5201` | Raw cotton | Cotton, not carded or combed | `5201.00.05.00` | Free |
| `5101` | Wool | Wool, not carded or combed | `5101.11.10.00` | Free |
| `4107` | Leather | Leather further prepared after tanning or crusting, includin | `4107.11.10` | Free |
| `6403` | Leather footwear | Footwear with outer soles of rubber, plastics, leather or co | `6403.12.30.00` | Free |
| `6109` | T-shirts | T-shirts, singlets, tank tops and similar garments, knitted  | `6109.10.00` | 16.5% |
| `6203` | Men's suits and trousers | Men's or boys' suits, ensembles, suit-type jackets, blazers, | `6203.11.15.00` | 7.5% |
| `6204` | Women's suits and trousers | Women's or girls' suits, ensembles, suit-type jackets, blaze | `6204.11.00.00` | 14% |
| `9403` | Furniture | Other furniture and parts thereof | `9403.10.00` | Free |
| `9404` | Mattresses and bedding | Mattress supports | `9404.10.00` | Free |
| `9503` | Toys | Tricycles, scooters, pedal cars and similar wheeled toys | `9503.00.00` | Free |
| `8712` | Bicycles | Bicycles and other cycles (including delivery tricycles), no | `8712.00.15` | 11% |
| `4011` | New rubber tires | New pneumatic tires, of rubber | `4011.10.10` | 4% |
| `8507` | Batteries | Electric storage batteries, including separators therefor, w | `8507.10.00` | 3.5% |
| `8541` | Semiconductor devices and solar cells | Semiconductor devices (for example, diodes, transistors, sem | `8541.10.00` | Free |
| `8542` | Integrated circuits | Electronic integrated circuits | `8542.31.00` | Free |
| `8471` | Laptops and computers | Automatic data processing machines and units thereof | `8471.30.01.00` | Free |
| `8517` | Smartphones and telephones | Telephone sets, including smartphones and other telephones f | `8517.11.00.00` | Free |
| `8528` | Televisions and monitors | Monitors and projectors, not incorporating television recept | `8528.42.00.00` | Free |
| `8418` | Refrigerators | Refrigerators, freezers and other refrigerating or freezing  | `8418.10.00` | Free |
| `8450` | Washing machines | Household- or laundry-type washing machines, including machi | `8450.11.00` | 1.4% |
| `8703` | Passenger cars | Motor cars and other motor vehicles principally designed for | `8703.10.10.00` | 2.5% |
| `8708` | Motor vehicle parts | Parts and accessories of the motor vehicles of headings 8701 | `8708.10.30` | 2.5% |
| `7208` | Hot-rolled steel | Flat-rolled products of iron or nonalloy steel, of a width o | `7208.10.15.00` | Free |
| `7601` | Unwrought aluminium | Unwrought aluminum | `7601.10.30.00` | 2.6% |
| `7403` | Refined copper | Refined copper and copper alloys, unwrought (other than mast | `7403.11.00.00` | 1% |
| `4407` | Sawn lumber | Wood sawn or chipped lengthwise, sliced or peeled, whether o | `4407.11.00` | Free |
| `4802` | Uncoated paper | Uncoated paper and paperboard, of a kind used for writing, p | `4802.10.00.00` | Free |
| `3901` | Polymers of ethylene | I. PRIMARY FORMS | `3901.10.10.00` | 6.5% |
| `3102` | Nitrogen fertilizers | Mineral or chemical fertilizers, nitrogenous | `3102.10.00` | Free |
| `3004` | Packaged medicaments | Medicaments (excluding goods of heading 3002, 3005 or 3006)  | `3004.10.10` | Free |

Endpoint: `hts.usitc.gov/reststop/exportList?from=<code>&to=<code>.99.99.99&format=JSON&styles=false`

## 2. EU public procurement (TED)

9,095 contract notices were published across these 29 countries in the seven days to 2026-09-02.
Germany alone accounts for 2107 of them - more than the twelve
quietest countries in the table put together (991).

Buyer names come back nested, and the shape changes: sometimes a string, sometimes an array, sometimes an
object keyed by language. Code that assumes one shape silently drops the other two.

| Country | Code | Notices in 7 days | Example buyers |
|---|---|---|---|
| Germany | `DEU` | 2107 | Stadtverwaltung Emmendingen; Stadt Eschweiler |
| Poland | `POL` | 1526 | POŁUDNIOWY KONCERN WĘGLOWY S.A.; GMINA STRZELECZKI |
| France | `FRA` | 936 | Bordeaux Métropole; Ville de Vienne |
| Spain | `ESP` | 522 | Ajuntament de Deltebre; Departament d'Empresa i Treball |
| Czechia | `CZE` | 407 | Fakultní nemocnice Olomouc; Pardubický kraj |
| Romania | `ROU` | 345 | REGIA NATIONALA A PADURILOR - ROMSILVA; SC TERMICA BRAD SA |
| Belgium | `BEL` | 308 | Loterie Nationale S.A. de droit public; Nationale Loterij N.V. van publiek recht |
| Sweden | `SWE` | 288 | Räddningstjänstförbundet Storgöteborg; Västra Götalandsregionen |
| Netherlands | `NLD` | 278 | Gemeente Haarlemmermeer; Fontys Hogeschool |
| Italy | `ITA` | 266 | Comune di Milano; COMUNE DI PROCIDA |
| Bulgaria | `BGR` | 175 | МИНИСТЕРСТВО НА ЗДРАВЕОПАЗВАНЕТО; ОБЩИНА БУРГАС |
| Croatia | `HRV` | 171 | URED PREDSJEDNIKA REPUBLIKE HRVATSKE; HRVATSKI SABOR |
| Lithuania | `LTU` | 164 | Vytauto Didžiojo universitetas (PV); UAB Ignitis grupės paslaugų centras (PV) |
| Norway | `NOR` | 161 | SYKEHUSINNKJØP HF; Harstad Kommune |
| Finland | `FIN` | 160 | Aalto University Foundation sr; Rikosseuraamuslaitos |
| Slovenia | `SVN` | 147 | UNIVERZITETNI KLINIČNI CENTER LJUBLJANA; NUKLEARNA ELEKTRARNA KRŠKO d.o.o. |
| Latvia | `LVA` | 143 | Akciju sabiedrība "Sadales tīkls"; Nodrošinājuma valsts aģentūra |
| Ireland | `IRL` | 137 | Clúid Housing Association; Office of Public Works (OPW) |
| Portugal | `PRT` | 136 | Águas do Tejo Atlântico, SA; Infraestruturas de Portugal S.A. |
| Austria | `AUT` | 135 | Stadt Wien - Wiener Gesundheitsverbund; WIENER LINIEN GmbH & Co KG |
| Greece | `GRC` | 118 | ΔΗΜΟΣ ΝΑΥΠΑΚΤΙΑΣ; ΠΑΝΕΠΙΣΤΗΜΙΟ ΠΕΛΟΠΟΝΝΗΣΟΥ |
| Hungary | `HUN` | 97 | Semmelweis Egyetem; MVM Démász Áramhálózati Kft. |
| Slovakia | `SVK` | 94 | Železničná spoločnosť Slovensko, a.s.; Banskobystrický samosprávny kraj |
| Denmark | `DNK` | 93 | Region Syddanmark; Tønder kommune |
| Estonia | `EST` | 70 | aktsiaselts TALLINNA SADAM; Tallinna Keskkonna- ja Kommunaalamet |
| Luxembourg | `LUX` | 54 | UNIVERSITE DU LUXEMBOURG; Fonds du Logement |
| Malta | `MLT` | 33 | Department of Contracts; Sectoral Procurement Directorate |
| Cyprus | `CYP` | 17 | Τμήμα Δασών; Τμήμα Οδικών Μεταφορών |
| Iceland | `ISL` | 7 | Fjársýsla ríkisins; Office of financial service and advisory |

Endpoint: `POST api.ted.europa.eu/v3/notices/search` with
`{"query":"publication-date>=today(-7) AND buyer-country IN (DEU)","fields":["buyer-name"]}` - no key needed.

## 3. FDA enforcement reports (openFDA)

Counts are the whole archive, not a recent window, and they range over three orders of magnitude:
*sterility* appears in 9,381 enforcement reports, *botulism* in 3. A product that offers a keyword filter
without telling the user how thin the word is will look broken the first time someone picks a rare one.

| Reason text contains | Records in the archive | Product types |
|---|---|---|
| sterility | 9,381 | food:2, drug:6267, device:3112 |
| listeria | 7,505 | food:7492, device:13 |
| contamination | 6,473 | food:3540, drug:2065, device:868 |
| salmonella | 3,658 | food:3625, drug:28, device:5 |
| milk | 3,427 | food:3423, drug:3, device:1 |
| lead | 2,813 | food:253, drug:50, device:2510 |
| labeling | 2,657 | food:433, drug:1248, device:976 |
| software | 1,874 | drug:1, device:1873 |
| soy | 1,615 | food:1613, device:2 |
| wheat | 1,573 | food:1573 |
| metal | 1,384 | food:988, drug:81, device:315 |
| peanut | 1,250 | food:1249, drug:1 |
| stability | 1,249 | food:9, drug:1044, device:196 |
| plastic | 1,102 | food:616, drug:32, device:454 |
| mislabeled | 974 | food:152, drug:551, device:271 |
| cross contamination | 919 | food:71, drug:798, device:50 |
| sterile barrier | 866 | device:866 |
| impurity | 807 | drug:807 |
| undeclared allergen | 737 | food:737 |
| particulate | 734 | food:3, drug:511, device:220 |
| foreign material | 724 | food:617, drug:18, device:89 |
| subpotent | 678 | food:4, drug:674 |
| battery | 649 | device:649 |
| glass | 542 | food:256, drug:246, device:40 |
| e. coli | 475 | food:469, drug:2, device:4 |
| dissolution | 408 | drug:402, device:6 |
| leaking | 370 | food:22, drug:75, device:273 |
| potency | 359 | food:11, drug:144, device:204 |
| clostridium | 351 | food:350, device:1 |
| cashew | 325 | food:325 |
| expired | 323 | food:29, drug:137, device:157 |
| endotoxin | 288 | drug:11, device:277 |
| mold | 269 | food:180, drug:45, device:44 |
| temperature abuse | 248 | food:56, drug:192 |
| undeclared egg | 218 | food:218 |
| sesame | 203 | food:198, drug:5 |
| gluten | 197 | food:197 |
| superpotent | 197 | drug:197 |
| undeclared sulfites | 180 | food:180 |
| firmware | 161 | device:161 |
| mislabeling | 137 | food:71, drug:12, device:54 |
| yeast | 127 | food:95, drug:30, device:2 |

Endpoint: `api.fda.gov/{food|drug|device}/enforcement.json?search=reason_for_recall:"<word>"`

## 4. USGS earthquakes

Counts are the 30 days to 2026-09-02, within the radius shown, at or above the magnitude shown.

**Magnitudes come back at full float precision** - `3.96264786337985`. Printed unrounded, that is how a data
product tells its user it was assembled carelessly.

| Around | Radius | Min magnitude | Events in 30 days | Largest |
|---|---|---|---|---|
| Hawaii (Big Island), HI | 200 km | M2+ | 141 | M5.2 42 km ESE of Naalehu, Hawaii |
| Puerto Rico | 200 km | M2.5+ | 106 | M4.1 36 km NE of Punta Cana, Dominican Republic |
| Midland, TX | 300 km | M2+ | 91 | M3.2 48 km W of Mentone, Texas |
| Reno, NV | 300 km | M2+ | 77 | M3.8 3 km N of San Leandro, CA |
| San Jose, CA | 200 km | M2+ | 67 | M3.9 6 km NW of Pinnacles, CA |
| El Paso, TX | 300 km | M2+ | 66 | M4.0 30 km ESE of Agua Prieta, Mexico |
| Bakersfield, CA | 200 km | M2+ | 58 | M4.0 10 km ENE of Coso Junction, CA |
| Sacramento, CA | 300 km | M2.5+ | 46 | M4.4 31 km NNW of Covelo, CA |
| Las Vegas, NV | 300 km | M2+ | 46 | M4.0 10 km ENE of Coso Junction, CA |
| Eureka, CA | 300 km | M2.5+ | 44 | M4.9 128 km WSW of Port Orford, Oregon |
| San Francisco, CA | 300 km | M2.5+ | 39 | M4.4 31 km NNW of Covelo, CA |
| Anchorage, AK | 300 km | M3+ | 36 | M5.6 57 km WNW of Skwentna, Alaska |
| Palm Springs, CA | 200 km | M2+ | 35 | M3.6 14 km N of Warner Springs, CA |
| Yellowstone, WY | 200 km | M1.5+ | 31 | M2.9 26 km W of Auburn, Wyoming |
| Klamath Falls, OR | 300 km | M2+ | 30 | M4.4 31 km NNW of Covelo, CA |
| Los Angeles, CA | 300 km | M2.5+ | 29 | M4.0 10 km ENE of Coso Junction, CA |
| Mammoth Lakes, CA | 150 km | M2+ | 26 | M3.3 19 km SW of Toms Place, CA |
| Idaho Falls, ID | 300 km | M2+ | 25 | M3.3 2 km NW of Little America, Wyoming |
| Salt Lake City, UT | 300 km | M2+ | 24 | M3.3 2 km NW of Little America, Wyoming |
| San Diego, CA | 300 km | M2.5+ | 17 | M3.6 14 km N of Warner Springs, CA |

Endpoint: `earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&latitude=&longitude=&maxradiuskm=&minmagnitude=&starttime=`

## If you would rather not maintain this

The same four sources, kept current and returned as rows, run on Apify:
[US import tariffs](https://apify.com/neverempty/us-import-tariff-api),
[EU tenders](https://apify.com/neverempty/eu-tender-monitor),
[FDA recalls](https://apify.com/neverempty/fda-recalls-api) and
[earthquakes](https://apify.com/neverempty/earthquakes-usgs).
