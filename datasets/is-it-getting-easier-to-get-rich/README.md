# Is It Getting Easier to Get Rich? Wealth, Billionaires and Inequality (1800–2026)

Four linked tables for asking whether wealth is getting easier to build and who holds it. The long-run table (World Inequality Database) covers 12 countries plus the World from 1800/1820 to 2024. It has the wealth shares of the top 0.1%, top 1%, top 10%, middle 40% and bottom 50%, average wealth per adult, how much wealth it takes to enter the top 1% and top 0.1% (in constant 2025 PPP dollars), how many years of average income that top-1% entry ticket is worth, and the household-wealth-to-national-income ratio. A yearly Forbes billionaire table (2000–2026) gives the count and combined net worth, both nominal and inflation-adjusted. A quarterly US Federal Reserve table (1989-Q3 to 2026-Q2) breaks US household net worth down by wealth group. A Maddison Project table of GDP per capita since 1800 (178 countries and regions) shows how average prosperity has changed across the 1800s, 1900s and 2000s.

## Sources

| Source | URL | Retrieved | License |
|---|---|---|---|
| World Inequality Database (WID.world), bulk download (country files US, FR, GB, DE, SE, NL, CN, IN, RU, JP, BR, ZA). Variables `shweal992j`, `ahweal992j`, `thweal992j`, `anninc992i`, `whweal999i`, `xlcusp999i` | https://wid.world/bulk_download/wid_all_data.zip (https://wid.world/data/) | 2026-10-30 | CC BY-NC-SA 4.0 (license badge on wid.world. Our World in Data lists the same data as CC BY 4.0, so the stricter license is used here) |
| World Inequality Database via Our World in Data, "inequality" table, version 2026-06-18 (World row: wealth shares only) | https://catalog.ourworldindata.org/grapher/wid/2026-06-18/world_inequality_database/inequality.feather (chart: https://ourworldindata.org/grapher/wealth-share-richest) | 2026-10-30 | CC BY-NC-SA 4.0 (WID original data), OWID processing CC BY 4.0 |
| Forbes World's Billionaires list, yearly count and combined net worth, from the table "Number and combined net worth of billionaires by year" on Wikipedia | https://en.wikipedia.org/wiki/The_World%27s_Billionaires | 2026-10-30 | CC BY-SA 4.0 (Wikipedia text). Underlying figures: Forbes |
| US Bureau of Labor Statistics, CPI-U all items, US city average, not seasonally adjusted (CUUR0000SA0), March values | https://api.bls.gov/publicAPI/v1/timeseries/data/CUUR0000SA0 | 2026-10-30 | Public domain (US government) |
| Board of Governors of the Federal Reserve System, Distributional Financial Accounts (DFA), net worth by wealth percentile (levels and shares) | https://www.federalreserve.gov/releases/z1/dataviz/download/zips/dfa.zip (https://www.federalreserve.gov/releases/z1/dataviz/dfa/) | 2026-10-30 | Public domain (US government) |
| Bolt & van Zanden, Maddison Project Database 2023, via Our World in Data | https://ourworldindata.org/grapher/gdp-per-capita-maddison-project-database (https://www.rug.nl/ggdc/historicaldevelopment/maddison/releases/maddison-project-database-2023) | 2026-10-30 | CC BY 4.0 |

Attribution: "Source: World Inequality Database (WID.world); Forbes via Wikipedia; US Federal Reserve Distributional Financial Accounts; US BLS; Maddison Project Database 2023 (Bolt & van Zanden); Our World in Data." None of these providers has endorsed this compilation. Because of the WID and Wikipedia licenses, use and share this dataset non-commercially, under the same license (CC BY-NC-SA 4.0), with attribution.

## Files

- `wealth_distribution_long_run.csv`: 1,045 rows (one per country per year), 16 columns. 12 countries plus World. France and Sweden start in 1800, the others in 1820. Data are every 10–30 years before 1900 and mostly annual later (yearly from 1980 for all countries).
- `forbes_billionaires_by_year.csv`: 27 rows (one per year, 2000–2026), 8 columns.
- `us_wealth_distribution_quarterly.csv`: 740 rows (148 quarters × 5 wealth groups), 11 columns. 1989-Q3 to 2026-Q2.
- `gdp_per_capita_long_run.csv`: 17,460 rows (one per country or region per year), 6 columns. 1800–2022, 178 entities (including World and regions, flagged `is_region`).

## Data dictionary

### wealth_distribution_long_run.csv

