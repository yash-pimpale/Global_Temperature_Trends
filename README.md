
<p align="center">
  <img width="460" height="300" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/Global_warming_logo.jpeg">
</p>

# Global Temperature Trends

## Overview

This project aims to comprehensively examine the factors contributing to global warming by analyzing a diverse dataset of global surface temperature measurements, atmospheric CO2 concentrations, volcanic activity, and solar irradiance over various timescales. By employing robust statistical methods and data visualization techniques, we will explore the relationships between these variables to discern whether human-made factors, particularly increased CO2 emissions, are the primary drivers of observed global temperature increases

## Objective

- Determine temperature trends at distinct geographical locations.
- Calculate and analyze the global surface average temperature variation over time.
- Investigate the correlation between levels of CO2 and temperature patterns.
- Explore the potential impact of volcanic eruptions on global surface temperature changes.
- Examine the influence of solar irradiance activity on variations in global surface temperature.

## Authors

- [@abolipathak](https://github.com/abolipathak)

- [@YashPimpale27](https://github.com/YashPimpale27)
## Installation

</p>

Libraries Used

```bash
import pandas as pd
import numpy as np
import netCDF4 as nc
from datetime import datetime, timedelta
import matplotlib.pyplot as plt
import seaborn as sns
from matplotlib.lines import Line2D
import matplotlib as mplt
import cartopy.crs as ccrs
import cartopy.feature as cfeature
import PIL
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import KFold
from sklearn.ensemble import RandomForestRegressor
from sklearn.metrics import mean_squared_error
```

## Land Surface Temperature Data Extraction 

Monthly Temperature data for each latitude and longitude from year 1880-2023 is present in a grided form in .netcdf file. We need to extract data for specific cities from this .netcdf file for all the years. Below steps are followed :

<p align="center">
  <img width="180" height="400" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/data_extraction.jpg">
</p>

- Extract Temperature, latitude and longitude present in .netcdf file.
- Actual latitude and longitude for each city are different than those present in .netcdf file. Hence we need to compute square distance between each latitude and longitude of respective city and find the nearest co-ordinate.
- Extract data for that city and add it in final dataframe.
- Repeat above step till data for each city is extracted and present in final dataframe.
- Final dataframe will contain Date, city, temperature, actual latitude, actual longitude, Nearest latitude, Nearest longitude and country column.

Note: Grided Form means latitude and longitude are divided into a sequence from max to min values. For e.g. latitude range from -90 to +90. Then it will be present as -90, -88, -86,....., +86, +88, +90.

Below is the Final extracted dataset obtained.

<p align="center">
  <img width="550" height="300" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/land_extracted_data.jpg">
</p>

## Visualization of Mean Land Surface Temperature Trend

The GIF depicts the mean land surface temperature for 12 months as line on the polar scale. Each line indicates mean temperature of a respective year with inner most line indicating year 1880 and outer most as year 2022.

<p align="center">
  <img width="500" height="500" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/Global_Mean_Temperature_Change_V3.gif">
</p>

Below figure depicts a line graph with mean land temperature on y-axis and Year on x-axis.

<p align="center">
  <img width="600" height="400" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/Mean_Land_Surface_Temperature_1.jpg">
</p>

Above figures indicate a noticeable increase in mean land surface temperatures from 1880 to 2022.
The temperature range rose from -0.35°C to 1.3°C over a 42-year span which signifies a significant 471% temperature increase during this period.

## Visualization of Land Surface Temperature Trend For Specific Cities

<p align="center">
  <img width="700" height="500" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/citywise_plot.png">
</p>


## Ocean Surface Temperature Data Extraction

We repeat the same procedure mentioned above (Land Surface Temperature) to extract temperature data for Ocean surface.

## Visualization of Mean Ocean Surface Temperature Trend

<p align="center">
  <img width="620" height="450" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/Ocean_surface.png">
</p>


The above figure depicts the rise in annual mean ocean surface temperatures.The initial temperature in 1880 was approximately -0.19°C and by the year 2022, the final temperature had risen to around 1.53°C.

## Oceanwise Surface Temperature Trends

<p align="center">
  <img width="620" height="450" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/ocean_plots.png">
</p>

In summary, both land and ocean surface temperature data plots exhibit a consistent rise in temperatures over the years. The land surface temperature experienced a substantial increase, while the ocean surface temperature similarly showed an upward trend. 

<p align="center">
  <img width="460" height="300" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/Globe_Mean_Temperature_V1.gif">
</p>

## Correlation Between Temperature and CO2

First load the yearwise atmospheric Carbon dioxide emission data and visualize the data using barplot to observe its trend.

The atmospheric carbon dioxide (CO2) levels have exhibited a consistent upward trend over the course of time. The initial recorded atmospheric CO2 concentration in the year 1959 was 315.98 parts per million (ppm), while in the year 2022, it was measured to be 418.56 ppm.

Since CO2 levels in the atmosphere have been steadily rising, let's investigate if this has anything to do with the increase in temperature.

We now calculate the correlation between mean land surface temperature and CO2 levels over a common range of years to assess their relationship. This is done by combining temperature and CO2 datasets using inner merge.

<p align="center">
  <img width="560" height="400" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/correlarion_co2.png">
</p>

The above scatter plot with temperature on the x-axis and CO2 levels on the y-axis, where each point is colored based on the year. It also adds a regression line to the plot which indicates the trajectory of linear relationship. It reveals a significant positive correlation between the two, substantiated by a Pearson correlation coefficient of 0.951. This coefficient indicates a strong linear relationship between the two variables, suggesting that as CO2 concentrations increase, there is a corresponding elevation in temperature levels.

## Role of Volcanic Eruptions in Rising CO2

Volcanic eruptions release a significant amount of natural CO2 into the atmosphere. We examine how much of the total atmospheric CO2 comes from volcanic emissions.

The substantial volume of CO2 emissions has reached a level where sensors struggle to differentiate between CO2 originating from volcanic sources and CO2 generated by human activities. As a consequences, there is currently a lack of available data specifically attributing CO2 emissions to volcanic sources. Hence we conducted a data modelling procedure to derive estimations of CO2 emissions originating from volcanic activities.

Sulphur dioxide is the second most prevalent gas emitted during volcanic eruptions. Each volcano has a unique CO2/SO2 ratio, allowing us to estimate the amount of carbon dioxide (CO2) released during an eruption.

The discovered dataset includes a CS ratio (carbon dioxide to sulphur dioxide ratio) for each volcano, but there are some missing values for CS. A separate dataset holds volcanic details like explosivity, type, primary rock compositions, elevation, tectonic context, and sulphur dioxide levels. We will utilize this information to predict and fill in missing CS ratios for corresponding records without these values.


## Estimation of Volcanic CO2 Emissions Through Machine Learning

We examined three different machine learning methods – linear regression, random forest, and support vector machine – to predict missing CS ratios. Among these, the random forest regression performed the best, showing a lower RMSE (Root Mean Squared Error) of 1.33. This means the predicted values were closer to the actual ones.

Below are the steps involved in model evaluation and prediction :

<p align="center">
  <img width="460" height="300" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/volcano_flowchart.jpg">
</p>

- Data Collection and Integration:
Merge two datasets - one containing CS ratio and SO2 values, and the other with various attributes of volcanoes.

- Data Preprocessing:
Standardize the data and split it into training, validation, and test sets based on available CS values.

- Model Development and Training:
Develop a Random Forest regression model. Train this model using the training and validation datasets, implementing K-folds cross-validation to enhance performance.

- Model Evaluation:
Evaluate the model's predictive accuracy by calculating the Root Mean Squared Error (RMSE) on the validation dataset (RMSE = 1.33).

- Prediction and Volcanic CO2 Calculation:
Apply the trained model to predict CS values for the test data. Estimate volcanic CO2 emissions by multiplying predicted CS ratios with corresponding SO2 values (measured in Kilotons).

- Conversions and Visualizations:
Convert volcanic CO2 emissions (Kilotons) and atmospheric CO2 levels (Parts per million) into Gigatons for better scale. Visualize the data to gain insights and understanding.

In summary, through merging datasets, training a Random Forest regression model, and evaluating its performance, we predicted missing CS ratios. This information was then used to estimate volcanic CO2 emissions. The chosen algorithm, Random Forest, yielded promising results with an RMSE of 1.33.

<p align="center">
  <img width="560" height="400" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/volcanic_co2.png">
</p>

It is evident from the plot that atmospheric CO2 levels are significantly higher than volcanic CO2 emissions. Atmospheric CO2 levels have been steadily increasing over the years, while volcanic CO2 emissions remain relatively stable. Hence Volcanic CO2 is not the major factor in rising atmospheric CO2 levels.

## Role of Solar Irradiations for Rise in Temperature

Solar irradiance refers to the amount of solar energy received per unit area at a specific location on Earth's surface. It is a measure of the intensity of sunlight reaching a particular area and is typically expressed in watts per square meter (W/m²). Solar irradiance plays a crucial role in understanding and predicting various natural processes, including climate patterns, energy generation from solar panels, and environmental impacts.

Lets examine the potential influence of solar irradiance activity as an additional natural factor contributing to the observed rise in temperature.

We choose a dataset with yearly total solar irradiance measured in W/m^2 from year 1660-2022. 

## Correlation between Temperature and Total Solar Irridance

<p align="center">
  <img width="560" height="400" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/tsi_scatterplot.png">
</p>

The scatter plot portrays temperature on the x-axis and Total Solar Irradiance (TSI) on the y-axis. A regression line is incorporated to display the direction of linear relationship. The plot displays a low positive correlation, as supported by a Pearson correlation coefficient of 0.345. This coefficient indicates a weak linear association, implying that with increasing TSI values, there is a minor increase in global temperature.

<p align="center">
  <img width="660" height="450" src="https://github.com/ACM40960/project-abolipathak/blob/main/Images/Temp_Solar_Plot.jpg">
</p>

Based on the analysis, since we observe a low positive correlation between the two, we can observe increased solar activity aligns with temperature rise. There are Instances of divergence i.e. the temperature fluctuations do not match the solar irradiance activity variations which suggest that solar activity isn't major factor in temperature changes. This can be observed in the year 1980, where we notice a separation between the temperature line and the solar irradiance line. This indicates that these two factors are not strongly linked or correlated with each other. The variations in the amount of solar energy (irradiance) reaching the Earth's surface have a limited and relatively small impact on causing changes in temperature over longer periods. Overall correlation doesn't fully explain recent temperature rise.

We need further research to precisely quantify solar influence on long-term temperature trends.

## Conclusion 

After a comprehensive analysis of the data, it becomes apparent that volcanic eruptions and solar irradiance variations are not the main drivers of the temperature increase. While these natural factors do have some influence, their impact on temperature changes seems to be relatively small. Therefore, we can deduce that the primary cause of the temperature rise is the CO2 emissions resulting from human activities.

## Future Work 

-  Study to figure out how much human activities contribute to the changes in temperature we see. Look into things like how much greenhouse gases we release, changes in how we use land, and other factors that might play a role.

- Look closely at really extreme weather events, like heatwaves and hurricanes, and see if they match up with changes in temperature over time. Check if these events are happening more often or getting stronger in recent years.

-  Take a broader look at what global warming means for our society and economy. Consider things like how it affects our ability to make money, where people live and move, and the health of the public.

- Check how well different plans to reduce the problem, like cutting down on pollution or using more clean energy, actually work. See if these strategies can change the trends in temperature and levels of CO2 in the air.

- Use past temperature and CO2 data to make educated guesses about what might happen in the future. Think about different situations, like if we keep polluting at the same rate or if we make big changes, and what the outcomes could be.

## Data Sources

- Surface Temperature : [NASA GISS](https://data.giss.nasa.gov/gistemp/)
- Atmospheric CO2 : [GML NOAA](https://gml.noaa.gov/ccgg/trends/mlo.html)
- Volcanic SO2 : [NASA GES DISC](https://disc.gsfc.nasa.gov/datasets/MSVOLSO2L4_4/summary?keywords=SO2%20volcanic)
- Volcano Eruption Details : [Global Volcanism Program](https://volcano.si.edu/search_volcano.cfm)
- Total Solar Irradiance : [NCEI NOAA](https://www.ncei.noaa.gov/data/total-solar-irradiance/access/yearly/)

## References 

- [CO₂ and Greenhouse Gas Emissions](https://ourworldindata.org/co2-and-greenhouse-gas-emissions)
by Hannah Ritchie, Max Roser and Pablo Rosado This article was first published in May 2017; last revised in August 2020.

- [The emissions of CO2 and other volatiles from the world’s subaerial volcanoes](https://www.nature.com/articles/s41598-019-54682-1#citeas)
by Tobias P. Fischer, Santiago Arellano, Simon Carn, Alessandro Aiuppa, Bo Galle, Patrick Allard, Taryn Lopez, Hiroshi Shinohara, Peter Kelly, Cynthia Werner, Carlo Cardellini & Giovanni Chiodini

- [NOAA Climate Change : Incoming Sunlight](https://www.climate.gov/news-features/understanding-climate/climate-change-incoming-sunlight)

- [CO2 emissions](https://skepticalscience.com/print.php?r=45)


## CDF Installation 

- pip install --upgrade spacepy
- Download CDF C library from "https://cdf.gsfc.nasa.gov/html/sw_and_docs.html" (Check 32 or 64 bit)
- Create a new folder in "C" drive as "CDF" and paste all the data in this folder (after unzipping the downloaded file)
- Set environment variables (in system variables tab) -->
	1. CDF_LIB --> C:\CDF\bin
	2. CDF_HOME --> C:\CDF
- Import library using "from spacepy import pycdf" command
