Data Practical Week 6
================
Bastien Nespolo
2022-06-20

Welcome in this report ! This report will be do conjointly with my
friend Catia Reis Da Costa because we did an excellent work on joint
actions and coordination in A.Bangerter’s class and we want to use our
data to work a bit more with it again. We were collecting data to
compare interactive or non interactive learning. We made participants do
a paper plane and then we tested their flight’s performances by
measuring time and distance on three throws.

Here we load libraries to read our next folders.

``` r
library(dplyr)
```

    ## Warning: le package 'dplyr' a été compilé avec la version R 4.1.3

    ## 
    ## Attachement du package : 'dplyr'

    ## Les objets suivants sont masqués depuis 'package:stats':
    ## 
    ##     filter, lag

    ## Les objets suivants sont masqués depuis 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(ggplot2)
```

    ## Warning: le package 'ggplot2' a été compilé avec la version R 4.1.3

## Exclusive dataset

Now we can load our personal and exclusive dataset !

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

We can see that on this dataset we have 4 “integer” variables; 7
“numeric” variables and only one “character” variable which correspond
to the role of participant.

This dataset contains the measurements for each throw. We measured 3x
the distance and time for each plane and compared the performance of the
students and teachers. We can see averages that summarize the
performances. Finally, we also find feedbacks which correspond to the
number of times the participants interacted to improve the performance
of their plane. This condition only exists in the interactive learning
condition for the student role, as the teacher in the non-interactive
condition was alone with a computer.

### Questions about our data

Now I will formulate 2 questions about this dataset. 1.Do students
(interactive condition) have better performances than teachers
(non-interactive condition) ? 2.Does a high learning time involve better
performances ?

## Plot 1

For the first question we will do a boxplot to compare performances
between student and teacher. For this first plot we will only take the
distance measures.

``` r
ggplot(plane, aes(x=roles, y=average_distance, fill=roles)) + 
  geom_boxplot()
```

![](week-6_files/figure-gfm/boxplot%20Q1-distance-1.png)<!-- --> Now we
will take the flying time as measure for this first question.

``` r
ggplot(plane, aes(x=roles, y=average_flying_time, fill=roles)) + 
  geom_boxplot()
```

![](week-6_files/figure-gfm/boxplot%20Q1-time-1.png)<!-- --> ##
Explanation 1

What we can see in these graphs is that teachers are better in both
measurements. We can think is that an interactive condition seems not to
involves better performances. Maybe is because teachers were not good or
because students didn’t want to understand. Sorry for the prose it’s to
hard in a foreign language, I didn’t have the required luggage.

## Plot 2

For the second question we will do a scaterplot. We start by the average
of distance.

``` r
ggplot(plane, aes(learning_time,average_distance,label=rownames(plane),color=roles)) +
  geom_point() + labs(y ="learning_time" , x = "average_distance") + geom_text(hjust = -0.3)
```

![](week-6_files/figure-gfm/scaterplot%20Q2-distance-1.png)<!-- --> Now,
let do the same with the average of flying time.

``` r
ggplot(plane, aes(learning_time,average_flying_time,label=rownames(plane),color=roles)) +
  geom_point() + labs(y ="learning_time" , x = "average_flying_time") + geom_text(hjust = -0.3)
```

![](week-6_files/figure-gfm/scaterplot%20Q2-time-1.png)<!-- --> Mhhh… It
seems a bit complicated to be sure about the results. I will add a
regression line on my plots to ee if there are correlations, none or
negative correlations.

Let’s do it with the first; average of distance

``` r
ggplot(plane,aes(learning_time,average_distance, label=rownames(plane),color=roles)) +
    geom_point() + labs(y ="learning_time" , x = "average_distance") + geom_text(hjust = -0.3)+geom_smooth(method = "lm", se = TRUE,color="black")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](week-6_files/figure-gfm/scatterplot%20Q2-distance%20with%20line-1.png)<!-- -->
…And for the flying time.

``` r
ggplot(plane,aes(learning_time,average_flying_time, label=rownames(plane),color=roles)) +
    geom_point() + labs(y ="learning_time" , x = "average_flying_time") + geom_text(hjust = -0.3)+geom_smooth(method = "lm", se = TRUE,color="black")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](week-6_files/figure-gfm/scatterplot%20Q2-time%20with%20line-1.png)<!-- -->

## Explanation 2

Okay now we can see better. The learning time has not a positive
correlation on both measures (distance and time that the plane did). So
these results suggest that if you take more time to learn how to do your
plane it will not obviously be better. It should depend on something
else, maybe the manual performances of each participant, the quality of
the teacher (in interactive condition) or maybe the capacity of each
student to understand the teacher. We can also say that with the line
that we added on the 2 last plots, we can see no correlation for average
distance with learning time and a negative correlation with the average
of flying time. For this last result, I think it could be corrected with
a bigger sample.

# Conclusion

I hope you enjoyed this exclusive analysis. If you want to know more
about this study we can share our poster presentation.
