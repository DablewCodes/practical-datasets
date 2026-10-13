# Minimum Wage vs Living Cost Around the World (2010–2026)

Statutory monthly minimum wages for 175 countries and territories, 2010–2026, from the ILO, in local currency, US dollars (market exchange rates) and PPP international dollars. Each wage sits next to cost-of-living benchmarks from the World Bank: the daily cost of a healthy diet, household consumption per person, price levels relative to the US, inflation, GDP per capita and ILO mean earnings. Ready-made ratios show how far a minimum wage goes in each country, for example how many people's healthy diets one minimum-wage salary can pay for. There is one row per country per year.

## Sources

| Source | URL | Retrieved | License |
|---|---|---|---|
| ILO, ILOSTAT: Statutory nominal gross monthly minimum wage by currency (`DF_EAR_INEE_CUR_NB`) | https://sdmx.ilo.org/rest/data/ILO,DF_EAR_INEE_CUR_NB/all | 2026-10-13 | CC BY 4.0 ([ILO rights and permissions](https://www.ilo.org/node/9321)) |
| ILO, ILOSTAT: Average monthly earnings of employees, USD (`DF_EAR_EMTA_SEX_CUR_NB`, total sex) | https://sdmx.ilo.org/rest/data/ILO,DF_EAR_EMTA_SEX_CUR_NB/ | 2026-10-13 | CC BY 4.0 |
| World Bank, World Development Indicators (PA.NUS.FCRF, PA.NUS.PRVT.PP, FP.CPI.TOTL.ZG, NY.GDP.PCAP.CD, NE.CON.PRVT.CD, SP.POP.TOTL), last updated 2026-10-08 | https://api.worldbank.org/v2/ (https://databank.worldbank.org/source/world-development-indicators) | 2026-10-13 | CC BY 4.0 |
| World Bank, Food Prices for Nutrition DataHub, FPN 5.0 (CoHD_PPP, CoHD_headcount), last updated 2026-07-21 | https://api.worldbank.org/v2/sources/88 (https://datacatalog.worldbank.org/search/dataset/0061222) | 2026-10-13 | CC BY 4.0 |
| World Bank country classifications (region, income group) | https://api.worldbank.org/v2/country | 2026-10-13 | CC BY 4.0 |

Attribution: "Source: ILO, ILOSTAT; World Bank, World Development Indicators and Food Prices for Nutrition." The ILO and the World Bank have not endorsed this compilation.

## File

`minimum_wage_vs_living_cost.csv`: 2,476 rows, 31 columns, 175 countries and territories, years 2010–2026. 167 rows are flagged `is_latest_complete_year = true` (one per country).

## Data dictionary

| Column | Type | Unit | Description |
|---|---|---|---|
| country_name | string | – | Country name (World Bank naming) |
| iso3_code | string | – | ISO 3166-1 alpha-3 code |
| region | string | – | World Bank region |
| income_group | string | – | World Bank income group. "Not classified" for Cook Islands, Jersey and Taiwan, China (regions assigned by geography) |
| year | integer | year | Reference year. The ILO reports the minimum wage in force at 31 December of that year |
| minimum_wage_type | string | – | ILO type, e.g. "Singular national minimum wage", "Occupational (unskilled workers)", "Regional" |
| ilo_monthly_conversion_note | string | – | How the ILO converted hourly or daily rates to monthly figures (e.g. hourly × 40 h × 4.33 weeks) |
| currency_code | string | ISO 4217 | Currency of `min_wage_monthly_lcu` |
| currency_name | string | – | Currency name |
| min_wage_monthly_lcu | number | local currency per month | Gross statutory minimum wage (ILO) |
| min_wage_monthly_usd | number | USD per month | Minimum wage at market exchange rates (ILO) |
| min_wage_monthly_ppp_intl_usd | number | international $ per month | Minimum wage at PPP for private consumption (ILO). Use for comparing purchasing power |
| exchange_rate_lcu_per_usd | number | LCU per USD | Official exchange rate, annual average (World Bank PA.NUS.FCRF) |
| ppp_factor_lcu_per_intl_usd | number | LCU per intl $ | PPP conversion factor, household consumption (World Bank PA.NUS.PRVT.PP) |
| price_level_index_usa_100 | number | index, USA = 100 | Consumer price level relative to the US, calculated as min_wage_monthly_usd ÷ min_wage_monthly_ppp_intl_usd × 100. Below 100 means cheaper than the US |
| inflation_cpi_pct | number | % per year | Consumer price inflation (World Bank FP.CPI.TOTL.ZG) |
| gdp_per_capita_usd | number | USD per year | GDP per capita, current USD (World Bank) |
| household_consumption_per_capita_monthly_usd | number | USD per person per month | Household final consumption expenditure (current USD) ÷ population ÷ 12. Average spending per person |
| healthy_diet_cost_daily_ppp_intl_usd | number | intl $ per person per day | Cost of the cheapest locally available healthy diet (2,330 kcal) (World Bank FPN, CoHD_PPP) |
| healthy_diet_cost_monthly_ppp_intl_usd | number | intl $ per person per month | Daily cost × 365 ÷ 12 |
| healthy_diet_cost_monthly_usd | number | USD per person per month | Monthly PPP cost × price_level_index_usa_100 ÷ 100 |
| pop_unable_to_afford_healthy_diet_pct | number | % of population | Share of people who cannot afford a healthy diet (World Bank FPN, CoHD_headcount) |
| mean_monthly_earnings_usd | number | USD per month | Mean monthly earnings of all employees, survey-based (ILO) |
| mean_earnings_source | string | – | Survey behind the mean earnings figure |
| min_wage_to_healthy_diet_ratio | number | ratio | Number of people whose healthy diet one monthly minimum wage can pay for (PPP ÷ PPP). Below 1 means it can't cover one person's healthy diet |
| min_wage_to_household_consumption_pct | number | % | Monthly minimum wage as a % of average household spending per person per month (USD ÷ USD) |
| min_wage_to_mean_earnings_pct | number | % | Minimum wage as a % of mean earnings (USD ÷ USD) |
| min_wage_annual_to_gdp_per_capita_pct | number | % | Minimum wage × 12 as a % of GDP per capita |
| min_wage_source | string | – | ILO's source type for the minimum wage (e.g. "ADM - Labour legislation") |
| data_note | string | – | Data-quality note when a value was removed or needs care (72 rows) |
| is_latest_complete_year | boolean | – | True for each country's latest year that has both a USD minimum wage and GDP per capita. Use as a filter for map or snapshot views |

