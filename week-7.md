Data Practical Week 7
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

## Dataset

Now that I load some libraries I select a dataset about animal I can
describe the variables. First I will indicate the meaning of the
variables with the help of this source. If you click
[here](https://stat.ethz.ch/R-manual/R-devel/library/cluster/html/animals.html)
you can check the website which gave me these information.

``` r
data(animals)
str(animals)
```

    ## 'data.frame':    20 obs. of  6 variables:
    ##  $ war: int  1 1 2 1 2 2 2 2 2 1 ...
    ##  $ fly: int  1 2 1 1 1 1 2 2 1 2 ...
    ##  $ ver: int  1 1 2 1 2 2 2 2 2 1 ...
    ##  $ end: int  1 1 1 1 2 1 1 2 2 1 ...
    ##  $ gro: int  2 2 1 1 2 2 2 1 2 1 ...
    ##  $ hai: int  1 2 2 2 2 2 1 1 1 1 ...

## Meanings of variables

1.  war = warm-blooded
2.  fly = can fly
3.  ver = vertebrate
4.  end = endangered
5.  gro = live in groups
6.  hai = have hair

Variables are encoded as 1 = no, 2 = yes

Here is a list of these 20 animals observed. This list has been found
[here](http://www.ru.ac.bd/stat/wp-content/uploads/sites/25/2019/03/503_09_Kaufman_Finding-Groups-in-Data-An-Introduction-to-Cluster-Analysis.pdf).
The list : ant, bee, cat, caterpillar, chimpanzee, cow, duck, eagle,
elephant, fly, frog, herring, lion, lizard, lobster, man, rabbit,
salmon, spider, and whale.

## Describing variables

All my variables are “integer”. Even if they are coded by numerical and
entire numbers, they represent if yes or no they have the attribute of
animal which correspond to a qualitative variable.

## Visualize the data

Now I will create several plots to see at which frequency an attribute
is present in all animals. For that, I will use Barplots. Don’t forget
that 1 means no and 2 means yes. So for the second graph we can see that
16 animals don’t fly and 4 animals fly.

``` r
a<-ggplot(animals,aes(war)) + geom_bar() + scale_y_continuous(limits = c(0, 20))
b<-ggplot(animals,aes(fly)) + geom_bar() + scale_y_continuous(limits = c(0, 20))
c<-ggplot(animals,aes(ver)) + geom_bar() + scale_y_continuous(limits = c(0, 20))
d<-ggplot(animals,aes(end)) + geom_bar() + scale_y_continuous(limits = c(0, 20))
e<-ggplot(animals,aes(gro)) + geom_bar() + scale_y_continuous(limits = c(0, 20))
f<-ggplot(animals,aes(hai)) + geom_bar() + scale_y_continuous(limits = c(0, 20))

a+b+c+d+e+f
```

    ## Warning: Removed 2 rows containing non-finite values (stat_count).

    ## Warning: Removed 3 rows containing non-finite values (stat_count).

![](week-7_files/figure-gfm/barplot%20frequency%20of%20attributes-1.png)<!-- -->

## Hypothesis

I’m wonder if warm-blooded animals are less endanger than those that are
not ? H0 will be that there is no correlation between warm-blood and
endangered.

Or maybe those who lived in groups are less endangered than those who
don’t ? H0 will be that living in group is not correlated with being
endangered.

## Statisticals tests and analysis

We will use a correlation test between (1) warm-blooded and endangered
animals and (2) between groups animal living in groups and endangered
animals. The correlation test will tell us if having a warm-blood
influences the survival of the species and in a second time if the fact
that a species lives in group influences the fact that the species is
endangered. Let’s do these correlations tests.

``` r
cor.test(animals$war, animals$end, use = "complete.obs")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  animals$war and animals$end
    ## t = 2.1381, df = 16, p-value = 0.04829
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  0.005814025 0.769024169
    ## sample estimates:
    ##       cor 
    ## 0.4714045

The results for this first correlation test is significant. The p-value
= 0.04829 so less than 0,05 which means that having warm-blooded seems
to correlate with the endangerment of the species. Therefore, H0 is
rejected.

Let’s do the same for the second correlation test.

``` r
cor.test(animals$gro, animals$end, use = "complete.obs")
```

    ## 
    ##  Pearson's product-moment correlation
    ## 
    ## data:  animals$gro and animals$end
    ## t = 0.73598, df = 13, p-value = 0.4748
    ## alternative hypothesis: true correlation is not equal to 0
    ## 95 percent confidence interval:
    ##  -0.3479068  0.6460712
    ## sample estimates:
    ## cor 
    ## 0.2

For these second results, we can see that the correlation test tells us
that p-value = 0.4748. In that way, it means that living in group is not
correlated with the endangerment of the species. Therefore H0 can not be
rejected.

Thanks and be happy to being part of a warm-blooded species !
