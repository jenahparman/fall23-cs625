# HW 4: Arrange Tables

Jenah Parman\
Due: October 25, 2023

## Introduction
This assignment focuses on data visualization and chart implementation, with the aim of answering real-world questions using appropriate charts and design principles. I have chosen **Table 91,"Women Who Have Had a Child in the Last Year by Age"** as the dataset for this assignment. This dataset offers insights into childbirth demographics across different age groups. The following report will detail the approach, chart selection, and design principles applied to reveal significant patterns and relationships within the data.

## Question 1
### Compare the ages of women at the time of the birth of their first child between 1990-2008. For instance, is there any evidence that women in the US are waiting longer to have their first child?
<p align="center">
<img src="/HW4/Resources/D1_Q1chart_tableau.png" width="800">
</p>

*Link to Chart: <a href= "/HW4/Resources/D1_Q1.twb" >Tableau Workbook</a>*

For this question, I created a slopegraph in Tableau to compare the ages of women at the time of the birth of their first child between 1990 and 2008. The slopegraph allows for a clear and intuitive visual representation of how these ages have changed over time. It displays two time points (1990 and 2008) for each woman, connected by a line, making it easy to see the shift in ages. This visualization is useful for identifying trends, such as whether women in the US are waiting longer to have their first child, as it clearly illustrates the direction and magnitude of change in a straightforward manner.

After creating the slopegraph, it becomes evident that the younger half of the age ranges exhibits a negative slope, indicating that fewer women in these age groups gave birth in 2008 compared to 1990. In contrast, the older half of the age ranges shows a positive slope, suggesting that more women in these age groups had their first child in 2008. Therefore, it appears that younger generations are waiting longer to have their first child (i.e., there are fewer instances in 2008 compared to 1990), while older generations are having more children in 2008.

**Idiom: Slopegraph / Mark: Point, Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| year | value, quantitative | horizontal spatial region (x-axis) |
| amount of births | value, quantitative | vertical position on two common scales (y-axis) |
| age range | key, categorical | color hue and color saturation |
| age range category (younger half or older half) | key, categorical | color hue |

I noticed that there was a clear divide between positive and negative slopes in the younger and older age groups, so I opted to differentiate them using two distinct hues (blue and orange). I also used variations in saturation within each hue to represent the age range (from dark to light, signifying youngest to oldest within each category). Due to limitations in Tableau, I manually selected line colors for accuracy. To enhance clarity and emphasize key data points, I added points at the end of each line to help viewers easily identify data associated with each year and age group, creating a more visually informative representation.

## Question 2
### How does this compare to the number of women in each age group who had a child (not necessarily their first) in that year? What does this say about the age of women giving birth in the US?
<p align="center">
<img src="/HW4/Resources/D1_Q2chart_tableau.png" width="1000">
</p>

*Link to Chart: <a href= "/HW4/Resources/D1_Q2.twb" >Tableau Workbook</a>*

