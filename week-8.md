Data Practical Week 8
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
library(ggplot2)
library(tibble)
library(cluster)
library(patchwork)
```

## Dataset and variables’check

In this report we will start by loading our dataset. I chose to take my
exclusive dataset that I create with my classmate Catia about paper
plane task (presented in reports of week 6). I think this dataset is
really good and fun for this exercise. Let’s load it.

``` r
plane<-read.table(file="plane.csv", header=TRUE, sep=";",dec=",") 
str(plane)
```

    ## 'data.frame':    20 obs. of  12 variables:
    ##  $ participants       : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ roles              : chr  "Teacher" "Student" "Teacher" "Student" ...
    ##  $ distance1          : int  180 405 760 420 540 310 220 500 580 410 ...
    ##  $ distance2          : int  270 420 430 240 580 230 450 550 610 430 ...
    ##  $ distance3          : int  360 540 430 280 410 580 210 230 480 520 ...
    ##  $ average_distance   : num  270 455 540 313 510 ...
    ##  $ time1              : num  1.17 0.92 2.66 1.8 2.17 2.11 1.41 2.42 2.23 2.04 ...
    ##  $ time2              : num  2.14 2.4 2.23 1.97 2.17 1.52 2.18 2.15 2.6 2.03 ...
    ##  $ time3              : num  2.33 1.07 2.23 1.46 1.17 2.62 1.78 2.2 1.92 2.04 ...
    ##  $ average_flying_time: num  1.88 1.46 2.37 1.74 1.84 2.08 1.79 2.26 2.25 2.04 ...
    ##  $ learning_time      : num  4 5.65 7.75 8.42 10.83 ...
    ##  $ feedback_percentage: num  NA 13.4 NA 26.3 NA ...

There are the same data from week 6. The dataset comes from
A.Bangerter’s class on coordination. We create this dataset to measure
if an interactive-learning (teacher to student; condition 2) produces
better performances rather than a non interactive-learning (Youtube to
student; condition 1).These different learning conditions were our
Explanatory variables. Performances was measured by recording paper
planes’ performances on 3 throws of a each paper plane created during
the learning condition. The flying time and distance traveled by each
plane were our measures and represent our Response variables.

## Correlations

Now we can see if there is a correlation between Explanatory and
Responses variables.

First I will create an exclusive value : “Performances” that I create by
multiplying the average distance with the average flying time. That’s
the performances for each participant.

``` r
performance<-plane$average_distance*plane$average_flying_time
str(performance)
```

    ##  num [1:20] 508 664 1280 545 938 ...

Now I will use this performances value to see if there is a correlation
between performances and learning time. I think that the learning time
is the best value to represent the different learning conditions. In
that way, I will correlate my performances (response variable) with a
value of different learning condition (explanatory variable). But first
I just need to create the average of learning time for each roles
(student which is learning condition 2 and teacher which is learning
condition 1).

``` r
student_learning_average<-plane%>% filter(roles=="Student")
mean(student_learning_average$learning_time)
```

    ## [1] 6.833

``` r
teacher_learning_average<-plane %>% filter(roles=="Teacher")
mean(teacher_learning_average$learning_time)
```

    ## [1] 6.914

The average of student learning time is 6.833 and the one for teachers
is 6.914… we will see if we use it.

Now we will know teacher’s performances.

``` r
performance_T<-teacher_learning_average$average_distance*teacher_learning_average$average_flying_time
```

And now we will know those for students.

``` r
performance_S<-student_learning_average$average_distance*student_learning_average$average_flying_time
```

Now I can correlate my performances (response variable) with learning
time (explanatory variable). Let’s do the correlation test

``` r
cor.test(performance_S, student_learning_average$learning_time, use = "complete.obs")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  performance_S and student_learning_average$learning_time
    ## t = -0.99244, df = 8, p-value = 0.35
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.7949908  0.3771590
    ## sample estimates:
    ##        cor 
    ## -0.3310913

…and now the same for teacher…

``` r
cor.test(performance_T, teacher_learning_average$learning_time, use = "complete.obs")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  performance_T and teacher_learning_average$learning_time
    ## t = -0.14821, df = 8, p-value = 0.8858
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.6602035  0.5969655
    ## sample estimates:
    ##         cor 
    ## -0.05232967

### Results discussion

The correlation between performances of students and their learning time
has a p-value = 0.35 which is not significant. The correlation between
performances of teachers and their learning time has p-value = 0.8858
which is not significant.

With these results, we can conclude that performances is independent of
learning time. There is no correlation between performances and learning
time. There is no causation in these correlations (which are not
significant and negatives). And even if correlations were significant,
we cannot say that there is a causation in a correlation. That’s two
separated things.

## Linear Model

Now, we will fit our model in a General Linear Model with all
performances and learning time.

``` r
predictor1<-lm(performance~plane$learning_time)
summary(predictor1)
```

    ## 
    ## Call:
    ## lm(formula = performance ~ plane$learning_time)
    ## 
    ## Residuals:
    ##     Min      1Q  Median      3Q     Max 
    ## -950.73 -572.10 -451.20   25.43 2409.68 
    ## 
    ## Coefficients:
    ##                     Estimate Std. Error t value Pr(>|t|)  
    ## (Intercept)          1733.83     686.82   2.524   0.0212 *
    ## plane$learning_time   -68.87      94.15  -0.732   0.4739  
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 1029 on 18 degrees of freedom
    ## Multiple R-squared:  0.02887,    Adjusted R-squared:  -0.02508 
    ## F-statistic: 0.5351 on 1 and 18 DF,  p-value: 0.4739

We can see that learning time is not a good predictor of performances.
(Results : plane$learning_time -68.87 94.15 -0.732 0.4739)

Now we can see it in a plot.

``` r
ggplot(plane,aes(performance,learning_time,label=rownames(plane),color=roles)) +
    geom_point() + labs(y ="Learning time (in minutes)" , x = "Plane's performance (in cm sec)") + geom_text(hjust = -0.4)+geom_smooth(method = "lm", se = TRUE,color="chartreuse")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](week-8_files/figure-gfm/plot%20of%20the%20linear%20model-1.png)<!-- -->

Now we can see the plot which shows to us the performance of each plane
on x axes (more is on the right, better it flown) and the learning time
of each participant on y axes (more is high, longer he/her learned). I
think this plot could have several problems. First the fact that the
unit cms (centimeters second) doesn’t really exist. Or a second problem
could be the fact that learning time is not a predictor of performance
and in this plot design, we could think that participant / plane number
8 has a good result because is high but in reality it was a bad
performance for a long learning time. I think the plot model doesn’t
describe better the data than the table in Linear Model part.

### Additional comments

Don’t hesitate to ask me more about this paper plane project if you
want. We have a poster to share in which you can scan a QR code and see
our data and our encoded interviews. Thanks to have read my reports ! I
hope you had fun.

Have a good end of day !

Bastien
