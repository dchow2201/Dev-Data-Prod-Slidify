---
title       : Developing Data Products Project 
subtitle    : Reproducible Pitch Presentation 
author      : David Chow
job         : The following is a pitch presentation for the mpg predictition application. 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## User's Instruction

User first need to supply some information about their car on the left panel.      
1. They must enter the number of cylinders their cars has, the choices are 4, 6, or 8.       
2. They need to specify the weight of their car using the slider. The weight is enter in the unit of per 1000 lbs. So if the car weight 3000 lb, then the user will enter 3.     
      
After the user specified their inputs, they can press the Submit button to render their mpg prediction. The prediction result is shown on the right panel. The unit of the predicted mpg is in miles per gallon.

---

## Prediction method

The prediction model is generated using the mtcars data set provided in R    

```r
head(mtcars,3)
```

```
##                mpg cyl disp  hp drat    wt  qsec vs am gear carb
## Mazda RX4     21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
## Mazda RX4 Wag 21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
## Datsun 710    22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
```

The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models).  

The variables that I have decided to use to predict *MPG* are *Number of cylinders* and *Weight (lb/1000)*.   

---

## Exploratory Analysis

The following is an exploratory graphs of the three variables:

```r
library(ggplot2)
qplot(wt,mpg,data=mtcars,geom=c("point","smooth"),
      method="lm", formula=y~x, facets=.~cyl,
      xlab="Weight (lb/1000)",ylab="Miles per Gallon")
```

![plot of chunk ggplot](assets/fig/ggplot.png) 


---

## Linear Model

The following is the summary of the linear regression model.   

```r
summary(lm(mpg~cyl+wt,data=mtcars))
```

```
## 
## Call:
## lm(formula = mpg ~ cyl + wt, data = mtcars)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -4.289 -1.551 -0.468  1.574  6.100 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   39.686      1.715   23.14  < 2e-16 ***
## cyl           -1.508      0.415   -3.64  0.00106 ** 
## wt            -3.191      0.757   -4.22  0.00022 ***
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.57 on 29 degrees of freedom
## Multiple R-squared:  0.83,	Adjusted R-squared:  0.819 
## F-statistic: 70.9 on 2 and 29 DF,  p-value: 6.81e-12
```

83% of the variation in mpg is explained by the model.    
While holding the number of cylinders in the car constant (4,6 or 8), for every 1000 lb increase in the car's weight, the mpg decrease by 3.2 miles per gallon.          



