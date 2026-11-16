# Running Participation vs House Prices, English Councils (2016–2025)

This dataset covers how many adults run or jog in each of England's 296 local authorities (councils), alongside house prices, household income and population density. It is built to test whether areas where more people run have higher house prices. The running and activity rates are from Sport England's Active Lives Adult Survey: the share of adults aged 16+ who took part at least twice in the last 28 days, for each survey year from Nov 2015–Nov 2016 to Nov 2024–Nov 2025. House prices are the HM Land Registry UK House Price Index, averaged over the same Nov–Oct months as each survey year. Income is ONS gross disposable household income (GDHI) per head, and population and density are ONS mid-year estimates. There are two files: a yearly panel and a one-row-per-council snapshot that pools the last three survey years.

## Sources

| Source | URL | Retrieved | License |
|---|---|---|---|
| Sport England, Active Lives Online, Adult survey: participation at least twice in last 28 days, activities "Running (including jogging and treadmill)" (id 90), "Running or jogging" (id 177), "All sport and physical activity" (id 1), 296 local authorities, Nov 15-16 to Nov 24-25 | https://activelives.sportengland.org/ | 2026-11-16 | © Sport England. Republished here with Sport England's permission (granted November 2026). Not an open licence: for any other reuse, see https://activelives.sportengland.org/Home/TermsAndConditions or contact Sport England |
| HM Land Registry, UK House Price Index full file (Aug 2026 release) | https://publicdata.landregistry.gov.uk/market-trend-data/house-price-index-data/UK-HPI-full-file-2026-08.csv | 2026-11-16 | Open Government Licence v3.0 |
| ONS, Regional gross disposable household income: local authorities, 1997–2024 (Table 3) | https://www.ons.gov.uk/economy/regionalaccounts/grossdisposablehouseholdincome/datasets/regionalgrossdisposablehouseholdincomelocalauthorities | 2026-11-16 | Open Government Licence v3.0 |
| ONS, Population estimates for England and Wales mid-2025, 2023 boundaries (MYE5 population density) | https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/estimatesofthepopulationforenglandandwales | 2026-11-16 | Open Government Licence v3.0 |

Attribution: "Source: Sport England, Active Lives Adult Survey (via Active Lives Online); HM Land Registry UK House Price Index; ONS." Contains HM Land Registry and ONS data © Crown copyright and database right 2026, licensed under the Open Government Licence v3.0. Sport England has not endorsed this compilation.

## Files

- `running_vs_house_prices_by_council_yearly.csv`: 2,960 rows, one per council per survey year (296 × 10).
- `running_vs_house_prices_by_council_latest.csv`: 296 rows, one per council. Running rates are pooled over Nov 2022 – Nov 2025. Prices are for Nov 2024 – Oct 2025, and income is for 2024.

## Data dictionary (yearly file)

| Column | Type | Unit | Description |
|---|---|---|---|
| la_code | string | – | ONS local authority district code (2023 boundaries) |
| la_name | string | – | Local authority name (ONS) |
| region | string | – | ITL1 region / English region (from ONS GDHI file) |
| survey_year_end | integer | year | Year the survey period ends (Nov to Nov), e.g. 2025 = Nov 2024 – Nov 2025 |
| survey_period | string | – | Survey period label |
| respondents | integer | people | Survey respondents in the council that year |
| running_incl_treadmill_pct | number | % of adults 16+ | Took part in running (incl. jogging and treadmill) at least twice in last 28 days. **Main jogging measure** |
| running_incl_treadmill_moe_pct_points | number | percentage points | Approximate 95% margin of error: 1.96 × √(p(1−p)/respondents). Ignores survey weighting, so it is a rough guide |
| running_jogging_pct | number | % of adults 16+ | Running or jogging outdoors only (narrower measure; more suppressed values) |
| any_sport_activity_pct | number | % of adults 16+ | Any sport or physical activity at least twice in last 28 days. Use as a general activity control |
| running_incl_treadmill_adults | integer | people | Sport England weighted population estimate of adults running |
| running_jogging_adults | integer | people | Same for running or jogging |
| any_sport_activity_adults | integer | people | Same for any sport or activity |
| avg_house_price_gbp | integer | GBP | UK HPI average (mix-adjusted) price, mean of the 12 monthly values Nov (year−1) to Oct (year) |
| detached_avg_price_gbp | integer | GBP | Same, detached houses |
| semi_detached_avg_price_gbp | integer | GBP | Same, semi-detached houses |
| terraced_avg_price_gbp | integer | GBP | Same, terraced houses |
| flat_avg_price_gbp | integer | GBP | Same, flats and maisonettes |
| gdhi_per_head_gbp | integer | GBP per person per year | ONS GDHI per head for calendar year = survey_year_end. Empty for 2025 (not yet published) |
| price_to_income_ratio | number | ratio | avg_house_price_gbp ÷ gdhi_per_head_gbp |
| population | integer | people | ONS mid-year population estimate (mid-year of survey_year_end) |
| area_km2 | number | km² | Land area |
| population_density_per_km2 | integer | people per km² | ONS population density |

