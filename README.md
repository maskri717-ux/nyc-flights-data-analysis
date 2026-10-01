# NYC Flights Data Analysis

An exploration of flight delays across New York City's three major airports. This project combines data quality checks, operational comparisons, and visual reporting to show how delay patterns vary and why a single average can miss part of the story.

[Read the full report](analysis_v2.html) | [View the Quarto source](analysis_v2.qmd)

## Main analytical question

What factors are associated with departure and arrival delays for NYC flights in 2013, and how does performance vary across airlines, airports, routes, time, season, and weather conditions?

## Dataset

The `nycflights13` package provides **336,776 flight records** for 2013 departures from JFK, LaGuardia (LGA), and Newark (EWR). Flight records include schedules, observed delays, carriers, destinations, and distances. Airline and airport lookup tables add context, while hourly weather observations support precipitation and visibility comparisons. The package identifies the Bureau of Transportation Statistics as the flight data source.

## Key findings

All findings below come from `analysis_v2.qmd`. Delay percentages use flights with recorded departure delays; weather comparisons also require the relevant weather measure.

- **Averages hide the typical experience.** The median departure was 2 minutes early, but the mean delay was 12.6 minutes and 22.2% of observed departures were at least 15 minutes late.
- **Later scheduled departures had higher delay shares.** The share delayed 15+ minutes rose from 9.4% in early morning to 36.1% late at night.
- **Airport comparisons depend on the metric.** LGA had the lowest 15+ minute departure-delay share at 19.5%, but the highest share of scheduled flights with no recorded departure at 3.01%.
- **Route detail matters.** For flights to Chicago O'Hare, the 15+ minute departure-delay share was 30.9% from JFK versus 19.6% from LGA.
- **Weather conditions were associated with different outcomes.** The 15+ minute departure-delay share was 40.0% with recorded precipitation versus 21.0% without it.

## Methodology

- Audit missing values and preserve original records, missing outcomes, and extreme delays.
- Compare means, medians, percentiles, and 15+ and 60+ minute delay shares across operational groups, using explicit denominators.
- Apply minimum observed-departure sample sizes for rankings: 1,000 for airlines and routes, and 500 for destinations.
- Join weather by departure airport, date, and scheduled local departure hour, checking key uniqueness and row preservation.
- Validate summary counts, categories, and percentage ranges with programmatic checks; present results in reproducible tables and charts.

## Tools used

**R**, **tidyverse** (including dplyr, tidyr, and ggplot2), **nycflights13**, **lubridate**, **scales**, and **knitr**; **Quarto**, HTML, and CSS for report presentation.

## Important limitations

- Results describe NYC departures in 2013, not current performance. Comparisons do not isolate causal effects or adjust for overlapping airline, route, schedule, and weather differences.
- Missing departure times serve only as a cancellation proxy, not confirmed cancellations. Departure and arrival summaries use different available samples.
- Weather reflects the scheduled departure hour, with some unmatched records, rather than conditions throughout the flight. Wind speed is excluded because of a source-data quality issue.
- Some destination names are missing from the airport lookup; those flights remain in the analysis under their airport codes.

## Intended repository structure

```text
nyc-flights-data-analysis/
|-- README.md
|-- analysis_v2.qmd
|-- analysis_v2.html
|-- styles.css
`-- analysis_v2_files/
```
