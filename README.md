# Correlation-Study-Climate-Change-EV-Adoption
Data Analytics: Modeling and Studying data relating to climate change and adoption of electric vehicles

### I. INTRODUCTION

Global warming has been a new hot and rising issue in the past concurrent years given rise from national and regional reports around the world. According to the NOAA (National Oceanic and Atmospheric Administration) we have seen ocean and surface temperatures climbing at a steady rate of 0.08 degrees Celsius or 0.13 degrees Fahrenheit per decade since the late 1800s. However, the average rate has increased to almost double that rate or 0.32 Fahrenheit over the past couple years, which leads us the public and scientists to believe that what the nations are doing right now in terms of energy choices have a stark effect on future reality. Given the findings, many of the globes and nation’s leading scientists and engineers have been coming up with solutions to address this problem, one of them being plug-in electric vehicles or (PEVs), with the main purpose of not only being more efficient but also addressing the adoption of them to remove gas guzzlers, lessening the impact of carbon dioxide emissions.

For this final paper, I have raised the question of trying to find out whether electrical vehicles are just the new buzzword or does the effect really have to do with the increasing dangers of climate change. My models will address and evaluate multiple variables including co2 emissions (metric tons per capita), Electric vehicle average ranges, charge ports available, electricity/gas prices, producer indexes for manufacturing related to such vehicles, and other car sales as comparison in the United States. All these variables including the climate change ones will be measured against the increasing sales of PEVs.

In terms of my prediction for whether climate change influences the adoption of PEVs, my educated guess is a simple no. My assumptions are that technologies and their adoption always come in the form of market sentiment and practicality, so we will be studying and investigating more of what contributes to sales (adoption) if the climate change variables are not significant.

### LITERATURE REVIEW

Since the study I’m doing on whether certain factors of vehicles and economics affect decisions of PEV adoption along with some climate change factors, it is very specific and information on articles are hard to find. However, I would like to reference one that was done by the RFF.org. The main study covered in the research article was climate insights of the year 2020 on electric vehicles by the authors Bo Maclnnis and Jon A. Krosnick. The paper goes into detail talking about how people generally take to the general topic of climate change and the stance that the public takes on buying PEVs for this express purpose. The carbon footprint of gas vehicles is not to be overlooked as it accounts for 28% of greenhouse gas emissions according to data from the EPA in 2018, of that 28%, 59% comes from light-duty-vehicles and 23% from medium-sized and heavier duty trucks. With this stated, it does go to show that the conversion to PEVs would help global warming. This paper also mentions another interesting aspect being the general American public’s belief on global warming. Only 58% of people in the states done by their study expresses very serious beliefs about global warming. Another survey by the same people expresses that only 29% of those people believe that an all-electric car helps the environment. Without this being a fact dump I would like to shed light on the rest of the facts right now: Around 50% of Americans believe that it would cost about the same amount of money to maintain and own an electric vehicle as a gas car, around 50% believe that an electric car would cost the same or more to drive, 52% believe that PEVs would depreciate at the same value as a normal car, 79% believing that finding a charging station would be difficult. Overall, this is a very interesting study and to conclude, I would like to state that, maybe there is more that goes into the adoption of electric vehicles, more than the raw factors of climate change, car specifications, and general economics. This study shows that we need to correct misconceptions and have more transparent and factual media to convince the public.

### II. DATA

To preface this section, I want to make a note that I had difficulty grabbing usable data from any raw source, everything had to be processed in one way or another and fit to the  years of 2011-2016, datapoints being monthly. This was the only way to not have holes in my data and fits the scientific study criteria of having more than fifty datapoints.

The datasets for this project come from the different sources and will be referenced in the index and sources section at the end of the paper, mostly United States data, excluding the global temperature data point.

1)	The department of energy US government site for electric vehicle range and plug data.
2)	Kaggle for electric vehicle general information and plug location data.
3)	Fuel and Electricity prices from the DATA.GOV catalog site.
4)	Data for temperature, general vehicle sales, producer price index (auto insurance, semiconductor chip) coming from FRED economic research site.
5)	Yahoo Finance for Tesla stock data.
6)	National Oceanic and Atmospheric Association for temperature average and verification on our co2 emissions data.

All data was cleaned and modified to fit into one singular dataframe for OLS modeling including the variables shown below. Some variables like average max range (average max range), top model for the month (top model), and tesla dummy variable (is tesla) were introduced as extra additions that would let us get usable data, especially for average max range which includes the average range of all PEVs available within that given month. This set of data adheres to an index of date by month starting on the 1st of each month and contains 72 rows and 15 columns including our dependent (units sold) and independent variables.

