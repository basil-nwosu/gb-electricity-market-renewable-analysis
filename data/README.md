# Data & Methodology

## Data Sources

This project combines publicly available electricity-market data from two primary sources:

- **NESO (National Energy System Operator)** – electricity demand, embedded wind generation, embedded solar generation and related GB electricity-system variables.
- **Elexon** – Market Index Price (MIP) and associated market-volume data.

The analysis covers **1 January to 27 August 2026**.

## Dataset Integration

The NESO and Elexon datasets were cleaned and transformed using **Power Query**.

The datasets were joined at settlement-period level using:

- `SETTLEMENT_DATE`
- `SETTLEMENT_PERIOD`

A **Left Outer Join** was used with the NESO demand dataset as the primary table.

The resulting analytical dataset contains approximately **11,470 half-hourly settlement-period observations**.

## Key Variables

### National Demand

`ND`

National electricity demand reported in the NESO dataset.

### Embedded Wind Generation

`EMBEDDED_WIND_GENERATION`

Estimated electricity generation from embedded wind capacity connected to distribution networks.

### Embedded Solar Generation

`EMBEDDED_SOLAR_GENERATION`

Estimated electricity generation from embedded solar capacity connected to distribution networks.

### Embedded Renewable Generation

A calculated variable combining embedded wind and solar generation:

`Embedded Renewable Generation = Embedded Wind Generation + Embedded Solar Generation`

### Embedded Renewable Penetration

Calculated as:

`Embedded Renewable Penetration = Embedded Renewable Generation / National Demand`

This measures embedded wind and solar generation relative to National Demand for each settlement period.

> **Important limitation:** This metric represents embedded wind and solar generation only. It should not be interpreted as total renewable generation or the total renewable share of electricity supplied in Great Britain.

### Market Index Price

`MARKET_INDEX_PRICE`

Market Index Price data obtained from Elexon and expressed in **£/MWh**.

Where required during data preparation, Market Index Price was calculated using volume-weighted price information.

### Negative Price Flag

Settlement periods were classified as negative-price periods when:

`MARKET_INDEX_PRICE < 0`

This variable was used to calculate the frequency of negative prices across renewable-penetration bands.

## Renewable Penetration Bands

Settlement periods were grouped into the following embedded renewable penetration bands:

- 0–10%
- 10–20%
- 20–30%
- 30–40%
- 40–50%
- 50–60%
- 60–70%
- 70–80%
- 80–90%
- 90–100%
- ≥100%

These bands were used to compare average Market Index Prices and negative-price frequency under different levels of embedded renewable generation.

## Analytical Workflow

The project followed the workflow:

**Raw data → Power Query cleaning and transformation → Dataset integration → Calculated variables → Exploratory analysis → Power BI modelling → DAX measures → Interactive dashboard → Market insights**

Key preparation steps included:

- Standardising date and settlement-period fields
- Checking and assigning appropriate data types
- Combining NESO and Elexon data
- Calculating embedded renewable generation
- Calculating embedded renewable penetration
- Creating renewable penetration bands
- Identifying negative-price settlement periods
- Creating time and datetime fields for temporal analysis
- Validating key price and renewable-generation observations

## Power BI Measures

The Power BI report includes measures for:

- Average Market Index Price
- Maximum Market Index Price
- Minimum Market Index Price
- Average embedded renewable penetration
- Negative-price frequency

The dashboard also includes an interactive date slicer, allowing the analysis period and associated KPIs to be filtered dynamically.

## Methodological Limitations

The analysis identifies **associations rather than causal relationships**.

Electricity prices are affected by multiple interacting factors beyond embedded renewable generation, including:

- Electricity demand
- Conventional generation availability
- Interconnector flows
- Storage
- System constraints
- Weather conditions
- Wider balancing and market conditions

Therefore, the observed relationship between higher embedded renewable penetration and lower or negative Market Index Prices should not be interpreted as evidence that renewable generation alone causes these price outcomes.
