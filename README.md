# Project 4
#### Landon, Abiza, Graham, Ed, Adi

### Problem Statement:
This project aims to uncover trends in emissions that are harmful to humans, focusing on demographics, trends over time, the connection between emissions and climate, and efforts to reduce emissions through increased solar energy production. Specifically, we want to understand the progress that the state of California has made in reducing emissions and what needs to be addressed going forward.

### Table of Contents:

Landon:
(Note: Due to size constraints the data could not be uploaded into the Github repo. To duplicate my results see below where I describe data assembly.)
- Data_orginization.ipynb
    - Initial merging of EPA data for the years 2016 through 2021.
    - Analysis on what data is best to keep.
- Merge_EJSCREEN_with_Energy_cost_Data.ipynb
    - Combines EPA data and LEAD data.
    - Performed analysis on data and created visualizations.

Abiza:
- Background_Info.ipynb
    - Exploration of relationships between health, poverty, and pollution 
    - Includes visuals 
- An OLS model predicting rate of ER admissions per 10,00 for cardiovascular disease using score of pollution 

Graham (Emissions Patterns):
- em_statewide_EDA.ipynb:
    - Visualizations of California state-wide emissions
    - Based on (and completes) formatting in em_statewide_formatting.ipynb
- em_county_EDA.ipynb:
    - Visualization tool for select California county-level emissions
    - Based on formatting in em_county_formatting.ipynb

Ed(Weather Insights):
- weather.ipynb:
    - Visualization and EDA on weather data from 1980 to 2022
    - Data source: https://www.visualcrossing.com/weather/weather-data-services
- wildfire.ipynb:
    - Visualization and EDA on wildfire and droughts data
    - Resources: 
        - https://www.fire.ca.gov/incidents/2018/
        - https://github.com/abarbour/FireHistory

Adi (Solar Energy)
- Solar_prod_data_col.ipynb
    - Webscraping of data from CA Dept. of Energy using Selenium
- Solar_prod_eda.ipynb
    - Visualization and analysis of PV and Thermal Solar energy production


#### Landon

Main Purpose:
This data set is presented to show some of the inequalities concerning energy as measured by variations around pricing and environmental hazards.

