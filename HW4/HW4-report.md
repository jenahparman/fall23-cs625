# HW 4: Arrange Tables

Jenah Parman\
Due: October 25, 2023

## Introduction - Dataset 1
This assignment focuses on data visualization and chart implementation, with the aim of answering real-world questions using appropriate charts and design principles. I have chosen **Table 91,"Women Who Have Had a Child in the Last Year by Age"** as the dataset for this assignment. This dataset offers insights into childbirth demographics across different age groups. The following report will detail the approach, chart selection, and design principles applied to reveal significant patterns and relationships within the data.

### Question 1
#### Compare the ages of women at the time of the birth of their first child between 1990-2008. For instance, is there any evidence that women in the US are waiting longer to have their first child?
<p align="center">
<img src="/HW4/Resources/D1_Q1chart_tableau.png" width="800">
</p>

*Link to Chart: <a href= "/HW4/Resources/D1_Q1.twb" >Tableau Workbook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/births4.csv">Births Excel Spreadsheet</a>*

For this question, I created a slopegraph in Tableau to compare the ages of women at the time of the birth of their first child between 1990 and 2008. The slopegraph allows for a clear and intuitive visual representation of how these ages have changed over time. It displays two time points (1990 and 2008) for each woman, connected by a line, making it easy to see the shift in ages. This visualization is useful for identifying trends, such as whether women in the US are waiting longer to have their first child, as it clearly illustrates the direction and magnitude of change in a straightforward manner.

After creating the slopegraph, it becomes evident that the younger half of the age ranges exhibits a negative slope, indicating that fewer women in these age groups gave birth in 2008 compared to 1990. In contrast, the older half of the age ranges shows a positive slope, suggesting that more women in these age groups had their first child in 2008. Therefore, it appears that younger generations are waiting longer to have their first child (i.e., there are fewer instances in 2008 compared to 1990), while older generations are having more children in 2008.

**Idiom: Slopegraph / Mark: Point, Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| year | key, ordered | horizontal spatial region (x-axis) |
| amount of births | value, quantitative | vertical position on two common scales (y-axis) |
| age range | key, categorical | color hue, color saturation |
| age range category (younger half or older half) | key, categorical | color hue |

I noticed that there was a clear divide between positive and negative slopes in the younger and older age groups, so I opted to differentiate them using two distinct hues (blue and orange). I also used variations in saturation within each hue to represent the age range (from dark to light, signifying youngest to oldest within each category). Due to limitations in Tableau, I manually selected line colors for accuracy. To enhance clarity and emphasize key data points, I added points at the end of each line to help viewers easily identify data associated with each year and age group, creating a more visually informative representation.

### Question 2
#### How does this compare to the number of women in each age group who had a child (not necessarily their first) in that year? What does this say about the age of women giving birth in the US?
<p align="center">
<img src="/HW4/Resources/D1_Q2chart_tableau.png" width="1000">
</p>

*Link to Chart: <a href= "/HW4/Resources/D1_Q2.twb" >Tableau Workbook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/births5.xlsx">Births Excel Spreadsheet</a>*

For this question, I created a bar chart in Tableau to compare the number of women giving birth across different age groups in 1990 and 2008. This selection was made for its ability to effectively represent the data and facilitate a clear visual comparison, with age groups categorized on the x-axis and the total number of women who had a child on the y-axis. The use of color (pink for 1990 and green for 2008) further aids in highlighting the differences between the two years. This chart format ensures clarity in presenting the data and enables viewers to easily discern changes in the age of women giving birth in the US over time.

Upon examining the bar chart, it becomes evident that there was a decline in the number of women in their 20s giving birth in 2008 compared to 1990. Additionally, the chart highlights a substantial disparity in the case of older women, specifically those aged 35 to 44, with the most notable difference in bar area when compared to other age categories. It is clear that these older women were giving birth at a considerably higher rate in 2008 compared to 1990.

**Idiom: Bar Chart / Mark: Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| age range | key, categorical | horizontal spatial region (x-axis) |
| total women who gave birth | value, quantitative | vertical position on a common scale (y-axis) |
| year | key, categorical | color hue, horizontal spatial region (x-axis) |

For the bar chart, I opted for pink and green as color choices. This decision was deliberate because I wanted to avoid potential confusion by using the same two colors from the first chart. In the first chart, these colors represented different elements, and to maintain clarity and differentiation in the second chart, I chose a fresh set of colors.

### Further Questions

Exploring the data has unveiled compelling questions for further investigation regarding shifting childbirth dynamics in the US. Here are some questions that emerged while analyzing the visualizations I created:

* **Are women evolving to ensure healthier childbirth as they wait longer to have kids, defying risks associated with geriatric pregnancies?**\
With women increasingly delaying childbirth, is there evidence of an evolutionary shift towards healthier childbirth experiences, contrary to the historical risks associated with later pregnancies? In the past, early motherhood was believed to lead to healthier children due to peak fertility. Are we witnessing an evolution in this regard as women choose to have children later in life?

