Data Practical Week 3
================
Bastien Nespolo
2022-06-20

Welcome in this report ! Here we load libraries to read our next
folders.

``` r
library(readr)
library(dslabs)
```

## Dataset number 1 !

We will start by load our first dataset. I chose orange because it’s a
fruit that I really appreciate and it’s the tree that I prefer.

In this dataset we have information about Trees, their circumferences
and their ages. Respectively according to Qualitative (nominal) ,
Quantitative (discrete) and Quantitative (discrete) categories. Just to
precise my opinion, even if it’s tree is represented by a number I
presuppose that researchers have this number attributed to a category of
tree as “pine” so for me Tree is a qualitative variable

Now, with the formula str we have an overview of variables.

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

## Dataset number 2 !

Now we will load a second dataset from an external source. Let’s do it !

In this table we can also see all types of variables and details about
them.

We can see that the only integer variable is X. Then, that Ingredient,
Text, Recipe index and unit are characters variables. Finally, rating
and quantity are numerical variables.

Qualitative variables are : Ingredient (nominal), Text (nominal), Recipe
Index (nominal), Unit (nominal) Quantitative variables are : Rating
(continuous), Quantity (discrete)

``` r
cookies<-read.csv("https://raw.githubusercontent.com/the-pudding/data/master/cookies/choc_chip_cookie_ingredients.csv")
str(cookies)
```

    ## 'data.frame':    1990 obs. of  7 variables:
    ##  $ X           : int  1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Ingredient  : chr  "all purpose flour" "all purpose flour" "all purpose flour" "all purpose flour" ...
    ##  $ Text        : chr  "3.0 cups all purpose flour" "2.8000000000000003 cups all purpose flour" "1.1076923076923078 cups all purpose flour" "3.333333333333333 cups sifted all purpose flour" ...
    ##  $ Recipe_Index: chr  "AR_1" "AR_10" "AR_101" "AR_102" ...
    ##  $ Rating      : num  0.921 0.905 0.6 0.938 0.881 ...
    ##  $ Quantity    : num  3 2.8 1.11 3.33 2 ...
    ##  $ Unit        : chr  "cup" "cup" "cup" "cup" ...

# Dataset number 3 !

Now we will load a third and last dataset from the library dslabs.

Here we can analyse our stars variables. We can see that stars’ names is
a Qualitative (nominal) categories. Magnitude is Quantitative
(continuous), temp is Quantitative (discrete) and type is Qualitative
(nominal).

``` r
data(stars)
str(stars)
```

    ## 'data.frame':    96 obs. of  4 variables:
    ##  $ star     : Factor w/ 95 levels "*40EridaniA",..: 87 85 48 38 33 92 49 79 77 47 ...
    ##  $ magnitude: num  4.8 1.4 -3.1 -0.4 4.3 0.5 -0.6 -7.2 2.6 -5.7 ...
    ##  $ temp     : int  5840 9620 7400 4590 5840 9900 5150 12140 6580 3200 ...
    ##  $ type     : chr  "G" "A" "F" "K" ...

Okay, now we see that we can analyze data and have information about
them.
