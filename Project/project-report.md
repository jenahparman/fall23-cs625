# CS 625: Semester Project

Jenah Parman\
Date: December 6, 2023

## Introduction
This report accompanies a visualization that compares the dietary patterns of the Blue Zones (five areas celebrated for longevity) with the average diets of their respective countries. It showcases the differences in calorie consumption from various food groups, highlighting what residents in the Blue Zones eat compared to others in their country. The aim is to provide a clear visual guide to the food choices that may play a role in the extended lifespans characteristic of these regions.

## Data
### Data Sources
#### Blue Zones Diets
The data source for the Blue Zones' diet was found on the website, *Blue Zones*. The data, which presents pie charts illustrating the diets of centenarians, is accessible at https://www.bluezones.com/explorations/. These charts break down the typical food group composition that these individuals consumed for the majority of their lives. Each Blue Zone has a chart representing the dietary proportions by food group, which contributes to our understanding of their lifelong eating habits. Various food groups were given for each Blue Zone, which were later categorized into seven food groups.
#### National Diets
The data source for the Blue Zones' respective national averages was found on the *Food and Agriculture of the United Nations* site, accessible at https://www.fao.org/faostat/en/#data/FBS. Filters were applied for select countries, food supply (kcal/capita/day), and the year 2021. All food groups were selected, which I later categorized into the same seven food groups. Please note that the national average data presented in this visualization is based on food supply figures, rather than direct dietary consumption. This approach provides an estimation of potential consumption based on the availability of various food items in each country.
### Data Cleaning
In preparation for this visualization, several key data cleaning steps were undertaken. First, I identified seven broad categories that could uniformly represent all food groups from both the Blue Zones and national averages. Then, using OpenRefine, I reclassified the existing food groups into these newly defined categories for consistency. Lastly, I totalled all of the foods kcal/day, subtracted "Other" from the total, and divided each to find the proportions of caloric intake.

For a detailed view of this process, please refer to the following links:

* Original Blue Zones diets dataset: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/BlueZone_diet_original.csv
* Original national diets dataset: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/FAO_national_diet.csv
* List of all food groups and new given food category: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/foodcategories_list.csv
* Final dataset used for visualization: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/final_dataset.csv

## Final Question and Chart
### Which food groups dominate the diets of the longest-living populations compared to the national averages?
I aimed to discover which food groups are most prevalent in the diets of the world's longest-living populations compared to national averages. The analysis revealed distinct dietary patterns in the Blue Zones. Notably, there was a higher consumption of plant-based foods such as fruits, vegetables, and legumes, indicating a preference for natural, unprocessed ingredients. In contrast, the national averages tended to show a more diverse mix, including greater amounts of processed and animal-based products. This finding sheds light on the dietary habits unique to Blue Zones and suggests a potential connection between these eating patterns and the exceptional longevity observed in these communities.

### Final Chart
<img src = "/Project/Resources/CS625_Project.png" width="1000">

*Link to chart:* https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/CS625_Project.pdf

#### Idiom/Mark/Data/Encode Table

Idiom: Small Multiples of Barbell Charts and Maps / Mark: Dots and lines, country maps and stars
| Idiom | Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- | --- | --- | --- |
| entire visualization | Blue Zone and Home Country | key, categorical | vertical and horizontal spatial region |
| barbell chart | food group | key, categorical | vertical spatial region (y-axis) |
| barbell chart | proportion of food group consumption | value, quantitative | horizontal position on a common scale (x-axis) |
| barbell chart | disparity of food group consumption in Blue Zone vs Home Country| value, quantitative | horizontal position on a common scale (x-axis), length of line |
| barbell chart | location (Blue Zone or Home Country) | key, categorical | color of dot (blue or green) |
| map | location of Blue Zone | value, quantitative | vertical and horizontal position (latitude and longitude coordinates) |
| map |location (Blue Zone or Home Country) | key, categorical | color (blue or green), shape (blue star or country map) |


## Final Thoughts
The journey to developing this visualization was filled with its fair share of trials and tribulations. Initially, the most challenging part was gathering the national average food consumption data for each country. This task proved to be difficult and tedious, as I struggled to find data that was consistent and comparable across different regions. Many sources had discrepancies, either in the research methods or in the units of measurement, such as grams instead of calories.

My breakthrough came when I discovered the Food and Agriculture Organization's website, which provided a comprehensive and consistent set of data. With this valuable resource in hand, I moved on to cleaning and categorizing the data. Determining the food categories and calculating the proportions turned out to be a smoother process than anticipated.

Creating the barbell charts in Tableau was relatively straightforward. However, deciding the order of the barbells posed a challenge. My initial approach was to arrange them from longest to shortest, but this arrangement evolved once I placed all the charts side by side. I also tackled creating the country maps in Tableau, which involved a bit of a learning curve. Figuring out how to accurately place the star marker, adjust the map color, and focus on each specific country took some effort, but fortunately, I found excellent guidance from YouTube tutorials and other online resources.

The final assembly of the maps and barbell charts was done using Canva, which led me to re-evaluate and standardize the order of the food group barbells across all charts for better comparability. The most time-consuming aspect was deciding on the positioning of the final chart elements and choosing the fonts in Canva. Selecting the right fonts to convey the right tone and readability proved to be unexpectedly challenging.

In summary, while the process had its complexities, it was very rewarding to see the final visualization come together, offering a clear and insightful comparison of dietary patterns in Blue Zones and their respective countries.

## References:
* National Library of Medicine, Blue Zones - https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6125071/
* Center for Integrative Healing & Wellness, Blue Zones - Learning from the Longevity Hot Spots - https://www.drfabio.com/healthblog/blue-zones-learning-from-the-longevity-hot-spots
* Blue Zones, Explorations - https://www.bluezones.com/explorations/
* Food and Agriculture Organization of the United Nations, Food Balances (2010-) - https://www.fao.org/faostat/en/#data/FBS
* Latitude, Find GPS coordinates for any address or location. - https://latitude.to/
* YouTube, Creating the Map of a Single Country (State) in Tableau by Data Embassy - https://www.youtube.com/watch?v=sadAnZD5Rg0
* YouTube, How to create a barbell chart in Tableau by Tableau - https://www.youtube.com/watch?v=IUrzmhNaLAs
* Tableau, Plotting Geographic Data Using Custom Longitude and Latitude Values - https://kb.tableau.com/articles/howto/plotting-geographic-data-using-custom-longitude-and-latitude?_gl=1*16hti7o*_ga*MTA5MzU4NzUxLjE2OTgzNDUxMjQ.*_ga_8YLN0SNXVS*MTcwMTI5MzQ2MC4xNS4xLjE3MDEyOTM0NzguMC4wLjA.&_ga=2.37448547.29238187.1701132351-109358751.1698345124