* **What's driving the trend of delayed parenthood among women?**\
Is the trend of women waiting to have kids primarily because of the increasing costs of raising a family? Could it be a matter of financial readiness?

* **How do education and healthcare factors impact women's family planning?**\
To what extent are education and healthcare related factors influencing women's choices when it comes to family planning? Is the increased access to healthcare and the availability of comprehensive sex education contributing significantly to the decision of when to start a family?

### Extra Credit [2 points]
#### Combine the data from Tables 91 and 92 (Women Who Have Had a Child in the Last Year By Selected Characteristics) to investigate other factors that affect this.

<p align="center">
<img src="/HW4/Resources/D1_ECchart_tableau.png" width="1000">
</p>

*Link to Chart: <a href= "/HW4/Resources/D1_EC.twb" >Tableau Workbook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/births7.xlsx">Births Excel Spreadsheet</a>*

I created an overlay bar chart in Tableau for this question because it's effective at combining data from Tables 91 and 92 to investigate factors influencing childbirth. By focusing on income as a key factor, the stacked bars illustrate how income levels relate to both total births and first births, enabling a clear assessment of this specific aspect of childbirth patterns.

From the bar chart I created, it's evident that individuals with higher income levels are having a significantly greater number of children, whether they are first births or not. This observation strongly suggests that the ability to raise a family may be substantially facilitated by higher income, emphasizing the correlation between income and family size.

**Idiom: Overlay Bar Chart / Mark: Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| number of first births | value, quantitative | horizontal position on a common scale (x-axis) |
| number of total births | value, quantitative | horizontal position on a common scale (x-axis) |
| income | key, categorical | vertical spatial region (y-axis) |
| type of birth (first or not first) | key, categorical | color hue |

I opted for an overlay stacked bar chart to illustrate the relationships between first births and total births within income ranges. This format simplifies comparisons and highlights any patterns. Horizontally arranged, it ensures clear readability of income ranges, while the contrasting orange and blue colors enhance visibility and differentiation.

# Extra Credit [4 points]

Below, you'll find my Python-based recreations of the charts originally created in Tableau.

## Question 1
### Compare the ages of women at the time of the birth of their first child between 1990-2008. For instance, is there any evidence that women in the US are waiting longer to have their first child?
<p align="center">
<img src="/HW4/Resources/D1_Q1chart_seaborn.png" width="800">
</p>

*Link to Chart: <a href= "https://colab.research.google.com/drive/17G5KNvDSdntp73Nt-74d_mf-l8fwCf3u?usp=sharing">ipynb Notebook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/births4.csv">Births Excel Spreadsheet</a>*

For this chart, I utilized Seaborn Object's Plot and incorporated lines with 'o' markers at both endpoints. To enhance clarity, I customized the axis ticks to display only the years 1990 and 2008. The colors were manually selected using hex codes, varying saturation for ages, and categorical hues to distinguish the younger and older age groups. Additionally, I adjusted the linewidth to match the original Tableau chart.

## Question 2
### How does this compare to the number of women in each age group who had a child (not necessarily their first) in that year? What does this say about the age of women giving birth in the US?
<p align="center">
<img src="/HW4/Resources/D1_Q2chart_seaborn.png" width="1000">
</p>

*Link to Chart: <a href= "https://colab.research.google.com/drive/17G5KNvDSdntp73Nt-74d_mf-l8fwCf3u?usp=sharing">ipynb Notebook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/births5.xlsx">Births Excel Spreadsheet</a>*

For this chart, I utilized Seaborn objects to construct a side-by-side bar chart by employing the 'Dodge' feature, ensuring that bars for each category are displayed separately, rather than stacked. The colors were manually selected using a hex color picker to closely match the original Tableau chart's aesthetics. Furthermore, I adjusted the y-axis units to display 'K' and 'M' instead of scientific notation, enhancing readability.

## Extra Credit Question
### Combine the data from Tables 91 and 92 (Women Who Have Had a Child in the Last Year By Selected Characteristics) to investigate other factors that affect this.
<p align="center">
<img src="/HW4/Resources/D1_ECchart_seaborn.png" width="1000">
</p>

*Link to Chart: <a href= "https://colab.research.google.com/drive/17G5KNvDSdntp73Nt-74d_mf-l8fwCf3u?usp=sharing">ipynb Notebook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/births7.xlsx">Births Excel Spreadsheet</a>*

For the overlay stacked bar chart, I employed Seaborn objects and performed some data adjustments, including scaling values by 1000 for consistency. I aimed to represent a part-to-whole relationship, with first births encompassed within total births, rather than being added on top. To achieve this, I subtracted the 'First Births' column from the 'Total Births' column and used the result as the new 'Total BIrths' before creating the stacked bar chart in Python. Additionally, I removed dollar signs from the income labels to ensure a more visually appealing and consistent display. The color palette was selected using a hex color picker, and the 'Stack' feature was used to create the chart.

# Extra Credit [5 points]

