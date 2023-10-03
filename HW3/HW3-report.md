# HW 3: Create Visualization Idioms from Real-World Data - CS 625, Fall 2023

Jenah Parman\
Due: October 4, 2023

## Introduction
text


## Data

### Bar Chart
For my bar chart, I used data from the table, <a href="/HW3/Resources/12s0800.xls">"National Research & Development (R&D) Expenditures as a Percent of Gross Domestic Product by Country"</a> (Table 800, Section 16: Science and Technolgy). This table exhibits the proportion of countries' GDP that is spent on R&D activities.\
To prepare the data for visualization, I decided to choose the most recent year in the table that had values for every country available (2008). Then, I copied these values and created a new Excel spreadsheet with two rows: one for the country names and the other for their corresponding value. Below is a screenshot of the original table on the left and a screenshot of the <a href="/HW3/Resources/r&d.xlsx">new table</a> on the right (what I used to create the bar chart).

<p float="left">
<img src="/HW3/Resources/screenshot1.png" width="499" alt="cat pet typo">
<img align=bottom src="/HW3/Resources/screenshot2.png" width="499" alt="dog pet typo">
</p>

### Scatterplot
To create the scatterplot, I used two different tables: <a href="/HW3/Resources/12s0029.xls">"Urban and Rural Population by State"</a> (Table 29, Section 1: Population) and <a href="/HW3/Resources/12s0358.xls">"Land and Water Area of States and Other Entities"</a> (Table 358, Section 6: Geography and Environment).
"Urban and Rural Population by State" had information on populations for urban and rural areas for each state for the years 1990 and 2000. "Land and Water Area of States and Other Entities" displayed the total area, land area, and water area of each state in square miles (and square kilometers).\
I decided to create a chart that would show the relationship between rural population and land area of states. I created a <a href="/HW3/Resources/landarea_vs_ruralpop.xlsx">new table</a> that contained only state names, rural population, and land area to use for the scatterplot.\
Below are screenshots of the original tables and the new table beneath them.

<p float="left">
<img src="/HW3/Resources/screenshot3.png" width="499" alt="cat pet typo">
<img src="/HW3/Resources/screenshot4.png" width="499" alt="dog pet typo">
</p>
<p align="center">
<img src="/HW3/Resources/screenshot5.png" width="499" alt="other facet before">
</p>

### Multiple Line Chart
For the multiple line chart, I used the table, <a href="/HW3/Resources/12s0858.xls">"Principal Crops--Supply and Use"</a> (Table 858, Section 17: Agriculture). This table contained information on different crops' supply and usage, including acreage planted and acreage harvested for every year from 1990 to 2010.\
I decided to use the top four crops (by acreage harvested) in the table. Below, on the left is a screenshot of the original table. On the right is a screenshot of the  <a href="/HW3/Resources/crops.xlsx">new table</a> I created which contains only the top four crops.

<p float="left">
<img src="/HW3/Resources/screenshot6.png" width="499" alt="cat pet typo">
<img src="/HW3/Resources/screenshot7.png" width="499" alt="dog pet typo">
</p>


When I created the chart, I ended up dropping the fourth crop,leaving the top three (Corn, Soybeans, and Wheat). This is because the fourth crop (Cotton) had a much lower acreage harvested than the others, causing there to be a wide gap in the graph that I did not like.

## Visualization Idioms

### Bar Chart
Idiom: Bar Chart / Mark: Line
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| country name | key, categorical | horizontal spatial region (x-axis) |
| R&D expenditures | value, quantitative | vertical position on a common scale (y-axis) |

### Scatterplot
Idiom: Scatterplot / Mark: Point
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| land area | value, quantitative | horizontal spatial region (x-axis) |
| rural population | value, quantitative | vertical spatial region (y-axis) |

### Multiple Line Chart
Idiom: Line Chart / Mark: Points with line connection
| Data: Attribute | Data: Attribute Type  | Encode: Channel | 
| --- |---| --- |
| year | key, ordered | horizontal spatial region (x-axis) |
| acerage harvested | value, quantitative | vertical position on a common scale (y-axis) |





## Creating the Charts



## Reflection




## References
