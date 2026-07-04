# SkyPulse — Beating Delays Before They Start

A real-time flight difficulty detection framework that quantifies flight operational complexity at Chicago O'Hare (ORD) to enable proactive resource planning.


## Business Problem

Certain flights are operationally complex due to tight ground times, high baggage volumes, and specific passenger needs, making on-time departures difficult. Identifying these flights today relies on manual experience — inconsistent and not scalable. This project builds a systematic, data-driven **Flight Difficulty Score** to quantify flight complexity and support proactive staffing and scheduling decisions.

## Approach

1. **Data Cleaning & Preparation** — standardized and cleaned five source datasets (flights, bags, PNR remarks, PNR flights, airports): removed 293 duplicate baggage records, corrected data types, standardized categorical fields.
2. **Exploratory Data Analysis** — identified the operational factors most correlated with delays.
3. **Feature Engineering** — built features such as *Ground Time Pressure* and *Baggage Complexity Ratio*.
4. **Difficulty Score Development** — a daily, weighted scoring model (MinMax-normalized, weighted by EDA-derived importance) that ranks and classifies every flight as **Easy**, **Medium**, or **Difficult**.
5. **Post-Analysis & Recommendations** — traced high-risk destinations back to their root operational drivers.

## Key Findings

- **Delays are frequent**: 49.6% of flights depart late, averaging a 47-minute delay.
- **Tight turnarounds are common**: 8.05% of flights are scheduled with ground time at or below the minimum turn requirement.
- **Load factor isn't the driver**: passenger load factor shows almost no correlation with delay (r = -0.15).
- **Special Service Requests matter**: flights with high SSR volume show meaningfully higher delays than low-SSR flights, independent of how full the flight is.
- A small number of destinations account for a disproportionate share of "Difficult" flights, driven by ground time pressure, SSR volume, and baggage complexity.

## Recommendations

1. Pre-allocate extra gate agents for "Difficult" flights to high-risk airports (e.g. IAH, SFO).
2. Auto-flag "Difficult" flights in the baggage system to prep transfer crews for high "Hot Transfer" bag volume.
3. Add a 10–15 minute ground-time buffer for consistently high-ranked flights.
4. Hold a daily pre-flight "Difficulty Huddle" for the top 3–5 flagged flights.
5. Review all schedules that fall below minimum turn time + buffer.
6. Push key complexity metrics to gate crew information displays.

## Repo Contents

| File | Description |
|---|---|
| `Skyhack3_0.ipynb` | Data cleaning, EDA, feature engineering, and difficulty scoring model |
| `SkyPulse.pptx` | Final presentation of problem, methodology, findings, and recommendations |
| `Airports Data.xlsx` | Source data — airport reference info |
| `Flight Level Data.xlsx` | Source data — flight schedules and ground times |
| `Bag+Level+Data.xlsx` | Source data — baggage records |
| `PNR+Flight+Level+Data.xlsx` | Source data — passenger bookings |
| `PNR Remark Level Data.xlsx` | Source data — SSR remarks |
| `test_neutrinos.csv` | Final output — per-flight Difficulty Score and classification |

## Tech Stack

Python · pandas · numpy · scikit-learn (MinMaxScaler) · matplotlib · seaborn

## Data

The five original source files are included in this repo:

| File | Contents |
|---|---|
| `Airports Data.xlsx` | Airport reference data |
| `Flight Level Data.xlsx` | Scheduled/actual flight times, ground times, load factors |
| `Bag+Level+Data.xlsx` | Baggage-level records (checked, transfer, hot transfer) |
| `PNR+Flight+Level+Data.xlsx` | Passenger booking data joined to flights |
| `PNR Remark Level Data.xlsx` | Special Service Request (SSR) remarks per passenger |

`test_neutrinos.csv` contains the final output — each flight's computed Flight Difficulty Score and Easy/Medium/Difficult classification.

## Running the Notebook

```bash
pip install pandas numpy matplotlib seaborn scikit-learn
jupyter notebook Skyhack3_0.ipynb
```

## License

MIT — see [LICENSE](LICENSE).