| Column | Type | Unit | Description |
|---|---|---|---|
| country | string | – | Country name, or "World" |
| country_code | string | – | ISO 3166-1 alpha-3. World = OWID_WRL |
| year | integer | year | Reference year |
| century | string | – | "1800s", "1900s" or "2000s" (calendar years 1800–1899, 1900–1999, 2000+) |
| wealth_share_top_0_1_pct | number | % of total wealth | Share of net personal wealth held by the richest 0.1% of adults |
| wealth_share_top_1_pct | number | % | Share held by the richest 1% |
| wealth_share_top_10_pct | number | % | Share held by the richest 10% |
| wealth_share_middle_40_pct | number | % | Share held by the 50th–90th percentiles |
| wealth_share_bottom_50_pct | number | % | Share held by the poorest 50%. Often close to 0, because their debts are subtracted from their assets |
| avg_wealth_per_adult_usd_ppp_2025 | integer | USD, 2025 prices, PPP | Average net personal wealth per adult (WID `ahweal992j` p0p100 ÷ 2025 PPP factor). Empty for World |
| top_1_pct_wealth_threshold_usd_ppp_2025 | integer | USD, 2025 prices, PPP | Minimum net wealth needed to be in the top 1% (WID `thweal992j` p99p100). Empty for World |
| top_0_1_pct_wealth_threshold_usd_ppp_2025 | integer | USD, 2025 prices, PPP | Minimum net wealth needed to be in the top 0.1% (WID `thweal992j` p99.9p100). Empty for World |
| avg_national_income_per_adult_usd_ppp_2025 | number | USD per year, 2025 prices, PPP | Average national income per adult (WID `anninc992i`). Empty for World |
| top_1_pct_threshold_in_years_of_avg_income | number | years | top_1_pct_wealth_threshold ÷ avg_national_income_per_adult. How many years of the average adult's full income it would take to reach the top 1% (no spending). Higher = harder to get into the top 1% by saving from an average income |
| household_wealth_to_national_income_ratio | number | ratio (× national income) | Net household wealth as a multiple of one year of national income (WID `whweal999i`). 5.8 means wealth equals 5.8 years of national income |
| wid_data_quality_score | integer | 0–5 | WID's per-observation quality score for the top-1% share (higher = more direct source data). 0 generally means the value was imputed, modelled or extrapolated (see caveats). Empty for World |

All WID values use equal-split adults (wealth of couples split equally, adults aged 20+). Monetary values are in constant 2025 local currency converted to US dollars at the 2025 PPP rate (WID `xlcusp999i`).

### forbes_billionaires_by_year.csv

| Column | Type | Unit | Description |
|---|---|---|---|
| year | integer | year | Year of the Forbes list (published each March) |
| billionaires_count | integer | people | Number of US-dollar billionaires on the Forbes list |
| combined_net_worth_usd_trillion | number | USD trillion, nominal | Combined net worth of everyone on the list |
| avg_net_worth_usd_billion | number | USD billion, nominal | combined_net_worth ÷ billionaires_count (calculated) |
| us_cpi_u_march | number | index, 1982–84 = 100 | US CPI-U for March of that year (BLS) |
| combined_net_worth_usd_trillion_2026_dollars | number | USD trillion, March-2026 prices | Combined net worth adjusted for US inflation (× CPI March 2026 ÷ CPI March of year) |
| nominal_1bn_usd_in_2026_usd_bn | number | USD billion, March-2026 prices | What $1 billion in that year is worth in 2026 dollars. Shows how inflation lowers the real bar for "billionaire" (e.g. 1.93 in 2000) |
| billionaires_count_change | integer | people | Change in count from the previous year. Empty for 2000 |

### us_wealth_distribution_quarterly.csv

| Column | Type | Unit | Description |
|---|---|---|---|
| quarter_end_date | date | YYYY-MM-DD | Last day of the quarter |
| year | integer | year | Calendar year |
| quarter | string | – | e.g. 2026-Q2 |
| wealth_group | string | – | US households ranked by net worth: Top 0.1%, Next 0.9% (99-99.9%), Next 9% (90-99%), Next 40% (50-90%), Bottom 50% |
| wealth_group_order | integer | – | 1 = richest group … 5 = Bottom 50% (for sorting) |
| net_worth_usd_million | integer | USD million, nominal | Total net worth (assets − liabilities) of the group |
| net_worth_share_pct | number | % | Group's share of total US household net worth. Groups sum to 100 (±0.1 rounding) |
| assets_usd_million | integer | USD million, nominal | Total assets |
| liabilities_usd_million | integer | USD million, nominal | Total liabilities |
| real_estate_usd_million | integer | USD million, nominal | Real estate assets |
| corporate_equities_and_mutual_funds_usd_million | integer | USD million, nominal | Stocks and mutual fund shares |

