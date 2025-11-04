# Morocco Tourism — 2012–2020 (Power BI)

Tracks **Total Arrivals** and **Total Nights** with breakdowns by **nationality** and **province**, plus a map.

## Model & approach
- **Star Schema:**
  - `FactTourism(Nights, Arrivals, DateKey, MarketKey, ProvinceKey)`
  - `DimMarket(Nationality, RegionGroup)`
  - `DimProvince(ProvinceName, Geo)`
  - `Calendar(Date, Year)` — **marked as Date table** for time intelligence (YoY).

## Example DAX
```DAX
Total Arrivals := SUM(FactTourism[Arrivals])
Total Nights   := SUM(FactTourism[Nights])
Arrivals LY    := CALCULATE([Total Arrivals], SAMEPERIODLASTYEAR('Calendar'[Date]))
Arrivals YoY % := DIVIDE([Total Arrivals] - [Arrivals LY], [Arrivals LY])