![image](https://user-images.githubusercontent.com/34585038/147900224-96c8b210-9a28-445c-90c5-44ab22307c1b.png)

Since electric vehicle data is not present or very hard to gather being a new industry all together, it was hard to get clean CSV dating further back prior to 2011 with recent years not being updated fully using 2016 as the most recent benchmark. I did not want to make any unnecessary interpolations or predictions, so this was the safest bet while fitting within the minimum data count necessary for OLS.

### III. MODELS AND METHODOLOGIES

**VARIABLES**

Note: All units are formatted to fit a monthly basis, all data pertains to the United States except for temperature being global (global issue).

**Independent variable: **

Units Sold (Amount of PEVs sold within that given month)

**Dependent variables:**

Average Gas Price (Dollars); Average Diesel Price (Dollars); co2 emissions (metric tons per capita); Charge Port (Number of charging ports sold for PEVs recorded in the US); Station Port (Number of charging ports located at stations in the US); Tesla Stock Price (NASDAQ dollars); Average Max Range (The average maximum range of vehicles available in that given month; Electric Price (Electricity Price in Dollars per Kilowatt Hours); Other Car Sales (Reported count of sales from units sold data set for non PEVs); Temperature Change (Temperature change above or below the normal predicted change in Celsius); PPI chip (Producer Price index for semiconductor chips and related electronics including car chips); PPI insurance (Producer Price index for auto insurance); Is Tesla (Dummy Variable, whether or not 0,1 the top grossing PEV of the month was a Tesla model)

**DESCRIPTIVE STATISTICS**

![image](https://user-images.githubusercontent.com/34585038/147900296-857245fe-bbcb-41a5-9451-a36268bd140e.png)

For the dataset we have 15 total variables and one of them, Units sold, being our dependent variable. Our total sample size is 72 months of total entries with years starting from 2011 through 2016, all data is based in the US excluding our temperature data. The averages are shown above for mean, standard deviation, min and max for each of the independent variables. All the numbers look relatively uniform. The main one I wanted to check was whether this dataset was being represented by tesla and as you can see it is mostly not true as there are many other PEVs out there like the Chevy Bolt, Nissan Leaf, and others, this can be seen via 2%-50-75% percentile being marked as non-Tesla.

**MODELING**

Before we can start the modeling process a correlation matrix was constructed to see if we could take out any variables. The variables that result in high correlation will be remove as usage of one or the other would result in duplication of representation.

After this collinearity (linearity or non-linearity check) we can move on to defining interactive terms, dummy variables, and analysis of heteroscedastic, specification testing (while modeling), and a serial correlation test for this time series relevant data.

These processes will be done in leu with our OLS modeling, improving as we go. Model variables will be adjusted based on the significance of the variable coefficient at the alpha level of 0.05 or 95% and removing variables till the model has only significant variables. Other evaluations will be done for heteroskedasticity and whether WLS should be required. 

The modeling format will be in such a fashion of:

**units_sold = c + b1 gas_price + b2 diesil_price + b3 co2 + b4 charge_port + b5 station_port + b6 tesla_stock + b7 avg_max_range + b8 electric_price + b10 other_car_sales+ b11 temp_change+ b12 PPI_chip + b13 PPI_insurance+ b14 is_tesla**

### IV. ANALYSIS AND INTERPRETATION

**CORRELATION CHECKS**

![image](https://user-images.githubusercontent.com/34585038/147900333-a1f7ea8c-b3c8-489a-b7bb-c9075070772f.png)

As for our initial correlation check you can see many having high correlation especially between some of the variables like (charge_port, station_port), (gas_price, diesel_price). Other than that, after I took some of the values out the correlations were within an acceptable range.

**DUMMY VARIABLES AND INTERACTION TERMS**

The only dummy variable used in this will be whether the EV of the month in terms of sales with a Tesla or a different brand car. The thought behind the inclusion of this variable was because Tesla is known as a publicly hyped company, it is primarily there to check if there were continuous hyped months or to determine if it was all just Tesla based EV data. 

For the interactive terms it is assumed that some of them will depend on each other. However, I will be removing most of them since some of the variables are correlated. The only interaction term that I found relevant that will need to be tested is co2 on temperature change. We will test for this although it will be excluded from the model if the interactions are not significant.

**SERIAL CORRELATION TEST**

Since one of the assumptions of linear regression is to have no correlation between residuals and must be independent. The closer to 0 the test statistic is the more evidence of positive serial correlation there is and vice versa with the value of 4. According to our model and doing the Durbin Watson test statistic is 1.416, within the range of 1.3 and 2.5, which in the case we would consider autocorrelation to be non-problematic in the regression model.

**HETEROSCEDASTICITY**

The formal definition of heteroscedasticity is when the variance of a dependent variable varies, in other words unequal scattering of residuals, complicating analysis. To test this, we will perform a Breusch-Pagan test. In regression analysis , heteroscedasticity means a situation in which the variance of the dependent variable varies across the data. Heteroscedasticity complicates analysis because many methods in regression analysis assume of equal variance. Since our p-value corresponding with the model is 0.079 and the f-value being 1.88 we can conclude that there is no heteroskedasticity present because we fail to reject the null hypothesis that homoscedasticity is present.

![image](https://user-images.githubusercontent.com/34585038/147900372-133ccaf5-b6d0-418a-9ca5-62cb7fb088d2.png)

### OLS MODELS OUTPUT & ANALYSIS

**OLS MODEL I**
units_sold={co2,gas_price,diesil_price,temp_change,station_port,avg_max_range,electric_price,other_car_sales, PPI_chip,PPI_insurance,is_tesla}

![image](https://user-images.githubusercontent.com/34585038/147900388-79cb58d3-509c-48af-81b9-5a91e59f1808.png)

According to this model I have not removed the variables flagged in our correlation test, I wanted to see some preliminary results and have a baseline. It shows multiple variables including diesel price, temp_change not being significant so those were revised for removal in the later model. The variation of that this base model accounts for is 92.9%.

**OLS MODEL II**

EV_UNITS_SOLD = – 4.25e+05 + 1.29e+04co2 + 1866.13gas_price + 0.3716charge_port + 312.9 avg_max_range + 1.386e+05electric_price + 8.043 other_car_sales + 1106.75PPI_chip + 1252.70PPI_insurance + 2230.085is_tesla

![image](https://user-images.githubusercontent.com/34585038/147900412-bc7c5d60-973d-4f17-b288-6f6d6b46ae9f.png)

According to model II, I have added in interaction terms as well as removal of the correlated variables and have got reasonable results (significant variables) for each remainder. The only thing that stands out here is that our temperature or emissions variable is still not significant along with the interaction term, so those are flagged for removal. I have tested out several combinations of more and less variables to see if temperature change would be significant, but that was to no avail, so I will be removing it. The variation accounted for this model is 93.1% slightly more than the previous model. As far as heteroskedasticity goes it fits all checks we will not have to implement a WLS model. 

**FINAL OLS MODEL**
units_sold={co2,gas_price,temp_change,charge_port,avg_max_range,electric_price,other_car_sales, PPI_chip,PPI_insurance,is_tesla}

![image](https://user-images.githubusercontent.com/34585038/147900432-b7c81c6f-7fe0-443f-88e9-8f530cddb8bc.png)

![image](https://user-images.githubusercontent.com/34585038/147900438-e075dd59-d611-4b59-ad15-2fb47a57b04b.png)

This model passes all final checks of heteroscedasticity, serial correlation, correlation, linearity, interactive/dummy variables, and specification testing. All the p-values here are significant and we have an optimal R2 score of 0.927 and F-statistic of 87.68, with a total number of observation n=72, with a total of 9 variables. All the variables have a positive effect on car sales. It seems like the only contributing or helpful climate related variable is co2 emission capita, which I feel is a better indicator instead of the physical surface temperature. For the coefficients, I believe that co2, gas_price, electric_price makes sense as positive variables as the increase in those negative cost factors can drive the switch to electrical vehicles. The other variables are all positive as well since those are industry indicator and specification indicators and can only drive the sales of price, especially with improvements being made each year. The only surprising one to me was charge_port, I would think that it would have a larger effect on decision making, but that comes with the express study of how ports effect EV purchases.


### V. CONCLUSION

My initial prediction of global warming effects having no effect on car sales are somewhat accurate. Through analyzing and performing OLS on the variables to thought have related to PEV sales, I have concluded that surface area temperature has no effect on PEVs whilst the other environment variable carbon emissions having a significant effect. In our final model we have included many variables including industry variables that relate heavily to why PEVs sell, and to be fair, that is more reasonable. It is not out of the realm of possibility for the public to care more about statistics like the driving range, how many charging ports are available, economic industry indexes to gauge the performance of the vehicle and future itself. Global warming might be the initial thought, but it is not one of the many determining factors behind the sales of a unit. To sum things up, the extent at which environmental variables effect are most likely due to how media portrays the subject. Certain statistics although referring to the same thing may have more weight. That thought alone sparks further discussion into delving into how public sentiment connects with the adoption or PEVs or the general sentiment behind climate change. In future studies I feel like there is more to account for behind conversion process to the sale of an EV, more variables will need to be introduced like (tax incentives provided, infrastructure programs, general sentiment using twitter “is it being talked about”, more variables on environmental changes (weather effects), etc.).

### SOURCES
•	Department of Energy
o	https://www.eia.gov/
o	https://afdc.energy.gov/data/10567
•	Kaggle
o	https://www.kaggle.com/geoffnel/evs-one-electric-vehicle-dataset
•	Data.gov
o	https://data.worldbank.org/indicator/EN.ATM.CO2E.PC?end=2018&start=1960&view=chart
•	FRED
o	https://fred.stlouisfed.org/series/ALTSALES
o	https://fred.stlouisfed.org/series/PCU33443344
o	https://fred.stlouisfed.org/series/EMISSCO2TOTVTTTOUSA
o	https://fred.stlouisfed.org/series/PCU9241269241263
o	https://fred.stlouisfed.org/series/APU000072610
•	Yahoo Finance
o	https://finance.yahoo.com/quote/TSLA/
•	NOAA
o	https://www.climate.gov/news-features/understanding-climate/climate-change-global-temperature
•	Literature Review
o	https://www.rff.org/publications/reports/climateinsights2020-electric-vehicles/

### STARGAZER OUTPUT

![image](https://user-images.githubusercontent.com/34585038/147900487-7481b146-45ba-44a1-9145-9e132169f039.png)


