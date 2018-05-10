modeling
========================================================
author: Ana I. Bento & John M. Drake 
date: 
autosize: true

========================================================

```r
library(GGally); library(magrittr); data(cars) 
cars %>% ggpairs(columns=c("speed","dist"))
```

![plot of chunk unnamed-chunk-1](modeling-presentation-figure/unnamed-chunk-1-1.png)


========================================================

```r
library(dplyr); cars %<>% mutate(log10speed=log10(speed))
cars %>% ggpairs(columns=c("log10speed","dist"))
```

![plot of chunk unnamed-chunk-2](modeling-presentation-figure/unnamed-chunk-2-1.png)

Reproducibility and subsampling
========================================================

```r
x <- tibble(rnorm(10)) %>% print
```

```
# A tibble: 10 x 1
   `rnorm(10)`
         <dbl>
 1      -0.130
 2       0.394
 3      -0.558
 4       0.148
 5      -1.13 
 6       0.556
 7       1.10 
 8      -0.294
 9      -0.720
10       1.42 
```

Reproducibility and subsampling
========================================================

```r
x %>% sample_n(5)
```

```
# A tibble: 5 x 1
  `rnorm(10)`
        <dbl>
1      -0.558
2       1.10 
3       0.148
4       1.42 
5       0.394
```

Reproducibility and subsampling
========================================================

```r
x %>% sample_n(5)
```

```
# A tibble: 5 x 1
  `rnorm(10)`
        <dbl>
1      -0.130
2      -0.720
3      -0.294
4       0.394
5       0.148
```

Reproducibility and subsampling
========================================================

```r
set.seed(123); x %>% sample_n(5) #1st call
```

```
# A tibble: 5 x 1
  `rnorm(10)`
        <dbl>
1      -0.558
2      -0.294
3       0.148
4       1.10 
5       0.556
```

Reproducibility and subsampling
========================================================

```r
set.seed(123); x %>% sample_n(5) #2nd call
```

```
# A tibble: 5 x 1
  `rnorm(10)`
        <dbl>
1      -0.558
2      -0.294
3       0.148
4       1.10 
5       0.556
```

Linear modeling
========================================================

```r
library(ggplot2)
ggplot(cars)+geom_point(aes(speed,dist))+
  geom_smooth(aes(speed,dist),method="lm")
```

![plot of chunk unnamed-chunk-8](modeling-presentation-figure/unnamed-chunk-8-1.png)


Linear modeling
========================================================

```r
summary(lm(speed~dist,data=cars))
```

```

Call:
lm(formula = speed ~ dist, data = cars)

Residuals:
    Min      1Q  Median      3Q     Max 
-7.5293 -2.1550  0.3615  2.4377  6.4179 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)  8.28391    0.87438   9.474 1.44e-12 ***
dist         0.16557    0.01749   9.464 1.49e-12 ***
---
Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

Residual standard error: 3.156 on 48 degrees of freedom
Multiple R-squared:  0.6511,	Adjusted R-squared:  0.6438 
F-statistic: 89.57 on 1 and 48 DF,  p-value: 1.49e-12
```


Lists
========================================================

```r
y<-list(3.14,"eggs",lm(speed~dist,data=cars)) %>% print
```

```
[[1]]
[1] 3.14

[[2]]
[1] "eggs"

[[3]]

Call:
lm(formula = speed ~ dist, data = cars)

Coefficients:
(Intercept)         dist  
     8.2839       0.1656  
```


Correlation coefficients
========================================================

```r
cor.test(cars$speed,cars$dist,method="spearman")
```

```

	Spearman's rank correlation rho

data:  cars$speed and cars$dist
S = 3532.8, p-value = 8.825e-14
alternative hypothesis: true rho is not equal to 0
sample estimates:
      rho 
0.8303568 
```



modelr
========================================================

* create models from data
* store modeling information with data
* group and nest data for analysis
* un-nest for visualization

