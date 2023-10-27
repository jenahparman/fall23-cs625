# HW 4: Arrange Tables

Jenah Parman\
Due: October 25, 2023

## Introduction - Dataset 1
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

For this question, I used a bar chart to compare the number of women giving birth across different age groups in 1990 and 2008. This selection was made for its ability to effectively represent the data and facilitate a clear visual comparison, with age groups categorized on the x-axis and the total number of women who had a child on the y-axis. The use of color (pink for 1990 and green for 2008) further aids in highlighting the differences between the two years. This chart format ensures clarity in presenting the data and enables viewers to easily discern changes in the age of women giving birth in the US over time.

Upon examining the bar chart, it becomes evident that there was a decline in the number of women in their 20s giving birth in 2008 compared to 1990. Additionally, the chart highlights a substantial disparity in the case of older women, specifically those aged 35 to 44, with the most notable difference in bar area when compared to other age categories. It is clear that these older women were giving birth at a considerably higher rate in 2008 compared to 1990.

**Idiom: Bar Chart / Mark: Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| age range | key, categorical | horizontal spatial region (x-axis) |
| total women who gave birth | value, quantitative | vertical position on a common scale (y-axis) |
| year | key, categorical | color hue |

## Further Questions

Exploring the data has unveiled compelling questions for further investigation regarding shifting childbirth dynamics in the US. Here are some questions that emerged while analyzing the visualizations I created:

* **Are women evolving to ensure healthier childbirth as they wait longer to have kids, defying risks associated with geriatric pregnancies?**\
With women increasingly delaying childbirth, is there evidence of an evolutionary shift towards healthier childbirth experiences, contrary to the historical risks associated with later pregnancies? In the past, early motherhood was believed to lead to healthier children due to peak fertility. Are we witnessing an evolution in this regard as women choose to have children later in life?

* **What's driving the trend of delayed parenthood among women?**\
Is the trend of women waiting to have kids primarily because of the increasing costs of raising a family? Could it be a matter of financial readiness?

* **How do education and healthcare factors impact women's family planning?**\
To what extent are education and healthcare related factors influencing women's choices when it comes to family planning? Is the increased access to healthcare and the availability of comprehensive sex education contributing significantly to the decision of when to start a family?

## Extra Credit
### Combine the data from Tables 91 and 92 (Women Who Have Had a Child in the Last Year By Selected Characteristics) to investigate other factors that affect this.

<p align="center">
<img src="/HW4/Resources/D1_ECchart_tableau.png" width="1000">
</p>

*Link to Chart: <a href= "/HW4/Resources/D1_EC.twb" >Tableau Workbook</a>*

I chose a stacked bar chart for this question because it's effective at combining data from Tables 91 and 92 to investigate factors influencing childbirth. By focusing on income as a key factor, the stacked bars illustrate how income levels relate to both total births and first births, enabling a clear assessment of this specific aspect of childbirth trends.

From the bar chart I created, it's evident that individuals with higher income levels are having a significantly greater number of children, whether they are first births or not. This observation strongly suggests that the ability to raise a family may be substantially facilitated by higher income, emphasizing the correlation between income and family size.

**Idiom: Overlay Bar Chart / Mark: Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| number of first births | value, quantitative | horizontal position on a common scale (x-axis) |
| number of total births | value, quantitative | horizontal position on a common scale (x-axis) |
| income | key, categorical | vertical spatial region (y-axis) |
| type of birth (first or not first) | key, categorical | color hue |




