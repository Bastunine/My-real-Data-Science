Data Practical Week 4
================
Bastien Nespolo
2022-06-20

Welcome in this report ! Here we load libraries to read our next
folders.

``` r
library(readr)
library(dslabs)
library(dplyr)
library(knitr)
library(gapminder)
```

Now we will load our dataset about Orange.

``` r
data(Orange)
str(Orange)
```

    ## Classes 'nfnGroupedData', 'nfGroupedData', 'groupedData' and 'data.frame':   35 obs. of  3 variables:
    ##  $ Tree         : Ord.factor w/ 5 levels "3"<"1"<"5"<"2"<..: 2 2 2 2 2 2 2 4 4 4 ...
    ##  $ age          : num  118 484 664 1004 1231 ...
    ##  $ circumference: num  30 58 87 115 120 142 145 33 69 111 ...
    ##  - attr(*, "formula")=Class 'formula'  language circumference ~ age | Tree
    ##   .. ..- attr(*, ".Environment")=<environment: R_EmptyEnv> 
    ##  - attr(*, "labels")=List of 2
    ##   ..$ x: chr "Time since December 31, 1968"
    ##   ..$ y: chr "Trunk circumference"
    ##  - attr(*, "units")=List of 2
    ##   ..$ x: chr "(days)"
    ##   ..$ y: chr "(mm)"

## Filter

Now that we have our dataset about this wonderful fruit, we will filter
Orange’s dataset to see which tree is aged over 1000 years, I’m really
impressed by them ! I’m also interested by their circumferences, so let
filter those bigger than 200 cm.

``` r
Orange_filter<- Orange %>% filter(age>1000, circumference>200)
```

Now we will select a subset of the column. We will look at Trees even if
they are written by numbers and age.

``` r
Orange_select <- Orange_filter %>% select(Tree, age)
```

Now, we can have a look on the first rows displayed. Head shows us the
first lines but in that case, there are few lines so we will see the
same.

``` r
head(Orange_select)
```

    ##   Tree  age
    ## 1    2 1372
    ## 2    2 1582
    ## 3    4 1372
    ## 4    4 1582

Okay, has we said, we already have seen this rows because only few tree
are very old. But anyway, now we will just see the law rows, just to see
them again.

``` r
tail(Orange_select)
```

    ##   Tree  age
    ## 1    2 1372
    ## 2    2 1582
    ## 3    4 1372
    ## 4    4 1582

Now we will see the structure of data.

``` r
str(Orange_select)
```

    ## Classes 'nfnGroupedData', 'nfGroupedData', 'groupedData' and 'data.frame':   4 obs. of  2 variables:
    ##  $ Tree: Ord.factor w/ 5 levels "3"<"1"<"5"<"2"<..: 4 4 5 5
    ##  $ age : num  1372 1582 1372 1582

So, now we will organize trees with their ages and order them to be to
the younger to the oldest between the four.

``` r
Orange_arranged <-Orange_select %>% arrange(age)
```

### Discussion

Now we can discuss what we see in this arrangement. It’s a bit hard to
say a lot of things because they re few data with this age selected, but
anyway, what we can see is that trees are alternated (2,4,2,4) and that
2 have the same age and also the two others.

Now it could be interesting to summarize our results, in case we need
once time. Even if they are not too much, we can show how to do in order
to reproduce it when our dataset will be bigger. For this case we will
see which tree is the oldest and which has the biggest circumference.

``` r
oldest<- Orange%>% group_by(Tree)%>%summarize(mean_age=mean(age))
```

WoW! The nature is wonderful ! She made that each tree has the same mean
of age. Personally I think that this dataset was made by an algorithm.
Let see if it’s the same case for circumferences.

``` r
biggest <- Orange%>% group_by(Tree)%>%summarize(mean_circumference=mean(circumference))
```

Okay, I prefer this kind of results. Here we can see that trees “4” have
the highest mean for their circumferences and that trees “3” the
smallest. I really wonder what is the difference between these trees…. I
think that I couldn’t tell you…

Okay now we will display the result arranged by a column of interest,
like circumference because it’s the most relevant to organize. And we
will say that the biggest tree will be on the first row. …

``` r
biggest%>%arrange(desc(mean_circumference))
```

    ## # A tibble: 5 x 2
    ##   Tree  mean_circumference
    ##   <ord>              <dbl>
    ## 1 4                  139. 
    ## 2 2                  135. 
    ## 3 5                  111. 
    ## 4 1                   99.6
    ## 5 3                   94

Big respect to tree number 4 !

<img src="https://thumbs.dreamstime.com/z/arbre-de-no%C3%ABl-fort-athl%C3%A8te-d-arbre-de-bodybuilder-avec-le-grand-muscle-63511630.jpg" style="width:30.0%" />
Now we will see if we have NA value.

``` r
any(is.na(Orange))
```

    ## [1] FALSE

False means that we don’t have NA value, but if it was the case, I would
use the formula filter(!is.na(column concerned)) with the correct
entries for the column concerned.

Now, we will add 2 datasets which are results_us_election_2016 and
murders.

