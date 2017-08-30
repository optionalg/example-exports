---
title: Introduction
key: cd230e1e79cb6f2b8f6d98892633810a
video_link:
    hls: https://videos.datacamp.com/transcoded/3094_lattice/v3/hls-ch1_1.master.m3u8
    mp4: https://videos.datacamp.com/transcoded_mp4/3094_lattice/v3/ch1_1.mp4
transformations:
    translateX: 70
    translateY: -6
    scale: 1.30

--- type:TitleSlide key:d95e80ee26
## Welcome to the course


*** =lower_third
name: Deepayan Sarkar
title: Associate Professor, Indian Statistical Institute



*** =script

Welcome to the course



--- type:FullSlide key:88c2071d19
## Data visualization

*** =part1

* Exploratory data analysis {{1}}

* Presenting or reporting results {{2}}


*** =script

Data visualization is an essential tool for any data analyst. 

It's important for exploratory data analysis, where you try to find and understand patterns in your data as quickly as possible. 

It's also important when presenting or reporting your results, but in that case, clarity and ease of customization are more important than speed.


--- type:FullSlide key:4155d27431
## Data visualization frameworks in R

*** =part1

* Base R graphics {{1}}

* `lattice` based on "Trellis graphics" (Cleveland) {{2}}

* `ggplot2` based on "Grammar of Graphics" (Wilkinson) {{3}}


Number of packages depending on these (March 2017): {{4}}


|         | graphics| lattice| ggplot2|
|---------|---------|--------|--------|
|CRAN     |     5612|    3654|    1566|
|CRAN+BioC|     7889|    4858|    2038| {{4}}



*** =script


There are many R packages for data visualization, but most of them are based on one of three graphics frameworks.

The first one is base R graphics, which has been available in R from the beginning, and provides a rich collection of tools. However, it's not very flexible. 

Lattice graphics is in some ways a successor to base graphics, and tries to address many of its shortcomings. 

The third and newest framework is based on the `ggplot2` package.

[NextOverlay]

All these frameworks are complete by themselves, but they are also important because of the large eco-system of packages built around them.

In this course, you'll learn to use lattice graphics, for both exploration and presentation. 

--- type:FullSlide key:22ce55bc0f
## The `USCancerRates` dataset

*** =part1

* Age-adjusted death rates due to cancer (per 100,000)

* Separately for males and females

* County-level data for 1999-2003

* Available in the `latticeExtra` package


*** =script

In the first couple of chapters, you'll use a dataset that records death-rates due to cancer, at the US county level, separately for males and females. 

--- type:FullSlide key:7bfe6ac8c8
## The `USCancerRates` dataset

*** =part1

```r
> library(lattice)
> data(USCancerRates, package = "latticeExtra")
> str(USCancerRates)
```

```
'data.frame':	3041 obs. of  8 variables:
 $ rate.male   : num  364 346 341 336 330 ...
 $ LCL95.male  : num  311 274 304 289 293 ...
 $ UCL95.male  : num  423 431 381 389 371 ...
 $ rate.female : num  151 140 182 185 172 ...
 $ LCL95.female: num  124 103 161 157 151 ...
 $ UCL95.female: num  184 190 206 218 195 ...
 $ state       : Factor w/ 49 levels "Alabama","Alaska",..: 1 1 1 1 1 ...
 $ county      : chr [1:3041] "Pickens County" "Bullock County" ...
```


*** =script

The main variable of interest is the annual rate of death due to cancer. State is also available as a covariate. 

Your goal will be to explore how the _distribution_ of death-rate varies with gender and location.

--- type:FullSlide key:ffe97fff06
## A histogram

*** =part1

```r
> histogram(~ rate.male, data = USCancerRates)
```

![](http://www.isid.ac.in/~deepayan/tmp/figures/ch1-hist1-1.png)

*** =script

Here is a familiar plot: the histogram. 

Histograms show the distribution of a continuous variable, which in this case is the death-rate among males. 

This histogram is not particularly exciting; later we'll improve on it.


--- type:FullSlide key:1a53207a8d
## A scatter plot

*** =part1

```r
> xyplot(rate.female ~ rate.male, data = USCancerRates)
```


![](http://www.isid.ac.in/~deepayan/tmp/figures/ch1-xy1-1.png)


*** =script

Here's another familiar visualization: a scatter plot. 

This one shows the death-rates among females versus males, where each circle represents the rates corresponding to one county. 

The plot suggests that the rates are correlated, and that there are some possible outliers, but otherwise it's not remarkable. 

--- type:FullSlide key:01751028d6
## The formula

*** =part1

```r
histogram(~ rate.male, data = USCancerRates)
xyplot(rate.female ~ rate.male, data = USCancerRates)
```

* ` ~ x` in `histogram()`:  `x` plotted on $x$-axis

* `y ~ x` in `xyplot()`:
	* `x` plotted on $x$-axis
	* `y` plotted on $y$-axis


Similar to modeling calls {{1}}
```r
lm(rate.female ~ rate.male, data = USCancerRates)
``` {{1}}



*** =script

These two plots are produced by the lattice functions histogram() and xyplot().

They are similar to base R graphics functions hist() and plot() respectively, but one important difference is in how the variables in the plot are specified.

The lattice functions take a formula and a data frame as inputs. 

The left hand side of the formula names variables on the y axis, and the right-hand side names variables on the x axis. 

A histogram does not need the y axis to be specified, so the left hand side remains blank in that case.

[NextOverlay]

The main advantage of the formula interface is that it lets you compactly describe the plot without making all the variables in the dataset visible in the workspace. 

This is similar to modeling functions such as `lm()`, like in this call to fit a linear regression model with `rate.female` as response and `rate.male` as predictor. 

--- type:FullSlide key:73cf187762
## A version for presentation

*** =part1


![](http://www.isid.ac.in/~deepayan/tmp/figures/ch1-xyPresentation-1.png)


*** =script

The plots you just saw are very minimal. Such minimal plots are usually sufficient for exploration, but for presentation purposes, plots needs to be more polished.

For example, here's a more elaborate version of the previous scatter plot. It has more descriptive labels, a reference grid, and a reference line along the "y equals x" diagonal.

This makes one point very clear that was hard to see in the earlier scatter plot. 

In absolute terms, the death-rate in females is substantially lower than in males, for almost all counties.

Throughout the course, you'll learn how to customize your lattice plots in different ways.

Now you go on to draw some histograms and scatter plots.



--- type:FinalSlide key:60e819e9de
## Let's practice!