## Data dictionary (latest file; columns not described above)

| Column | Type | Unit | Description |
|---|---|---|---|
| respondents_3yr | integer | people | Respondents summed over 2023–2025 survey years |
| running_incl_treadmill_pct_3yr | number | % of adults 16+ | Respondent-weighted mean of the three yearly rates |
| running_jogging_pct_3yr | number | % | Same for running or jogging |
| any_sport_activity_pct_3yr | number | % | Same for any sport or activity |
| running_incl_treadmill_moe_pct_points_3yr | number | percentage points | Approximate 95% margin of error for the pooled rate |
| running_share_of_active_pct | number | % | Runners as a share of active adults (running ÷ any activity × 100). Separates "a running area" from "an active area" |
| running_quintile | integer | 1–5 | Quintile of running_incl_treadmill_pct_3yr across councils (5 = most running) |
| house prices, population, density | – | – | Survey year 2025 values (Nov 2024 – Oct 2025 prices; mid-2025 population) |
| gdhi_per_head_gbp | integer | GBP | 2024 (latest available) |

## Caveats

- These are council-wide averages, not neighbourhoods. A council can contain both rich and poor areas. This is an ecological comparison: it can't show that runners live in pricier homes.
- Correlation is not causation. Income drives both running and house prices. Control for gdhi_per_head_gbp, density, region and any_sport_activity_pct.
- Most councils have only ~400–500 respondents a year, so single-year rates move by ±3 points. Use the 3-year pooled file for comparisons between councils.
- Sport England suppresses small counts (shown as empty): 23 council-years for running incl. treadmill, 170 for running or jogging. Isles of Scilly has no running rate and no UK HPI prices.
- 2020-21 survey years overlap COVID lockdowns, when running rose and other activities fell.
- UK HPI uses 2021 codes for Barnsley and Sheffield (E08000038/39). These were mapped to the 2023 codes E08000016/19. Recent months of UK HPI are revised for a few months after release.
- The margins of error are approximations and don't use Sport England's design weights.

## Quick check (latest file, 295 councils)

- Median average house price by running quintile, from lowest to highest running: £204k, £276k, £287k, £341k, £482k.
- Without controls, each +1 point of running goes with about 8.5% higher prices. After controlling for income, density, overall activity and region, it's about 2.2% per point (t ≈ 5.6). The link shrinks a lot but doesn't disappear.

## Dashboard ideas

- Scatter of running rate vs average house price, coloured by region, sized by population, with a trend line. Add a filter on income band to see if the link holds within similar-income councils.
- Bar chart of median price by running quintile, plus a second panel for price-to-income ratio.
- Map of England councils (ONS LAD codes join to ONS boundary files) with running rate and price side by side.
- Yearly panel: running rate over time for the top and bottom 10 councils by house price, with the 2020-21 COVID years marked.
- "Over- and under-performers": councils with high running but low prices, or the reverse (residuals from a price ~ income model).