Data Assembly:
This data comes from two sources. The first part comes from the EPA. They have data for each census block across the country and measure various environmental hazards alongside demographic information. They have relevant data for the years 2016 through 2021. The actual data measured varies somewhat from year to year. So when I measured these data, I preserved only the data consistently recorded for each year. The data can be found [here](https://gaftp.epa.gov/EJSCREEN/).

Another dataset I used was the [LEAD tool](https://lead.openei.org/), a dataset about Low-Income Energy Affordability. This dataset has the average annual energy cost for households by Census Tract. A Census Tract includes census blocks, which constitute the rows of the other dataset. A Census block adds one number to the end of the census tract code. So I was able to merge the datasets on this code.

(Note: Due to size constraints, the data could not be uploaded into the Github repo. To duplicate my results, you may pull from the following websites:
EPA data:  Index of /EJSCREEN (epa.gov)
   1. From the 2016 directory pull:  EJSCREEN_Full_V3_USPR_TSDFupdate.csv
   
   2. From the 2017 directory pull: EJSCREEN_2017_USPR_Public.csv
 
   3. From the 2018 directory pull: EJSCREEN_StatePctile_2018.csv
   
   4. From the 2019 directory pull:  EJSCREEN_2019_StatePctiles.csv
   
   5. From the 2020 directory pull:  EJSCREEN_2020_StatePctiles.csv
   
   6. From the 2021 directory pull:  EJSCREEN_2021_StatePctiles.csv

The LEAD data can be pulled from:  LEAD Tool (openei.org)
   1. When  the website loads:
   
   2. Click go
   
   3. Search for California
   
   4. In the map-overlay window click view Census Tracts
   
   5. Download the data, there is an option right below the displayed map.)


Data Dictionary:
Note: Each feature with an * actually represents 6 features measuring the same thing but for different years. We have data for the year 2021, 2020, 2019, 2018, 2017, and 2016. These descriptions are from the EPAs dictionary [here](https://www.epa.gov/ejscreen/ejscreen-map-descriptions#:~:text=Air%20Toxics%20Respirato,ry%20Hazard%20Index%20Air%20toxics%20respiratory,set%20by%2.%20EPA%20National%20Air%20Toxics%20Assessments).
|Feature|Type|Description|
|---|---|---|
|ID|code|The census block number for the area.|
|Geography ID| code| The census tract number for the area. The same as ID but without the last numeral.|
|Name|string|The name of the census tract the area is a part of.|
|County|code|The county the area is a part of.|
|Tribal Areas|string| The name of the tribe associated with this area and nan if there is no such tribe.|
|Avg. Annual Energy Cost|int| The average yearly cost of energy in the census block area. Measured in Dollars|
|Shape_Area|int| The land area of the Census Block. Measured in miles.|
|Shape_Length|int|The longest length within the Census Block. Measured in miles.|
|ACSTOTPOP_*|float| The total population in the Census Block.|
|CANCER_*|float|A generated value that describes the local cancer risk.|
|DSPLM_*|float| The amount of Diesel Particulate matter in the air, measured in micrograms per cubic meter.|
|LESSHSPCT_*|float| The percent of the population with less than a High-school education.
|LINGISOPCT_*|float| The percentage of the population that is linguistically isolated.
|LOWINCPCT_*|float| Percent of the population with low income.|
|MINORPCT_*|float| Percent of the population that is part of a minority group.|
|OVER64PCT_*|float| The percent of the population over the age of 64.|
|OZONE_*|float| The amount of ozone in the lower atmosphere, measured in parts per billion.|
|PM25_*|float| The amount of atmospheric particulate matter that has a diameter of 2.5 micrometers or less. Measured in micrograms per cubic meter.|
|PNPL_*|float| Gives the relative proximity of superfund sites. These are sites the EPA is commited to decontaminate.|
|PRE1960PCT_*|float| The percent of the housing stock built before 1960.|
|PRMP_*|float| Gives the relative proximity of facilities regestired with the risk management peogram. These facilities are required to have an action plan if public becomes endangered by chemicals or volitale compounds they store.|
|PTRAF_*|float| Gives the relative amount of traffic in the area. Measured in daily vehicles per meter.|
|PTSDF_*|float| Gives the relative amount of local waste water discharge. Measured in facilities per kilometer.|
|PWDIS_*|float| Provides the relative amount of local hazardous waste. Measured in toxicity-weighted concentration per meter.|
|RESP_*|float| Air toxics respiratory hazard index (the sum of hazard indices for those air toxics with reference concentrations based on respiratory endpoints, where each hazard index is the ratio of exposure concentration in the air to the health-based reference concentration set by the EPA). (Direct quotation from the above [website](https://www.epa.gov/ejscreen/ejscreen-map-descriptions#:~:text=Air%20Toxics%20Respiratory%20Hazard%20Index%20Air%20toxics%20respiratory,set%20by%20EPA%29.%20EPA%20National%20Air%20Toxics%20Assessments).)
|UNDER5PCT_*|float| The percentage of the population under the age of 5.|

Data Visualizations and Conclusions:
I visualized the data by grouping according to county. I found that counties with more poverty did not have cheaper energy available. It cost at least $2000 dollars annual. Many of the more prosporous counties had cheaper costs. Ozone pollution was also corralted to higher energy costs, demonstrating that more expensive energy was related to worse environmental hazards.

Future Work:
Fundamentally this data shows that there are injustices related to energy pricing. However, there are many confounding variables when looking at data like this. This includes population, the extent the location is rural, and how low income communities are geographically distributed. I would like to perform more work to untangle these variables. This future work may include finding more data to link these data to where energy is produced and the local energy mix consumed.

Python Packages: pandas


#### Abiza

Why should we care about air quality and make efforts to reduce emissions?
The majority of pollutants are emitted through human activities like burning fossil fuels, vehicle exhaust fumes and emissions from agriculture and industry (ClientEarth). These pollutants enter our body through our respiratory tract. Constant and extended exposure to these contaminants may result in serious health issues. Short term effects include disrupted breathing, asthma, chest pain,and coughing. And long term effects include heart disease, lung disease, stroke, and even cancer. Currently, there is more research being done on linking pollution to other conditions and diseases as well. 

I used data from the California Office of Environmental Health Hazard Assessment (https://oehha.ca.gov/calenviroscreen/maps-data) to draw conclusions on the relationships between health, poverty, and pollution .The simply downloaded from OEHHA, and imputed the  I used Python as my programming language and used the following packages to read my data, create some graphs, and finally create a simple OLS model to predict Age-adjusted rate of emergency department visits for heart attacks per 10,000 : pandas, matplotlib, matplotlib.pyplot, numpy, seaborn and statsmodel.api. Due to high housing costs and historical discrimination, low-income and minority neighborhoods are clustered around industrial sites, truck routes, ports and other air pollution hotspots. Unfortunately, areas that are lower income and have higher poverty rates disproportionately feel environmental burdens. We as humans need to put in effort to clean the air that we polluted to protect ourselves and those around us. There are many ways to contribute to making our air clean again. However, we will go more into detail about reducing emissions through the use of solar energy.


#### Graham (Emissions Patterns):
To analyze emissions patterns over time in California, I used emissions inventory data from the California Air Resources Board [CEPAM2019v1.03 Standard Emission Tool](https://ww2.arb.ca.gov/applications/cepam2019v103-standard-emission-tool). I used this tool to gather data on nine different types of emission which can be harmful for humans to inhale over the period 2000-2021, both statewide and for ten particular counties, which are meant to represent a reasonable cross-section of California counties. Observations after 2019 are projections, and so crucially do not capture emissions caused by severe wildfires in 2020 and 2021. I also conducted analysis on emissions per capita, for which I gathered population data for the state and counties from the Federal Reserve Economic Database (FRED) [Resident Population Series tool](https://fred.stlouisfed.org/series/CAPOP).

These datasets were relatively complete and required minimal cleaning. Missing values in the emissions data indicated that the corresponding source did not exist in the given year for the given locality (county), and so were imputed to be 0. Population data from FRED were complete. I formatted emissions and population data into data frames for each locality (state/county) so that they would be easiest to perform EDA on and create visualizations from. This included creating data for emissions per capita. Ultimately, each observation in a given data frame or its corresponding CSV is specific to an emission source, type of emission, and year, and includes both total and per capita emission volume in tons per day.

Python Packages: pandas, matplotlib.pyplot, seaborn

#### Adi (Solar Production):
Climate change has been known to largely be driven by increasing levels of greenhouse gasses in the atmosphere, emitted by the burning of fossil fuels. These emissions not only impact human life through changes in the environment, but through direct health effects of particulates as well. Solar energy production provides a method for producing energy with a much smaller carbon footprint, eliminating the need for burning coal or natural gas. Solar electricity production in California falls into two categories - solar thermal, using the concentrated heat of sunlight to heat a fluid to make steam to turn a traditional turbine and generator making electricity; and solar photovoltaic (PV), the direct conversion of sunlight into electricity. The data presented was collected, processed, and analyzed using the Python programming language. The Selenium package was used for webscraping of the California Department of Energy’s yearly solar statistics here: https://ww2.energy.ca.gov/almanac/renewables_data/solar/index_cms.php. Data collected includes solar production by plant and company name, solar production by counties, solar energy imports, and total annual solar production. Each table of data was collected for each year available and combined into CSVs for each separate category. Data was organized into dataframes per category of data, and analyzed using visualizations from matplotlib. Bar graphs were used to show imported energy, production by county, and total production per year, and line plots were used to show the change over time of the top and bottom producing counties.