### gdp_per_capita_long_run.csv

| Column | Type | Unit | Description |
|---|---|---|---|
| entity | string | – | Country, region or World (Maddison / OWID naming) |
| entity_code | string | – | ISO alpha-3, or OWID_ code for World. Empty for some regions and historical entities |
| year | integer | year | Reference year (1800–2022) |
| century | string | – | "1800s", "1900s" or "2000s" |
| gdp_per_capita_intl_usd_2011 | integer | international $ per person, 2011 prices | GDP per capita adjusted for inflation and living costs |
| is_region | boolean | – | True for World and regional aggregates, or rows with no country code |

## Key figures (from the data)

- Billionaires: 470 in 2000 → 3,428 in 2026 (7.3×). Combined net worth $0.9 trn → $20.1 trn nominal, or $1.7 trn → $20.1 trn in 2026 dollars.
- Top 1% share of world wealth: 46% (1820), 54% (1910), 34% (1980, lowest), 36% (2024). A U-shape: high in the 1800s, a big fall from about 1914 to 1980, then a rise.
- Years of average income needed to reach the US top 1% of wealth: 55 (1900), 38 (1950), 30 (1980), 54 (2024). France: 89 → 21 → 25 → 47. China: 25 (1900), 5 (1980), 59 (2024).
- US (Fed): the top 0.1% held 8.6% of household wealth in 1989-Q3 and 15.0% in 2026-Q2. The bottom 50% went from 3.5% to 2.3%.
- World GDP per capita (2011 int-$): 1,128 (1820) → 2,265 (1900) → 9,904 (2000) → 16,677 (2022).

## Caveats

- Data gaps are left empty. No values were estimated or filled in by this compilation. All calculated columns are marked as such above.
- WID figures before roughly 1900–1950, and for countries with little historical tax data (Brazil, Japan, Russia, South Africa, China and India before 1980), are largely modelled by WID researchers. Their metadata says, for example, that US wealth figures for 1800–1912 and Chinese ones for 1800–1979 were "approximated by imputing" from other variables. 351 of the 989 country rows have `wid_data_quality_score` = 0. The latest years (2022–2024) are often 0 too, because they are nowcasts. Filter on the score for a conservative view.
- WID's World series before 1980 comes at 10–30-year intervals and comes from long-run estimates (Chancel & Piketty). Treat it as an approximate trend, not exact values.
- WID World wealth shares are available via Our World in Data, but World wealth levels and thresholds are not, so those columns are empty for World.
- Forbes counts start in 2000 in the source table used. Earlier yearly counts were not available in a source this compilation could redistribute. Forbes estimates are snapshots taken in March, rely on asset prices (stock market swings move the count a lot, e.g. 2009 and 2021), and Forbes has widened its coverage over time.
- No reliable yearly global millionaire count is published under an open license (the UBS Global Wealth Report and the Capgemini World Wealth Report are proprietary), so millionaire counts are not included. The WID top-1% and top-0.1% thresholds are the open alternative for "how rich is rich".
- The real billionaire values use the US CPI. Most billionaires are not American, so this is a dollar-inflation adjustment, not a local cost-of-living adjustment.
- Fed DFA values are nominal US dollars and cover only US households. DFA is based on the Survey of Consumer Finances plus Financial Accounts and is revised every quarter.
- Maddison values before 1950 are sparse for many countries and are historical reconstructions. The 2011 international-dollar prices in the GDP file differ from the 2025 PPP dollars in the WID file, so don't mix the two units in one calculation.
- "Easier to get rich" can be read several ways. This dataset supports three views: absolute (real wealth and GDP levels rising), relative (the top-1% threshold measured in years of income) and concentration (shares held by the top groups). They don't always agree.

## Dashboard ideas

- U-curve line chart: World and country top 1% wealth shares 1820–2024, with shading for the 1800s, 1900s and 2000s.
- "Ticket to the top 1%": years of average income needed, by country and decade. Shows the cheap mid-century period and today's rise.
- Billionaire boom: count bars plus a line for combined wealth, nominal vs 2026 dollars, with 2009 and 2021 annotated.
- Inflation lowers the bar: `nominal_1bn_usd_in_2026_usd_bn` over time next to the count.
- US wealth pie over time: stacked area of the five Fed wealth groups' shares by quarter, 1989–2026.
- Bottom 50% vs top 1%: slope chart per country, 1900 → 1980 → 2024.
- Richer world, unequal split: world GDP per capita (log scale) next to the world top 10% share, by century.
- Wealth vs income: `household_wealth_to_national_income_ratio` 1800/1820–2024 for France, the UK and the US (Piketty's "capital is back").
