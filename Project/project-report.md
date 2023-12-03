<!---
Report
As always, I expect your report to include your name, CS625, date, and appropriate headings and Markdown markup for clarity and neatness. You will lose points if there are many spelling or grammatical errors.

Your report, named project-report.md, should include the following information:

* a brief description of your chosen datasets (including links to the original sources of the data)
* final question that you addressed
* appropriately-sized image of your final chart
* link to your final chart (similar to HW3, include whatever links or files are needed to view the implementation of your final chart)
idiom/mark/data/encode table for the final chart (see Markdown Code for Table)
* explanation of how your final chart answers the question and how your headline fits your chart
"Final Thoughts" section that provides a commentary on the development process, including roughly how much time you spent developing your visualization and what aspects took the most time
"References" section that includes links to any examples and references that you used in completing this assignment
-->

# CS 625: Semester Project

Jenah Parman\
Date: December 6, 2023

## Introduction
This report accompanies a visualization that compares the dietary patterns of the Blue Zones (five areas celebrated for longevity) with the average diets of their respective countries. It showcases the differences in calorie consumption from various food groups, highlighting what residents in the Blue Zones eat compared to others in their country. The aim is to provide a clear visual guide to the food choices that may play a role in the extended lifespans characteristic of these regions.

## Data
### Blue Zones Diets Data Source
The data source for the Blue Zones' diet was found on the website, *Blue Zones*. The data, which presents pie charts illustrating the diets of centenarians, is accessible at https://www.bluezones.com/explorations/. These charts break down the typical food group composition that these individuals consumed for the majority of their lives. Each Blue Zone has a chart representing the dietary proportions by food group, which contributes to our understanding of their lifelong eating habits. Various food groups were given for each Blue Zone, which were later categorized into seven food groups.
### National Diets Data Source
The data source for the Blue Zones' respective national averages was found on the *Food and Agriculture of the United Nations* site. Filters were applied for select countries, food supply (kcal/capita/day), and the year 2021. All food groups were selected, which I later categorized into the same seven food groups. Please note that the national average data presented in this visualization is based on food supply figures, rather than direct dietary consumption. This approach provides an estimation of potential consumption based on the availability of various food items in each country.
### Data Cleaning
In preparation for this visualization, several key data cleaning steps were undertaken. First, I identified seven broad categories that could uniformly represent all food groups from both the Blue Zones and national averages. Then, I reclassified the existing food groups into these newly defined categories for consistency and clarity. Lastly, I totalled all of the foods kcal/day, subtracted "Other" from the total, and divided each to find the proportions of caloric intake.

For a detailed view of this process, please refer to the following links:

* Original Blue Zones diets dataset: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/BlueZone_diet_original.csv
* Original national diets dataset: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/FAO_national_diet.csv
* List of all food groups and new given food category: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/foodcategories_list.csv
* Final dataset used for visualization: https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/final_dataset.csv

## Final Question and Chart
### Which food groups dominate the diets of the longest-living populations compared to the national averages?
I aimed to discover which food groups are most prevalent in the diets of the world's longest-living populations compared to national averages. The analysis revealed distinct dietary patterns in the Blue Zones. Notably, there was a higher consumption of plant-based foods such as fruits, vegetables, and legumes, indicating a preference for natural, unprocessed ingredients. In contrast, the national averages tended to show a more diverse mix, including greater amounts of processed and animal-based products. This finding sheds light on the dietary habits unique to Blue Zones and suggests a potential connection between these eating patterns and the exceptional longevity observed in these communities

### Final Chart
<img src = "/Project/Resources/CS625_Project.png" width="1000">

*Link to chart:* https://github.com/odu-cs625-datavis/fall23-mcw-jenahparman/blob/main/Project/Resources/CS625_Project.pdf

#### Idiom/Mark/Data/Encode Table

Idiom: Small Multiples of Barbell Charts and Maps / Mark: Dots and lines, stars
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| food group | key, categorical | vertical spatial region (y-axis) |
| proportion of food group consumption | value, quantitative | horizontal position on a common scale (x-axis) |
| disparity of food group consumption | value, quantitative | horizontal position on a common scale (x-axis), length of line |
| location (Blue Zone or Home Country) | key, categorical | color of dot (blue or green) |
| location of Blue Zone | value, quantitative | vertical and horizontal position (latitude and longitude coordinates) |
| Blue Zone | key, categorical | vertical and horizontal spatial region |







