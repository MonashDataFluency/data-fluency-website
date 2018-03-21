---
title: "05 Making Plots With ggplot"
date: 2018-02-23T13:28:03+11:00 
tags: [no_sidebar]
draft: false
teaching: 40
exercises: 50
questions:
    - " How can I visualize data in Python?"
    - " What is 'grammar of graphics'?"
objectives:
    - "Familiarise yourself with The Gramma of Graphics through plotinine library"
    - "Create a ggplot object."
    - "Explore different geom objects"
    - "Explore other layers of ggplot, including themes and labels"
keypoints:
    - "plotnine is python implementation of The Gramma of Graphics"
    - "ggplot is a set of gramma rules to make publication quality plots"
    - "ggplot has idea of layer, building a plot is just adding different layers together"
---

## Introduction

Python has powerful built-in plotting capabilities such as [`matplotlib`](https://matplotlib.org/), but with great power comes great complexity. For this exercise, we are going to use different python library, [`plotnine`](https://plotnine.readthedocs.io/en/stable/). There are a number of different libraries to choose from, but we are setting on [`plotnine`](https://plotnine.readthedocs.io/en/stable) as this is python port of original [`ggplot2`](http://ggplot2.org/) an R library (package), which is a very nice way to create publication quality plots and syntax is preserved, meaning you can take your python ggplot code and run it in R if you want it.
Strictly speaking [`plotnine`](https://plotnine.readthedocs.io/en/stable/) is just another implementation of [The Grammar of Graphics](http://link.springer.com/book/10.1007%2F0-387-28695-0) by Leland Wilkinson, which in theory could go on it own direction and diverge away from an R `ggplot` .

#### The Grammar of Graphics

> statistical graphic is a mapping from data to aesthetic attributes (colour, shape, size) of geometric objects (points, lines, bars)
> Faceting can be used to generate the same plot for different subsets of the dataset

These are basic building blocks according to the grammar of graphics:

- **data** The data + a set of aesthetic mappings that describing variables mapping
- **geom** Geometric objects, represent what you actually see on the plot: points, lines, polygons, etc.
- **stats** Statistical transformations, summarise data in many useful ways.
- **scale** The scales map values in the data space to values in an aesthetic space
- **coord** A coordinate system, describes how data coordinates are mapped to the plane of the graphic.
- **facet** A faceting specification describes how to break up the data into subsets for plotting individual set

Let's explore those in details

# Plotting in ggplot style

Let set up our working environment with necessary libraries and also load our csv file into data frame called `survs_df`,

```python
import numpy as np
import pandas as pd
from plotnine import *

%matplotlib inline
survs_df = pd.read_csv('data/surveys.csv').dropna()
```

Producing a plot with ggplot, we must give three things:

1. A data frame containing our data.
2. How the columns of the data frame can be translated into positions, colors, sizes, and shapes of graphical elements ("aesthetics").
3. The actual graphical elements to display ("geometric objects").

## Introduction to plotting

```python
ggplot(survs_df, aes('weight', 'hindfoot_length')) + geom_point()
```

Lets see if we can also include information about species and year

```python
ggplot(survs_df, aes('weight', 'hindfoot_length',
    size = 'year')) + geom_point()
```

```python
ggplot(survs_df, aes('weight', 'hindfoot_length', 
    size = 'year', color = 'species_id')) + geom_point()
```

We can do simple counting plot, to see how many observation (data points) we have for each year for example

```python
ggplot(survs_df, aes('year')) + \
    geom_bar(stat = 'count')
```

Let's now also color by species to see how many observation we have per species in a given year

```python
ggplot(survs_df, aes('year', fill = 'species_id')) + \
    geom_bar(stat = 'count')
```

## Challenges

> Is there a better visualisation for comparing weight across years? The plot should have categorical data on x axis and continuous on y axis
> Plot a boxplot of `hindfoot_length` across different species (`species_id` column)

## More geom types

```python
ggplot(survs_df, aes('year', 'weight')) + \
    geom_boxplot()
```
    
Why are we not seeing mulitple boxplots, one for each year?
This is because year variable is continues in our data frame, but for the purpose we want it to be categorical.

```python
survs_df['year_fact'] = pd.Series(survs_df['year'], dtype = "category")

ggplot(survs_df, aes('year_fact', 'weight')) + \
    geom_boxplot()
```

```python
ggplot(survs_df, aes('year_fact', 'weight')) + \
    geom_violin()
```

To save an image for later

```python
plt1 = ggplot(survs_df, aes('year_fact', 'weight')) + \
           geom_boxplot() + \
           xlab("Years") + \
           ylab("Weight log2(kg)") + \
           ggtitle("Boxplots, summary of species wieght in each year")

ggsave(filename = "plot1.png", \
       plot = plt1, \
       device = 'png', \
       dpi = 300, \
       height = 25, \
        width = 25)
```

## Challenges

> Can you log2 transform `weight` and plot "normalised" boxplot. Hint: use `np.log2()` function and name new column `weight_log`

Also will log2 transforming make this data visualisation better? 

```python
survs_df['weight_log'] = np.log2(survs_df['weight'])
    
ggplot(survs_df, aes('year_fact', 'weight_log')) + \
    geom_boxplot() + \
    xlab("Years") + \
    ylab("Weight log2(kg)") + \
    ggtitle("Boxplots, summary of species wieght in each year")
```

## Faceting

ggplot has a special technique called *faceting* that allows to split one plot
into multiple plots based on a factor included in the dataset. We will use it to
make one plot for a time series for each species.

```python
ggplot(survs_df, aes('year_fact', 'weight')) + \
    geom_boxplot() + \
    facet_wrap("~sex")

```

```python
ggplot(survs_df, aes('year_fact', 'weight_log')) + \
    geom_boxplot() + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1)) + \
    facet_wrap("~species_id") 
```

## Theming

```python
ggplot(survs_df, aes('year_fact', 'weight')) + \
    geom_boxplot() + \
    theme_bw()
```

```python
ggplot(survs_df, aes('year_fact', 'weight_log')) + \
    geom_boxplot() + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1)) + \
    facet_wrap("~species_id") + \
    theme_xkcd()
```

## Extra bits 1

Let's try to bin years into decades, which could be crude but might gives simple images to look at.

```python
bins = [(survs_df['year'] < 1980),
        (survs_df['year'] < 1990),
        (survs_df['year'] < 2000),
        (survs_df['year'] >= 2000)]

labels = ['70s', '80s', '90s', 'Z']

survs_df['year_bins'] = np.select(bins, labels)
```

```python
plt2 = ggplot(survs_df, aes('year_bins', 'weight_log')) + \
           geom_boxplot()
plt2 
```

```python
plt2 = ggplot(survs_df, aes('year_bins', 'weight_log')) + \
           geom_boxplot() + \
           theme(axis_text_x = element_text(angle = 90, hjust = 1)) + \
           facet_wrap("~species_id") 
plt2 
```

## Extra bits 2

This is a different way to look at your data

```python
ggplot(survs_df, aes("year_fact", "weight")) + \
    stat_summary(fun_y = np.mean, fun_ymin=np.min, fun_ymax=np.max) + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1))
    
ggplot(survs_df, aes("year_fact", "weight")) + \
    stat_summary(fun_y = np.median, fun_ymin=np.min, fun_ymax=np.max) + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1))
    
ggplot(survs_df, aes("year_fact", "weight_log")) + \
    stat_summary(fun_y = np.mean, fun_ymin=np.min, fun_ymax=np.max) + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1))
```
    
## Extra bits 3

It is very informative to look across years, year by year, it becomes apparent straight away that for some species there is a lot of data is missing.And going forward, maybe, you'd want to filter those low counting species. (this is after faceting by `species_id` in section [Extra bits 1](#extra-bits-1)).

```python
#survs_cnts_df = survs_df.groupby(['species_id'], as_index=False).count().sort_values(['record_id'])
survs_cnts_df = survs_df[['species_id']].groupby(['species_id']).size().reset_index()
species_to_remove = list(survs_cnts_df[survs_cnts_df['record_id'] < 200].species_id)
survs_df_filt = survs_df[survs_df['species_id'].isin(species_to_remove) == False]
```

```python
ggplot(survs_df_filt, aes('year_fact', 'weight_log')) + \
    geom_boxplot() + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1))

ggplot(survs_df_filt, aes('year_fact', 'weight_log')) + \
    geom_boxplot() + \
    theme(axis_text_x = element_text(angle = 90, hjust = 1)) + \
    facet_wrap("~species_id") 
```
