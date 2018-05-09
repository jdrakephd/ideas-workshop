<style>
.small-code pre code {
  font-size: 1em;
}
</style>

wrangling
========================================================
author: Ana I. Bento & John M. Drake
date: 
autosize: true

Reading in data (files and objects)
========================================================

Files: You've already seen the main command for reading in data from files -> `read.csv`

We can also use `read_csv` in much the same way. It's slightly faster and the resulting data frame is recognized as a tibble (more info: https://cran.r-project.org/web/packages/tibble/vignettes/tibble.html)



Reading in data (files and objects)
========================================================


Objects: We can read previously saved objects (incl. data frames) with the `load` command

For example, if you created a data frame called `df` that took a lot of time (e.g. from some slow simulation) then you could first save it:

- `save(df,file='get_df.Rda')`

..and later, load it again (e.g. when you start a new session and it's no longer in memory)

- `load('get_df.Rda')`

The file extension .Rda is short for Rdata (and you can use .Rdata as the extension, if you prefer)


The 'tidy data' format
========================================================

It is good practice to work with 'tidy data':

- Each variable has its own column
- Each observation has its own row
- Each value has its own cell


This involves a few commands from the `dplyr` package, particularly:

- gather
- select
- mutate



The 'tidy data' format
========================================================



Additionally, we often make use of string manipulation (`stringr` package), especially:

- str_replace_all
- paste (base R)

Otherwise, if someone takes the temperature in saint augustine, and someone counts the number of people on the beach at St. Augustine - how will their data ever be combined?

FIPS codes
========================================================

State and County-level US data are often referenced by FIPS codes (a bit like zip codes)

- California = 6
- Orange County (CA) = 59
- Full FIPS = 6059

- Georgia = 13
- Clarke County (GA) = 59
- Full FIPS = 13059



Piping
========================================================
**A) Run several functions**


```r
foo_foo <- hop(foo_foo, through = forest)
foo_foo <- scoop(foo_foo, up = field_mice)
foo_foo <- bop(foo_foo, on = head)
```

**B) String function calls together**


```r
bop(
  scoop(
    hop(foo_foo, through = forest),
    up = field_mice
  ), 
  on = head
)
```

**C) Use piping**


```r
foo_foo %>% hop(through = forest) %>% scoop(up = field_mouse) %>% bop(on = head)
```


Piping and assigning
========================================================


```r
x <- 2
y <- sqrt(sin(x))
y
```

```
[1] 0.9535709
```


```r
x <- 2
x <- sqrt(sin(x))
x
```

```
[1] 0.9535709
```



Piping and assigning
========================================================



```r
library(magrittr)
x <- 2
y <- x %>% sin %>% sqrt
y
```

```
[1] 0.9535709
```


```r
library(magrittr)
x <- 2
x %<>% sin %>% sqrt
x
```

```
[1] 0.9535709
```

Applying functions to each row
========================================================


```r
library(tidyverse)
library(magrittr)
pocket_money <- tibble(name=c("Jack","Jill"),
                       savings=c(10,15),chores=c(5,2)) %>% print
```

```
# A tibble: 2 x 3
  name  savings chores
  <chr>   <dbl>  <dbl>
1 Jack      10.     5.
2 Jill      15.     2.
```

Applying functions to each row
========================================================


```r
get_sum<-function(savings,chores){return(sum(savings,chores))}
pocket_money %>% rowwise %>% mutate(total=get_sum(savings,chores)) %>% print
```

```
Source: local data frame [2 x 4]
Groups: <by row>

# A tibble: 2 x 4
  name  savings chores total
  <chr>   <dbl>  <dbl> <dbl>
1 Jack      10.     5.   15.
2 Jill      15.     2.   17.
```

Applying functions to each row
========================================================



```r
get_sum<-function(savings,chores){return(sum(savings,chores))}
pocket_money %>% mutate(total=get_sum(savings,chores)) %>% print
```

```
# A tibble: 2 x 4
  name  savings chores total
  <chr>   <dbl>  <dbl> <dbl>
1 Jack      10.     5.   32.
2 Jill      15.     2.   32.
```


Combining data sets
========================================================

In base R, data frames are combined using the `merge` function

Using the `dplyr` package, tibbles are combined using `join` functions (https://cran.r-project.org/web/packages/dplyr/vignettes/two-table.html)

The different types of `join` are best explored by example, like with these superheros -> http://stat545.com/bit001_dplyr-cheatsheet.html

You can specifiy the column names to match on, otherwise R will do a _natural join_ using all variables in common


Combining data sets
========================================================


```r
gourmet <- tibble(
  state=c("GA","CA","NC","TX"),
  sauce=c("sweetBBQ","hot","tangyBBQ","smokyBBQ")
)

greeting <- tibble(
  state=c("TX","GA","CA","NY"),
  word=c("howdy","hey y'all","'sup","hello")
)

full_join(gourmet,greeting)
```

```
# A tibble: 5 x 3
  state sauce    word     
  <chr> <chr>    <chr>    
1 GA    sweetBBQ hey y'all
2 CA    hot      'sup     
3 NC    tangyBBQ <NA>     
4 TX    smokyBBQ howdy    
5 NY    <NA>     hello    
```


Combining data sets
========================================================


```r
gourmet <- tibble(
  state=c("GA","CA","NC","TX"),
  sauce=c("sweetBBQ","hot","tangyBBQ","smokyBBQ")
)

greeting <- tibble(
  state=c("TX","GA","CA","NY"),
  word=c("howdy","hey y'all","'sup","hello")
)

inner_join(gourmet,greeting)
```

```
# A tibble: 3 x 3
  state sauce    word     
  <chr> <chr>    <chr>    
1 GA    sweetBBQ hey y'all
2 CA    hot      'sup     
3 TX    smokyBBQ howdy    
```

Obtaining summary information
========================================================


```r
set.seed(123)
grades <- tibble(
  student_ID=as.character(1:10),
  major=sample(c("E","B"),10,replace=T),
  U_G=sample(c("U","G"),10,replace=T),
  score=sample(60:100,10,replace=T)
) %>% print
```

```
# A tibble: 10 x 4
   student_ID major U_G   score
   <chr>      <chr> <chr> <int>
 1 1          E     G        96
 2 2          B     U        88
 3 3          E     G        86
 4 4          B     G       100
 5 5          B     U        86
 6 6          E     G        89
 7 7          B     U        82
 8 8          B     U        84
 9 9          B     U        71
10 10         E     G        66
```

Obtaining summary information
========================================================



```r
grades %>% group_by(major) %>% summarize(avScore=mean(score))
```

```
# A tibble: 2 x 2
  major avScore
  <chr>   <dbl>
1 B        85.2
2 E        84.2
```




