# HW 5: Analyzing Data Using Distribution Charts

Jenah Parman\
Date: November 8, 2023

## Introduction
This report is focused on the task of creating distribution charts, namely histograms, eCDFs, and boxplots, with the specific aim of utilizing them to guide further analysis of the underlying data. I chose the dataset from Table 29, 'Urban and Rural Population by State' as the basis for this analysis.

## Part 1: Create Distribution Charts

Before creating any distribution charts with the dataset, I performed some data adjustments using Pandas.

        import pandas as pd
        import numpy as np
        import seaborn as sns
        import seaborn.objects as so
        import matplotlib.pyplot as plt
        import matplotlib as mpl
        import matplotlib.ticker as mtick
        from seaborn import axes_style
        
        df = pd.read_excel('/content/10s0029.xls', skiprows=4)
        df1 = df.copy()

I removed unnecessary rows, including the header rows, 'United States,' and 'District of Columbia', and footer rows.

        df1.drop(df.index[:4],axis=0,inplace=True)
        df1.drop(df.index[[4,13]],axis=0,inplace=True)
        df1.drop(df.index[56:],axis=0,inplace=True)


Then, I retained only the columns that contained urban and rural populations and reset the index. 

        df1.drop(df.columns[[1,2,3,4,5,7]],axis=1,inplace=True)
        df1 = df1.reset_index(drop=True)

I then rescaled the population values by multiplying them by 1000 for accuracy and renamed the columns to simply "State", "Rural", and "Urban".

        df1.iloc[:, 1:4] = df1.iloc[:, 1:4] * 1000
        df1.columns = ['State','Urban','Rural']

Lastly, to better organize the data for analysis, I transformed it into a long format, where the urban and rural data became part of a single column labeled "Population_Type" and the adjacent column which represented the population became "Population_Amount".

        df1 = df1.melt(id_vars=['State'],
                       value_vars=['Urban','Rural'],
                       var_name='Population_Type',
                       value_name='Population_Amount')
                       
<a href="/HW5/Resources/10s0029.xls">Link to 'Before' Dataset</a> | <a href="/HW5/Resources/newdf.csv">Link to 'After' Dataset</a>

### Boxplot

For this chart, I used the Seaborn library to create a boxplot to visualize the distribution of urban and rural populations in the year 2000.

First, I set the figure size and then, created the boxplot using the new processed dataset, with `Population_Amount` as the y-axis and `Population_Type` as the x-axis.

        sns.set(rc={'figure.figsize':(8,6)})
        ax = sns.boxplot(data=df1,y='Population_Amount',x='Population_Type')

I then renamed the axes, set the title, and set tick labels so that there are comma seperators for thousands, making population values more readable.

        ax.set(ylabel='Population Amount')
        ax.set(xlabel='Population Type')
        ax.set_title("Distribution of Urban and Rural Populations in 2000")
        ax.get_yaxis().set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.0f}'))
        plt.show()
        
<p align="center">
<img src="/HW5/Resources/boxplot1.png" width="800">
</p>

Link to Chart: <a href= "https://colab.research.google.com/drive/153VaBggkMXGLEe8KKbDQVQjVxoLHJFux?usp=sharing">ipynb Notebook</a>

The boxplot effectively enables a comparison between urban and rural populations by seperately displaying major outliers. Notably, the boxplot represents these outliers as diamond markers rather than incorporating them within the standard box and whisker glyph. However, a drawback of the boxplot is the considerable amount of empty space due to these prominent outliers, leading to inefficiency in visual space utilization.

The boxplot makes it evident that urban populations significantly exceed rural populations, and it also highlights the presence of remarkable and conspicuous outliers within the urban population distribution.

### eCDF

For this chart, I used the Seaborn library to create a empirical cumulative distribution function (eCDF) plot to visualize the distribution of rural populations in the year 2000.

First, I created a new DataFrame that contained only the rural populations of each state.

        df_rural = df1[df1['Population_Type'] == 'Rural'].copy()
        df_rural.drop(df_rural.columns[[1]],axis=1,inplace=True)

Then, I set the figure size and then, created the eCDF using the new dataset, with `Population_Amount` as the x-axis.
        
        sns.set(rc={'figure.figsize':(10,6)})
        ax = sns.ecdfplot(data=df_rural, x='Population_Amount')

I then set the x-axis label, title, and x-axis tick labels so that there are comma seperators for thousands, making population values more readable.

        ax.set(xlabel='Rural Population',title='eCDF of Rural Population by State in 2000')
        ax.get_xaxis().set_major_formatter(mpl.ticker.StrMethodFormatter('{x:,.0f}'))
        plt.show()

<p align="center">
<img src="/HW5/Resources/ecdf1.png" width="800">
</p>

Link to Chart: <a href= "https://colab.research.google.com/drive/153VaBggkMXGLEe8KKbDQVQjVxoLHJFux?usp=sharing">ipynb Notebook</a>

