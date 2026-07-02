# Quantifying Demographic Impacts on Climate Change: A Longitudinal Analysis of Global CO2 Emissions

### [View the Interactive Project Report Live Here](https://emmilymandell.github.io/co2-population-analysis/)

## Project Overview
This project investigates the longitudinal, macroeconomic relationship between national population growth dynamics and changes in annual carbon dioxide ($CO_2$) emissions across 180 countries from 1961 to 2022. By integrating macro datasets from the World Bank and the Global Carbon Budget, we built a log-log linear regression model to quantify the scaling elasticity between demographic growth rates and national carbon load.

The core objective of this study is to move past naive, absolute trends and provide a statistically rigorous baseline of environmental loading driven strictly by demographic shifts.

## Key Findings & Structural Insights
* Emission Elasticity ($\beta_1$): Our model estimates a coefficient of 0.646. In a log-log framework using first-differenced data, this indicates an elasticity of annual scaling: a 1% increase in the magnitude of a nation's annual population growth corresponds to an approximate 0.646% increase in the magnitude of their annual $CO_2$ emissions.
* Model Explanatory Power ($R^2$): The model yields an Adjusted $R^2$ of 0.383. This indicates that 38.3% of the variance in positive year-over-year $CO_2$ changes can be explained structurally by shifts in annual population growth. While significant variance remains unexplained due to omitted macroeconomic factors, ~38% represents a remarkably robust baseline for a single-variable model on noisy global panel data.
* Statistical Significance: The coefficient rejected the null hypothesis with extreme significance ($t = 64.42$, $p < 2.2 \times 10^{-16}$), validating the strong positive link between demographic acceleration and emissions scaling.

## Data Infrastructure & Feature Engineering
The project constructs an automated data-joining and preprocessing pipeline utilizing two open-source foundational datasets:
1. World Bank Population Indices: Annual national census data mapping total population metrics.
2. Our World in Data (Global Carbon Budget): Annual metrics tracking metric tonnes of industrial and fossil-fuel-based $CO_2$ output.

### Feature Engineering Pipeline:
To circumvent spurious correlation common in absolute time-series data (where variables trend upward simply due to the passage of time), the pipeline transitions raw metrics into absolute first-differences ($\Delta$) isolated sequentially within country groups:

$$\Delta \text{Population} = \text{Population}_t - \text{Population}_{t-1}$$

$$\Delta \text{CO}_2\text{ Emissions} = \text{CO}_{2, t} - \text{CO}_{2, t-1}$$

To linearize the relationship for OLS modeling and stabilize variance across vastly different country scales (e.g., China vs. small island nations), a $\log_{10}$ transformation was applied to observations displaying positive growth.

## Tech Stack & Analytical Ecosystem
* Language: R (v4.3+)
* Primary Libraries: 
  * `tidyverse` (Data manipulation, advanced reshaping, and group-nested parsing)
  * `ggplot2` (Custom thematic visualizations utilizing log scales)
  * `broom` (Tidying complex linear model statistics into analytic dataframes)
  * `scales` (Formatting plotting axes into readable comma metrics)

## How to Reproduce this Analysis
To clone this repository and reproduce the statistical summaries locally:

1. Clone the repository:
   ```bash
   git clone [https://github.com/emmilymandell/co2-population-analysis.git](https://github.com/emmilymandell/co2-population-analysis.git)