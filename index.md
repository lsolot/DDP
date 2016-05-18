---
title       : MPG Predictor for mtcars Data 
subtitle    : Using Weight, Horsepower and Transmission Type
author      : Lou Solot
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Method

1. Use Linear Regression to find the variables that can predict MPG
2. Build a prediction model using those variables
3. Create a shiny app that enables users to input those variables in order to predict MPG
4. Include the mtcars table so that users can compare their result to the real data

```r
sort(cor(mtcars)[1,])
```

```
##         wt        cyl       disp         hp       carb       qsec 
## -0.8676594 -0.8521620 -0.8475514 -0.7761684 -0.5509251  0.4186840 
##       gear         am         vs       drat        mpg 
##  0.4802848  0.5998324  0.6640389  0.6811719  1.0000000
```

This correlation shows that wt, hp, am, cyl and disp are all highly correlated with mpg

--- .class #id 

## Eliminate Variables Highly correlated with Each Other

```r
sort(cor(mtcars)[4,])
```

```
##        mpg         vs       qsec       drat         am       gear 
## -0.7761684 -0.7230967 -0.7082234 -0.4487591 -0.2432043 -0.1257043 
##         wt       carb       disp        cyl         hp 
##  0.6587479  0.7498125  0.7909486  0.8324475  1.0000000
```

We can eliminate hp and disp since predictors should not be highly correlated with each other

--- .class #id

## Build the Model Using Weight, Horsepower and Transmission Type


```r
pred <- lm(mpg ~ am + wt + hp, data = mtcars)
summary(pred)$coef
```

```
##                Estimate  Std. Error   t value     Pr(>|t|)
## (Intercept) 34.00287512 2.642659337 12.866916 2.824030e-13
## am           2.08371013 1.376420152  1.513862 1.412682e-01
## wt          -2.87857541 0.904970538 -3.180850 3.574031e-03
## hp          -0.03747873 0.009605422 -3.901830 5.464023e-04
```

--- .class #id

## Plots


```r
par(mfrow = c(2,2))
plot(pred)
```

![plot of chunk unnamed-chunk-4](assets/fig/unnamed-chunk-4-1.png)

--- .class #id

## Conclusion


```r
summary(pred)$r.squared
```

```
## [1] 0.8398903
```

* This model explains ~84% of the variance
* This shows that the combination of weight, horsepower and transmission type is a good predictor of mpg