This eCDF provides a visual representation of the distribution of rural population across states, making it easy to observe the spread and variation in population. One disadvantage of this chart is, it is a little difficult to tell what type of distribution the dataset has.

This chart shows that the majority of states have a relatively low rural population, considering the steep initial climb in the eCDF curve.

### Histogram

For this chart, I used the Seaborn Objects to create a histogram to visualize the distribution of rural populations in the year 2000.

First, I created the plot using the new dataset for rural populations and the `'Population_Amount'` column for the x-axis.

        (so.Plot(df_rural,"Population_Amount")

I played around with different binwidths to get a visually pleasing chart that accurately represents the data.

          .add(so.Bars(), so.Hist(binwidth=400000,binrange=(0,4000000)))

I then set the x- and y-axis labels and the title. I also adjusted the tick labels so that they were comma-seperated by thousands for better readability and adjusted the layout size.

          .label(y="count", x="population", title="Distribution of Rural Population by State in 2000")
          .scale(x=so.Continuous().label(like="{x:,.0f}"), y=so.Continuous().label(like="{x:,.0f}"))
          .layout(size=(10,6))
        )

<p align="center">
<img src="/HW5/Resources/histogram1.png" width="800">
</p>

Link to Chart: <a href= "https://colab.research.google.com/drive/153VaBggkMXGLEe8KKbDQVQjVxoLHJFux?usp=sharing">ipynb Notebook</a>

This histogram provided a straightforward way to visualize the frequency of states falling within specific rural population ranges, making it easy to identify density characteristics in the distribution. One drawback to the histogram is its sensitivity to choice of bin sizes. The distribution shape and characteristics varied greatly depending on the bin widths that I played around with.

The histogram revealed the presence of multiple modes in the rural distribution. It also shows that only a few states have large rural populations.

## Part 2: Further Analysis

After viewing the distribution of rural populations, I was curious as to how this distribution would compare with urban on an eCDF. To do this, I created a dual eCDF featuring one curve for urban populations and one for rural populations. The dual chart highlighted the presence of extreme outliers in the urban population distribution. It effectively demonstrated the significant contrast in urban population compared to the cumulative distribution of all rural populations.

<p align="center">
<img src="/HW5/Resources/ecdf2.png" width="800">
</p>

Link to Chart: <a href= "https://colab.research.google.com/drive/153VaBggkMXGLEe8KKbDQVQjVxoLHJFux?usp=sharing">ipynb Notebook</a>

Viewing rural and urban populations seperately led me to wonder if there was any correaltion, for instance, do states with higher urban populations tend to have lower rural populations? For this scatterplot, I decided to drop the upper half of states' urban populations to avoid a skewed chart. There was a somewhat positive correaltion between urban and rural states, suggesting that a state's total population amount affects both urban and rural populations.

<p align="center">
<img src="/HW5/Resources/scatterplot2.png" width="800">
</p>

Link to Chart: <a href= "https://colab.research.google.com/drive/153VaBggkMXGLEe8KKbDQVQjVxoLHJFux?usp=sharing">ipynb Notebook</a>

After gaining insight into states' rural and urban populations, I was interested to learn more about population density, or total population divided by state land area. To visualzie this, I created a choropleth map where the darker states represent more people per square mile.

I found a table in the same section of the Statistical Abstract of the United States, Table 13 - State Population--Rank, Percent Change, And Population Density. I performed similar Pandas processing steps as the original dataset to prepare for analysis.\
<a href="/HW5/Resources/10s0013.xls">Link to 'Before' Dataset</a> | <a href="/HW5/Resources/dens_df.csv">Link to 'After' Dataset</a>

The choropleth map revealed that smaller, coastal states typically had the greatest population density. It also showed that more rural areas had the lowest population density.

<p align="center">
<img src="/HW5/Resources/choropleth2.png" width="800">
</p>

Link to Chart: <a href= "https://colab.research.google.com/drive/153VaBggkMXGLEe8KKbDQVQjVxoLHJFux?usp=sharing">ipynb Notebook</a>

## References
* Statistical Abstract of the United States: 2012, https://www.census.gov/library/publications/2011/compendia/statab/131ed.html
* Understanding Pandas Melt — pd.melt(), https://pub.towardsai.net/understanding-pandas-melt-pd-melt-362954f8c125
* Histograms and eCDF’s: Practical Tips to reading them like a fourth grader, https://lazymodellingcrew.com/post/post_14_reading_like_a_fourthgrader_ta/
* Visualizing Distributions Examples in Python (Seaborn), https://github.com/odu-cs625-datavis/public-fall23-mcw/blob/main/vis_distributions_Python.ipynb
* Choropleth Maps using Plotly in Python, https://www.geeksforgeeks.org/choropleth-maps-using-plotly-in-python/#
