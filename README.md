# IPL Historical Performance Dashboard

An interactive **Tableau** dashboard that analyses **260,000+ ball-by-ball records** from Indian Premier League (IPL) matches to uncover player, team, and match-level insights.

![Dashboard Preview](dashboard.png)

---

## Overview

The dataset combines **match-level data** (venue, toss, winner, player of the match) with **ball-by-ball delivery data** (batter, bowler, runs, wickets). The two sources were cleaned and merged on `match_id` into a single dataset, `IPL_Cleaned_Merged_Data.csv`, with **36 columns**.

**Granularity:** each row represents **one ball bowled**.

---

## Dashboard Contents

The dashboard contains **13 linked views**:

| Type | Views |
|---|---|
| **KPI Cards** | Total Matches, Total Runs, Total Wickets |
| **Trends** | Runs per Season, Scoring Trend by Over |
| **Rankings** | Top 10 Batsmen, Top 10 Wicket-Taking Bowlers, Top Player of the Match, Top Venues, Matches Won by Team |
| **Breakdowns** | Toss Decisions, Types of Dismissals |
| **Analysis** | Batter Run Rate Analysis (runs vs. balls faced) |

**Interactivity:** selecting a **season** filters every view on the dashboard through a Tableau filter action.

---

## Calculated KPIs

| KPI | Formula (Tableau) |
|---|---|
| Total Matches | `COUNTD([match_id])` |
| Total Balls | `COUNT([ball])` |
| Strike Rate | `SUM([batsman_runs]) / COUNT([ball]) * 100` |
| Batting Average | `SUM([batsman_runs]) / number of dismissals` |
| Economy Rate | `SUM([total_runs]) / (COUNT([ball]) / 6)` |
| Boundary % | Runs from 4s and 6s / total batsman runs * 100 |
| Toss Win % | Matches where the toss winner also won / total matches |

`COUNTD` (count distinct) is used for matches because each match appears once for every ball bowled.

---

## Data Preparation

- Merged match-level and ball-by-ball data on `match_id`
- Handled missing values (e.g. `dismissal_kind` = "NA" when no wicket fell)
- Standardised inconsistent entries such as team and venue names
- Set correct data types for dates, runs, and identifiers

---

## Tech Stack

- **Python**: data cleaning and merging
- **Tableau**: calculated fields, dashboard design, filter actions

---

## How to Open

1. Install [Tableau Public](https://public.tableau.com/) (free) or Tableau Desktop.
2. Download an IPL ball-by-ball dataset and save it as `IPL_Cleaned_Merged_Data.csv`.
3. Open `IPL Historical Performance Dashboard.twb` and point the data source to the CSV.

---

## Future Improvements

- **Toss Win %** at match level: count distinct matches instead of balls, so long matches don't carry extra weight.
- **Bowler wickets**: exclude run-outs and retired-hurt dismissals, which are not credited to the bowler.
- **Strike rate**: exclude wides from balls faced.
- Rebuild the dashboard in **Power BI** with DAX measures.
