# What each public ATS job board API actually returns

Measured notes on the public job board endpoints of **Greenhouse, Lever, Ashby, Workable and Workday**.

Every number here was produced by calling the live endpoints on **2026-09-01** and counting the rows that came back. Nothing is estimated. Where a figure depends on the company rather than the ATS, it says so.

**See also: [which ATS each of 193 companies uses](company-ats-map.md)** - board slugs, board URLs and open role counts, all measured.

**See also: [which ATS each of 193 companies uses](us-station-ids.md)** - board slugs, board URLs and open role counts, all measured.

## The short version

| | Greenhouse | Lever | Ashby | Workable | Workday |
|---|---|---|---|---|---|
| `title`, job URL | 100% | 100% | 100% | 100% | 100% |
| `postedAt` | 100% | 100% | 100% | 100% | **0%** |
| `department` | 100% | 100% | 100% | 13–100% | **0%** |
| `employmentType` | **0%** | 96% | 100% | 78–100% | **0%** |
| `workplaceType` | **0%** | 100% | 89–100% | 100% | **0%** |
| `isRemote` | **0%** | 0–34% | 89–100% | 0–5% | **0%** |
| structured salary | **0%** | **0%** | **0–96%** | **0%** | **0%** |

Ranges mean the figure varies by company, not by ATS. Sample: 1,000 Greenhouse rows (2 boards), 155 Lever (2), 275 Ashby (3), 37 Workable (3), 622 Workday (2).

## Five things that surprised us

**1. Salary is a property of the employer, not of the ATS.**
Ashby is the only one of the five that carries structured compensation at all. But across three Ashby boards the fill rate was **96%, 60% and 0%**. Quoting "Ashby returns salary" from a single board is how you end up shipping a promise you cannot keep.

**2. Workday carries the least of the five.**
Its board listing returns a title, a location, a job code, and a *relative* string like "Posted 3 Days Ago". A relative phrase is not a date, so a date field derived from it is a guess. Anything that filters on posted date, department or remote flag will silently drop every Workday row.

**3. Workday is also addressed differently.**
The other four accept a bare board name. Workday needs the full board URL — `https://<tenant>.wd5.myworkdayjobs.com/<Site>` — because the tenant *and* the site name are both part of the address. One request returns at most 500 roles per board.

**4. A board that does not exist and a board with no open roles are different answers.**
`lever:netflix` is not a Lever board at all (404). `workable:aircall` is a real board with zero open roles. Both return "nothing" to a naive client. If you are monitoring hiring activity, collapsing those two into an empty array destroys the signal you came for.

**5. Workable answers 200 for a one-character board name.**
`a` returns a response. `zzqqxxnotarealcompany` returns 404. So a 200 from Workable is not proof that the company you meant exists.

## Getting the data

Public endpoints, no key, no proxy:

| ATS | Endpoint shape |
|---|---|
| Greenhouse | `boards-api.greenhouse.io/v1/boards/<board>/jobs` (plus `/departments` for department names) |
| Lever | `api.lever.co/v0/postings/<board>?mode=json` |
| Ashby | `api.ashbyhq.com/posting-api/job-board/<board>` |
| Workable | `apply.workable.com/api/v1/widget/accounts/<board>` |
| Workday | the tenant's `/wday/cxs/<tenant>/<site>/jobs` POST endpoint |

Lever returns `createdAt` as a UNIX millisecond number; the others use different date shapes. Normalising them to ISO 8601 UTC is most of the work of putting five sources into one table.

## Ready-made version

We maintain these as hosted Actors on Apify, returning all five ATSs in one identical 29-column row shape, where a board with no open roles, a board that does not exist and a failed fetch come back as three *different* rows:

- [ATS Jobs Scraper — Greenhouse, Lever, Ashby, Workable, Workday](https://apify.com/neverempty/ats-jobs-api)
- [ATS Job Board Finder — a company domain to its ATS and board name](https://apify.com/neverempty/ats-board-finder)
- [All of our data tools](https://apify.com/neverempty)



### One Actor per ATS

If you only need one board type, these return the same 29 columns each:

- [Greenhouse Jobs Scraper & API](https://apify.com/neverempty/greenhouse-jobs)
- [Lever Jobs Scraper & API](https://apify.com/neverempty/lever-jobs)
- [Ashby Jobs Scraper & API](https://apify.com/neverempty/ashby-jobs)
- [Workable Jobs Scraper & API](https://apify.com/neverempty/workable-jobs)
- [Workday Jobs Scraper & API](https://apify.com/neverempty/workday-jobs)

## Also in this repository

- [US public data APIs: five ways a 200 does not mean "here is your data"](us-public-data-apis.md) — measured notes on the National Weather Service, NOAA tides, NDBC buoys, USGS and the FAA

## Licence

The notes and figures in this repository are free to use and quote (CC0). Attribution is welcome but not required.