## Caveats

- Data gaps are left empty. No values were estimated or filled in.
- Countries where minimum wages come only from collective bargaining (e.g. Denmark, Sweden, Norway, Finland, Italy, Austria) are not in the ILO series. Where a country sets minimum wages by region or sector, the ILO uses the capital city, manufacturing or unskilled rate (e.g. Switzerland, India, Pakistan, China). See `minimum_wage_type`.
- Some legal minimums are decades old and far below real pay (e.g. Burundi, Rwanda, Uganda before 2017, Georgia's 20 GEL). Statutory amounts don't show what people actually earn.
- Rates set per hour or per day were converted to monthly figures by the ILO under fixed assumptions (see `ilo_monthly_conversion_note`).
- For 2025–2026 the ILO often gives only local-currency values, and World Bank data for 2025 is incomplete. 2024 is the most complete year.
- Values removed as clear source errors (flagged in `data_note`):
  - Cambodia: ILO treats the USD-denominated wage as riel, so its USD and PPP conversions were removed.
  - Ecuador 2024 and Uruguay 2024: ILO values are about 1/12 of 2023.
  - Serbia 2010–2012: the PPP value is off.
  - Venezuela 2010–2011: household consumption is implausible.
- For euro adopters (Bulgaria, Croatia, Estonia, Latvia, Lithuania) and Liberia, the ILO local-currency value and the World Bank exchange or PPP rate are in different units in some years. Those World Bank rates were left empty. The USD and PPP columns are still valid.
- The healthy-diet cost covers food for one person only, not rent, transport or dependants. Read `min_wage_to_healthy_diet_ratio` as a minimum benchmark, not a living wage. Household consumption per capita is an average across the whole population.
- Mean earnings come from different surveys in different countries and can include part-time and low-paid workers, so ratios above 100% can occur (e.g. Indonesia, Honduras).
- Currency redenominations (Belarus 2016, Sierra Leone 2022, Venezuela 2018/2021) cause jumps in local-currency values. Use the USD or PPP columns for trends.

## Dashboard ideas

- World map of `min_wage_monthly_usd` vs `min_wage_monthly_ppp_intl_usd` (filter `is_latest_complete_year`), with a toggle showing how much PPP changes the ranking.
- "How many healthy diets does a minimum wage buy?": a bar chart of `min_wage_to_healthy_diet_ratio`, coloured by income group.
- Scatter of minimum wage (PPP) against GDP per capita, sized by `pop_unable_to_afford_healthy_diet_pct`.
- Trend lines of real purchasing power over 2010–2024, using PPP wages or local-currency wages deflated by `inflation_cpi_pct`.
- Region comparison of `min_wage_to_household_consumption_pct` and `min_wage_to_mean_earnings_pct` (how binding the minimum wage is).
