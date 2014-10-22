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

The data was extracted from the 1974 Motor Trend US magazine, and comprises fuel consumption and 10 aspects of automobile design and performance for 32 automobiles (1973–74 models).  

The variables that I have decided to use to predict *MPG* are *Number of cylinders* and *Weight (lb/1000)*.        

### Result:   
86% of the variation in mpg is explained by the model.          
* 4 cylinder car: for every 1000 lb increase in the car's weight, the mpg decrease by 5.4 miles per gallon.      
* 6 cylinder car: for every 1000 lb increase in the car's weight, the mpg decrease by 3.8 miles per gallon.      
* 8 cylinder car: for every 1000 lb increase in the car's weight, the mpg decrease by 2.2 miles per gallon.

---

## Exploratory Analysis

The following is an exploratory graphs between **MPG**,**Weight** and **Number of Cylinder**:    


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
summary(lm(mpg~cyl*wt,data=mtcars))
```

```
## 
## Call:
## lm(formula = mpg ~ cyl * wt, data = mtcars)
## 
## Residuals:
##    Min     1Q Median     3Q    Max 
## -4.229 -1.350 -0.504  1.465  5.234 
## 
## Coefficients:
##             Estimate Std. Error t value Pr(>|t|)    
## (Intercept)   54.307      6.128    8.86  1.3e-09 ***
## cyl           -3.803      1.005   -3.78  0.00075 ***
## wt            -8.656      2.320   -3.73  0.00086 ***
## cyl:wt         0.808      0.327    2.47  0.01988 *  
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 2.37 on 28 degrees of freedom
## Multiple R-squared:  0.861,	Adjusted R-squared:  0.846 
## F-statistic: 57.6 on 3 and 28 DF,  p-value: 4.23e-12
```

    