## Introduction - Dataset 2
This assignment focuses on data visualization and chart implementation, with the aim of answering real-world questions using appropriate charts and design principles. I have chosen **Table 118 - Death Rates for Major Causes of Death--States and Island Areas"** as the second dataset for this assignment. This dataset provides vital insights into death rates attributed to major causes across various states and island areas. The following report will detail the approach, chart selection, and design principles applied to reveal significant patterns and relationships within the data.

### Question 1
#### Which states had the highest death rates over all causes in 2006?
<p align="center">
<img src="/HW4/Resources/D2_Q1chart_tableau.png" width="800">
</p>

*Link to Chart: <a href= "/HW4/Resources/D2_Q1.twb" >Tableau Workbook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/deaths.xlsx">Deaths Excel Spreadsheet</a>*

For this question, I decided to make a horizontal bar chart in Tableau. This orientation was chosen to enhance the readability of state names. The bars are in a pastel green shade. The decision to use a bar chart was driven by the need for a to compare death rates among states, allowing for an efficient visual assessment of the data. In examining the chart, it became clear that Mississippi had the highest death rates overall, followed by Alabama, West Virginia, Louisiana, and Oklahoma.

**Idiom: Bar Chart / Mark: Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| state | key, categorical | vertical spatial region (x-axis) |
| number of deaths | value, quantitative | horizontal position on a common scale (x-axis) |

### Question 2
#### Is this ordering different if you compare deaths due to disease vs. deaths due to accident, injury, and assault? In other words, which states are more hazardous to your health vs. which states are the most dangerous?

<p float="left">
<img src="/HW4/Resources/D2_Q2chart2_tableau.png" width="499" >
<img src="/HW4/Resources/D2_Q2chart1_tableau.png" width="499" >
</p>

*Link to Chart: <a href= "/HW4/Resources/D2_Q2.twb" >Tableau Workbook</a>*\
*Link to Edited Excel Spreadsheet: <a href= "/HW4/Resources/deaths2.xlsx">Deaths Excel Spreadsheet</a>*

For this question, I merged the data from both categories and constructed horizontal bar charts in Tableau for comparison. Utilizing the same pastel green color for consistency, the charts distinctly displayed variations in the states with the highest death rates, depending on the cause of death. I aimed to explore the variation in ordering rather than directly comparing the values themselves. To achieve this, I created two charts and positioned them side by side. It's important to note that while assessing the assault data, there were missing values for the states of North Dakota, Wyoming, and Vermont, which were replaced with '0' for the visualization. These visualizations made it evident that differences exist in the states categorized as the most hazardous to one's health versus those considered the most dangerous. For deaths caused by disease, the top five states with highest rates were Mississipi, Oklahoma, Alabama, West Virginia, and Tennessee. For deaths caused by accidents, injuries, and assault, the top five states were: Mississippi, Louisiana, New Mexico, West Virginia, and Alabama. There are a few similarities in both charts, and Mississippi was the top state in both. 

**Idiom: Bar Chart / Mark: Line**
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| state | key, categorical | vertical spatial region (x-axis) |
| number of deaths | value, quantitative | horizontal position on a common scale (x-axis) |
| cause of death | key, categorical | vertical spatial region |


### Further Questions

Exploring the data has unveiled compelling questions for further investigation regarding shifting childbirth dynamics in the US. Here are some questions that emerged while analyzing the visualizations I created:

* **What are the underlying factors contributing to differences in state death rates when comparing deaths due to disease versus deaths resulting from accidents, injuries, and assaults?**\
   Are there specific regional or lifestyle factors that explain variations in state death rates based on the cause of death?

* **Are states with high death rates due to disease taking different preventive measures compared to those with high death rates from accidents, injuries, and assaults?**\
  What strategies and interventions could be tailored to address these differing health and safety challenges effectively?

# References

* Statistical Abstract of the United States: 2012, https://www.census.gov/library/publications/2011/compendia/statab/131ed.html
* *Visualization Analysis and Design*, https://go.oreilly.com/old-dominion-university//library/view/visualization-analysis-and/9781466508910/
* Understanding Pandas Melt — pd.melt(), https://pub.towardsai.net/understanding-pandas-melt-pd-melt-362954f8c125Links to an external site.
* pandas.DataFrame.drop, https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop.html
* The seaborn.objects interface, https://seaborn.pydata.org/tutorial/objects_interface.html
* Properties of Mark objects, seaborn.objects.Plot, https://seaborn.pydata.org/generated/seaborn.objects.Plot.html#seaborn.objects.Plot
* Customizing Matplotlib with style sheets and rcParams, https://matplotlib.org/stable/users/explain/customizing.html
* List of named colors, https://matplotlib.org/stable/gallery/color/named_colors.html
* Marks and Channels tutorial with Seaborn Objects, https://github.com/odu-cs625-datavis/public-fall23-mcw/blob/main/Marks_Channels_Seaborn_Objects.ipynb
* How to Tableau : Multiple Measures on Multiple Rows, https://www.youtube.com/watch?v=6o_D9vDZfa8
* Overlay Bar Chart, https://domo-support.domo.com/s/article/360043429413?language=en_US





