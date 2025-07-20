****Solution**: Spotfire Dashboard for COVID-19, US Census, and Open Weather Data**

Objective

Spotfire dashboard that integrates COVID-19 data, US Census data, and Weather data to analyze relationships between demographic, health, and environmental factors over time and across different states.
________________________________________
**Data Sources**
1.	COVID-19 Data:
o	Metrics: Daily cases, deaths, vaccination rates.
o	Source: CDC COVID Data Tracker.
o	Granularity: State and county level (2020–2023).
2.	US Census Data:
o	Metrics: Population, median income, unemployment rates, age distribution.
o	Source: US Census Bureau.
o	Granularity: State and county level (latest estimates).
3.	Weather Data:
o	Metrics: Temperature, precipitation, humidity, extreme weather events.
o	Source: Open Weather.
o	Granularity: State level, aggregated monthly (2020–2023).
________________________________________
**Data Ingestion**
Tools Used
•	Spotfire Data Connector(ODATA):
o	Configured to load COVID-19 data as ODATA.
•	Python Scripts via Spotfire Data Functions: -Configured to load US Census and Weather data directly from API into Spotfire Data Function and convert into data table .
o	Automated data loading and initial preprocessing.
Process
1.	COVID-19 Data:
o	Imported Weekly deaths from 2020 to 2023 into Spotfire.
2.	US Census Data:
o	Imported data via API containing demographic and economic data.
o	Mapped State and Year as the primary key for joining with other datasets.
3.	Weather Data:
o	Imported single day weather data aggregated by state.
________________________________________
**Data Transformation**

A. **Cleaning**
1.	Missing Values:
o	COVID-19: Filled missing Vaccination Rate with state-level averages.
o	Weather: Interpolated missing values for Humidity and Precipitation using monthly averages.
2.	Standardization:
o	Dates converted to the format YYYY.
o	State names standardized to title case (e.g., New York).
3.	Filtering:
o	Removed non-state territories (e.g., Guam, Puerto Rico, New York City) to focus on US states.

B. **Joining**
•	Merged datasets using:

o	Primary Keys: State and Date.
o	Join Types:
	Left Inner Join for COVID-19 and Weather data.
	Left Join for Census data with the merged COVID-19/Weather dataset.
________________________________________
**C. Feature Engineering**
1.	Derived Metrics:
o	Covid Deaths Per Capita = Covid Deaths ÷ Population.
o	Deaths Per Capita = Deaths ÷ Population.
o	Weather-COVID Interaction: Humidity * Avg Temperature.
2.	Categorical Variables:
o	Grouped income into Low, Medium, and High categories using percentiles.
3.	Time-Based Aggregations:
o	Rolled daily COVID-19 data into monthly averages for consistency with Weather data.
________________________________________
**D. Normalization**
•	Applied z-score normalization to numeric variables (e.g., population, case rates) to ensure uniform scaling across features.
________________________________________
**Approach**
Data Integration and Preprocessing
1.	Data Cleaning:
o	Handled missing values by filling them with mean or median where applicable.
o	Standardized formats across datasets (e.g., date and state names).
2.	Data Joining:
o	Merged datasets on common attributes like State and Date.
3.	Derived Metrics:
o	Calculated per-capita COVID-19 deaths using census population data.
o	Derived average monthly temperature and precipitation from weather data.
________________________________________
**Data Functions in Use:**
Python Scripts in used as Data Function
•	Open Weather Data: This python script is used to get weather data from Open Weather API. The variables are state,capital,temperature, feels like,min temperature, max temperature,pressure,humidity,visibility,weather description,cloudiness,wind speed,wind direction,latitude,longitude. The funcion parses the data into data frame which is passed as output parameter into table.
•	US Census Data Function: This python script is used to get US Census data from US Census API. The variables are state,total population,median household income,gini index (income inequality),median gross rent,median home value,median age,unemployment rate,white population,black or african american population,hispanic or latino population.The funcion parses the data into data frame which is passed as output parameter into table.
•	Random Forest Algorithm: This python script contains Random Forest Algorithm to predict covid case rate based on population, Household Income, Temperature, Humidity.
•	K-Means Clustering ML Algorithm: This python script is contains K-Means Clustering algorithm which is cluster data using variables such as population,age,unemployment rate,GDP,home value,home rent and median income.
________________________________________
**Dashboard Architecture/Features**
1. Overview Page
•	Visuals:
o	Landing Page describing ojective of the dashboard.
2. COVID 19 Deaths Analysis Page
•	Visuals:
o	Line chart comparing COVID-19 case rates across different yearss.
o	Choropleth map showing the correlation between demographic factor such as Population and COVID-19 deaths.
•	Interactivity:
o	Dropdowns to select specific variables (State, Year).
3. Weather Impact Page
•	Visuals:
o	Line chart overlaying average minimum and maximum temperature.
o	Choropleth map of average temperature for different states.
o	Tree Map showing overall weather coverage for different states.
•	Interactivity:
o	Dropdowns to select specific variables (State, Year).
4. US Census Data Page
•	Visuals:
o	Scatterplot chart overlaying the median home value and gross home rent.
o	Bar Chart to visualize different population such as Black, White and Hispanic.
•	Interactivity:
o	Dropdowns to select specific variables (State, Year).
o	The Population breakdown can be visualized either in Bar Chart or Line Chart.
________________________________________
**Handling User Interactions**
1. Synchronization
•	All visualizations are interlinked, so user selections in one visualization automatically update others.
•	Example:
o	Selecting Texas in the State filters all charts and tables to show data for Texas.
2. Real-Time Calculations
•	Using Spotfire data functions (Python scripts) to predict key metrics, such as:
o	Actual vs Predited Economic Index.
o	K_Means Clustering used to group data into clusters.
3. Performance Optimization
To handle large datasets and ensure responsiveness:
•	Using Spotfire in-memory data tables for fast querying.
•	Calculations are pre-aggregated where possible, reducing runtime computations.
________________________________________
**Key Insights**
1.	States with higher population densities and lower median incomes experienced higher COVID-19 deaths.
2.	Weather conditions (e.g., low humidity, cold temperatures) correlated with higher case spikes during winter months.
________________________________________
Challenges and Limitations
1.	Data Quality:
o	Missing values in some weather datasets, particularly for smaller states.
2.	Temporal Misalignment:
o	Some COVID-19 data points lacked exact weather information for corresponding dates.
3.	Granularity Discrepancies:
o	Census and COVID-19 data was static (yearly updates), while weather data were dynamic.
________________________________________
Future Improvements
1.	Advanced Analytics:
o	Incorporate machine learning models to predict COVID-19 trends based on weather and demographic data.
2.	Enhanced Interactivity:
o	Add drill-down capabilities to explore county-level data.
3.	Real-Time Updates:
o	Automate data refresh for the dashboard to ensure up-to-date analysis.