``` r
full_join(results_us_election_2016, murders)
```

    ## Joining, by = "state"

    ##                   state electoral_votes clinton trump others abb        region
    ## 1            California              55    61.7  31.6    6.7  CA          West
    ## 2                 Texas              38    43.2  52.2    4.5  TX         South
    ## 3               Florida              29    47.8  49.0    3.2  FL         South
    ## 4              New York              29    59.0  36.5    4.5  NY     Northeast
    ## 5              Illinois              20    55.8  38.8    5.4  IL North Central
    ## 6          Pennsylvania              20    47.9  48.6    3.6  PA     Northeast
    ## 7                  Ohio              18    43.5  51.7    4.8  OH North Central
    ## 8               Georgia              16    45.9  51.0    3.1  GA         South
    ## 9              Michigan              16    47.3  47.5    5.2  MI North Central
    ## 10       North Carolina              15    46.2  49.8    4.0  NC         South
    ## 11           New Jersey              14    55.5  41.4    3.2  NJ     Northeast
    ## 12             Virginia              13    49.8  44.4    5.8  VA         South
    ## 13           Washington              12    54.3  38.1    7.6  WA          West
    ## 14              Arizona              11    45.1  48.7    6.2  AZ          West
    ## 15              Indiana              11    37.8  56.9    5.3  IN North Central
    ## 16        Massachusetts              11    60.0  32.8    7.2  MA     Northeast
    ## 17            Tennessee              11    34.7  60.7    4.6  TN         South
    ## 18             Maryland              10    60.3  33.9    5.8  MD         South
    ## 19            Minnesota              10    46.4  44.9    8.6  MN North Central
    ## 20             Missouri              10    38.1  56.8    5.1  MO North Central
    ## 21            Wisconsin              10    46.5  47.2    6.3  WI North Central
    ## 22              Alabama               9    34.4  62.1    3.6  AL         South
    ## 23             Colorado               9    48.2  43.3    8.6  CO          West
    ## 24       South Carolina               9    40.7  54.9    4.4  SC         South
    ## 25             Kentucky               8    32.7  62.5    4.8  KY         South
    ## 26            Louisiana               8    38.4  58.1    3.5  LA         South
    ## 27          Connecticut               7    54.6  40.9    4.5  CT     Northeast
    ## 28             Oklahoma               7    28.9  65.3    5.7  OK         South
    ## 29               Oregon               7    50.1  39.1   10.8  OR          West
    ## 30             Arkansas               6    33.7  60.6    5.8  AR         South
    ## 31                 Iowa               6    41.7  51.1    7.1  IA North Central
    ## 32               Kansas               6    36.1  56.7    7.3  KS North Central
    ## 33          Mississippi               6    40.1  57.9    1.9  MS         South
    ## 34               Nevada               6    47.9  45.5    6.6  NV          West
    ## 35                 Utah               6    27.5  45.5   27.0  UT          West
    ## 36             Nebraska               5    34.3  59.9    5.8  NE North Central
    ## 37           New Mexico               5    48.3  40.0   11.7  NM          West
    ## 38        West Virginia               5    26.5  68.6    4.9  WV         South
    ## 39               Hawaii               4    62.2  30.0    7.7  HI          West
    ## 40                Idaho               4    27.5  59.3   13.2  ID          West
    ## 41                Maine               4    48.0  45.0    7.0  ME     Northeast
    ## 42        New Hampshire               4    46.8  46.5    6.7  NH     Northeast
    ## 43         Rhode Island               4    54.4  38.9    6.7  RI     Northeast
    ## 44               Alaska               3    36.6  51.3   12.2  AK          West
    ## 45             Delaware               3    53.4  41.9    4.7  DE         South
    ## 46              Montana               3    35.9  56.5    7.6  MT          West
    ## 47         North Dakota               3    27.2  63.0    9.8  ND North Central
    ## 48         South Dakota               3    31.7  61.5    6.7  SD North Central
    ## 49              Vermont               3    56.7  30.3   13.1  VT     Northeast
    ## 50              Wyoming               3    21.9  68.2   10.0  WY          West
    ## 51 District of Columbia               3    90.9   4.1    5.0  DC         South
    ##    population total
    ## 1    37253956  1257
    ## 2    25145561   805
    ## 3    19687653   669
    ## 4    19378102   517
    ## 5    12830632   364
    ## 6    12702379   457
    ## 7    11536504   310
    ## 8     9920000   376
    ## 9     9883640   413
    ## 10    9535483   286
    ## 11    8791894   246
    ## 12    8001024   250
    ## 13    6724540    93
    ## 14    6392017   232
    ## 15    6483802   142
    ## 16    6547629   118
    ## 17    6346105   219
    ## 18    5773552   293
    ## 19    5303925    53
    ## 20    5988927   321
    ## 21    5686986    97
    ## 22    4779736   135
    ## 23    5029196    65
    ## 24    4625364   207
    ## 25    4339367   116
    ## 26    4533372   351
    ## 27    3574097    97
    ## 28    3751351   111
    ## 29    3831074    36
    ## 30    2915918    93
    ## 31    3046355    21
    ## 32    2853118    63
    ## 33    2967297   120
    ## 34    2700551    84
    ## 35    2763885    22
    ## 36    1826341    32
    ## 37    2059179    67
    ## 38    1852994    27
    ## 39    1360301     7
    ## 40    1567582    12
    ## 41    1328361    11
    ## 42    1316470     5
    ## 43    1052567    16
    ## 44     710231    19
    ## 45     897934    38
    ## 46     989415    12
    ## 47     672591     4
    ## 48     814180     8
    ## 49     625741     2
    ## 50     563626     5
    ## 51     601723    99

This relation shows the tendency to each state to vote for Clinton or
Trump.
