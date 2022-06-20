Data Practical Week 5
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
library(tidyverse)
```

## Dataset and description

We will load a dataset from the package dplyr. I don’t specially like
starwars, even if it’s nice and famous, but I chose this dataset in
order to learn a bit more about it. And fun fact, my brother’s name come
from starwars… I let you think about who he can be.

``` r
data(starwars)
```

With the str formula we can have a look on types of data and describe
them a bit.

``` r
str(starwars)
```

    ## tibble [87 x 14] (S3: tbl_df/tbl/data.frame)
    ##  $ name      : chr [1:87] "Luke Skywalker" "C-3PO" "R2-D2" "Darth Vader" ...
    ##  $ height    : int [1:87] 172 167 96 202 150 178 165 97 183 182 ...
    ##  $ mass      : num [1:87] 77 75 32 136 49 120 75 32 84 77 ...
    ##  $ hair_color: chr [1:87] "blond" NA NA "none" ...
    ##  $ skin_color: chr [1:87] "fair" "gold" "white, blue" "white" ...
    ##  $ eye_color : chr [1:87] "blue" "yellow" "red" "yellow" ...
    ##  $ birth_year: num [1:87] 19 112 33 41.9 19 52 47 NA 24 57 ...
    ##  $ sex       : chr [1:87] "male" "none" "none" "male" ...
    ##  $ gender    : chr [1:87] "masculine" "masculine" "masculine" "masculine" ...
    ##  $ homeworld : chr [1:87] "Tatooine" "Tatooine" "Naboo" "Tatooine" ...
    ##  $ species   : chr [1:87] "Human" "Droid" "Droid" "Human" ...
    ##  $ films     :List of 87
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope" ...
    ##   ..$ : chr [1:6] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:7] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:4] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope"
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope" ...
    ##   ..$ : chr [1:3] "Attack of the Clones" "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr [1:3] "Attack of the Clones" "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr [1:6] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Revenge of the Sith" "Return of the Jedi" "A New Hope" ...
    ##   ..$ : chr [1:4] "The Empire Strikes Back" "Return of the Jedi" "A New Hope" "The Force Awakens"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr [1:3] "The Phantom Menace" "Return of the Jedi" "A New Hope"
    ##   ..$ : chr [1:3] "The Empire Strikes Back" "Return of the Jedi" "A New Hope"
    ##   ..$ : chr "A New Hope"
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:5] "The Empire Strikes Back" "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith" ...
    ##   ..$ : chr [1:3] "The Empire Strikes Back" "Attack of the Clones" "Return of the Jedi"
    ##   ..$ : chr "The Empire Strikes Back"
    ##   ..$ : chr "The Empire Strikes Back"
    ##   ..$ : chr [1:2] "The Empire Strikes Back" "Return of the Jedi"
    ##   ..$ : chr "The Empire Strikes Back"
    ##   ..$ : chr [1:2] "Return of the Jedi" "The Force Awakens"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:2] "Attack of the Clones" "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:2] "Attack of the Clones" "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:2] "Attack of the Clones" "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "Return of the Jedi"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Attack of the Clones" "The Phantom Menace"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "The Phantom Menace"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr "Attack of the Clones"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr "Revenge of the Sith"
    ##   ..$ : chr "Revenge of the Sith"
    ##   ..$ : chr [1:2] "Revenge of the Sith" "A New Hope"
    ##   ..$ : chr [1:2] "Attack of the Clones" "Revenge of the Sith"
    ##   ..$ : chr "Revenge of the Sith"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr "The Force Awakens"
    ##   ..$ : chr [1:3] "Attack of the Clones" "The Phantom Menace" "Revenge of the Sith"
    ##  $ vehicles  :List of 87
    ##   ..$ : chr [1:2] "Snowspeeder" "Imperial Speeder Bike"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Imperial Speeder Bike"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Tribubble bongo"
    ##   ..$ : chr [1:2] "Zephyr-G swoop bike" "XJ-6 airspeeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr "AT-ST"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Snowspeeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Tribubble bongo"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Sith speeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Flitknot speeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Koro-2 Exodrive airspeeder"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Tsmeu-6 personal wheel bike"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##  $ starships :List of 87
    ##   ..$ : chr [1:2] "X-wing" "Imperial shuttle"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "TIE Advanced x1"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "X-wing"
    ##   ..$ : chr [1:5] "Jedi starfighter" "Trade Federation cruiser" "Naboo star skiff" "Jedi Interceptor" ...
    ##   ..$ : chr [1:3] "Trade Federation cruiser" "Jedi Interceptor" "Naboo fighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr [1:2] "Millennium Falcon" "Imperial shuttle"
    ##   ..$ : chr [1:2] "Millennium Falcon" "Imperial shuttle"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "X-wing"
    ##   ..$ : chr "X-wing"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Slave 1"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Millennium Falcon"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "A-wing"
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Millennium Falcon"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Naboo Royal Starship"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Scimitar"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Jedi starfighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Naboo fighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "Belbullab-22 starfighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr "T-70 X-wing fighter"
    ##   ..$ : chr(0) 
    ##   ..$ : chr(0) 
    ##   ..$ : chr [1:3] "H-type Nubian yacht" "Naboo star skiff" "Naboo fighter"

We can see that we have 11 variables which are “character” ; 2 are
“numeric” and only 1 (height) is “integer”. On this dataset we can see
all characters of Starwars and details about them like their mass or eye
color. It could be interesting for real fans if they don’t already know
these information as their height. I think the most important is the
film in which they are because if you are really fan of one character
you can directly know where you can follow his/her adventures.

Now we will make our data long in place of wide. For that we will need
to use the package “tidyverse” that I will install now and load the
library.

``` r
library(tidyverse)
```

## Gather

And let’s the gather formula do what we want.

``` r
starwars%>% gather(name, height, mass, hair_color, skin_color, eye_color, birth_year, sex, gender, homeworld, species, films, vehicles, convert = TRUE)
```

    ## # A tibble: 957 x 3
    ##    starships name  height   
    ##    <list>    <chr> <list>   
    ##  1 <chr [2]> mass  <dbl [1]>
    ##  2 <chr [0]> mass  <dbl [1]>
    ##  3 <chr [0]> mass  <dbl [1]>
    ##  4 <chr [1]> mass  <dbl [1]>
    ##  5 <chr [0]> mass  <dbl [1]>
    ##  6 <chr [0]> mass  <dbl [1]>
    ##  7 <chr [0]> mass  <dbl [1]>
    ##  8 <chr [0]> mass  <dbl [1]>
    ##  9 <chr [1]> mass  <dbl [1]>
    ## 10 <chr [5]> mass  <dbl [1]>
    ## # ... with 947 more rows

There we reversed the wide table in a long table. (In this format, the
table is really big. For me I would used the previous format if I really
needed for a study.) We can try the formula of pivot_longer and use
numeric variables to make it better.

## Pivot

``` r
starwars %>% pivot_longer (c("mass", "birth_year"), names_to = "variables")
```

    ## # A tibble: 174 x 14
    ##    name    height hair_color skin_color eye_color sex   gender homeworld species
    ##    <chr>    <int> <chr>      <chr>      <chr>     <chr> <chr>  <chr>     <chr>  
    ##  1 Luke S~    172 blond      fair       blue      male  mascu~ Tatooine  Human  
    ##  2 Luke S~    172 blond      fair       blue      male  mascu~ Tatooine  Human  
    ##  3 C-3PO      167 <NA>       gold       yellow    none  mascu~ Tatooine  Droid  
    ##  4 C-3PO      167 <NA>       gold       yellow    none  mascu~ Tatooine  Droid  
    ##  5 R2-D2       96 <NA>       white, bl~ red       none  mascu~ Naboo     Droid  
    ##  6 R2-D2       96 <NA>       white, bl~ red       none  mascu~ Naboo     Droid  
    ##  7 Darth ~    202 none       white      yellow    male  mascu~ Tatooine  Human  
    ##  8 Darth ~    202 none       white      yellow    male  mascu~ Tatooine  Human  
    ##  9 Leia O~    150 brown      light      brown     fema~ femin~ Alderaan  Human  
    ## 10 Leia O~    150 brown      light      brown     fema~ femin~ Alderaan  Human  
    ## # ... with 164 more rows, and 5 more variables: films <list>, vehicles <list>,
    ## #   starships <list>, variables <chr>, value <dbl>

I prefer this table but unfortunately all my data are present 2 times
and I didn’t manage to delete the duplicated data. For me this table is
already in a “tidy format”.

Now we will take a column in our dataset and split the columns values
into new columns with the formula separate(). It’s a bit hard because in
this dataset, I don’t have a relevant value to split. However, I chose
to do it with skin color because some of the sample have several color
for their skin(s). I think it’s funny… Let’s do it.

## Separation

``` r
starwars %>% separate(skin_color, into=c("skin", "color"), sep=",")
```

    ## # A tibble: 87 x 15
    ##    name    height  mass hair_color skin  color eye_color birth_year sex   gender
    ##    <chr>    <int> <dbl> <chr>      <chr> <chr> <chr>          <dbl> <chr> <chr> 
    ##  1 Luke S~    172    77 blond      fair   <NA> blue            19   male  mascu~
    ##  2 C-3PO      167    75 <NA>       gold   <NA> yellow         112   none  mascu~
    ##  3 R2-D2       96    32 <NA>       white " bl~ red             33   none  mascu~
    ##  4 Darth ~    202   136 none       white  <NA> yellow          41.9 male  mascu~
    ##  5 Leia O~    150    49 brown      light  <NA> brown           19   fema~ femin~
    ##  6 Owen L~    178   120 brown, gr~ light  <NA> blue            52   male  mascu~
    ##  7 Beru W~    165    75 brown      light  <NA> blue            47   fema~ femin~
    ##  8 R5-D4       97    32 <NA>       white " re~ red             NA   none  mascu~
    ##  9 Biggs ~    183    84 black      light  <NA> brown           24   male  mascu~
    ## 10 Obi-Wa~    182    77 auburn, w~ fair   <NA> blue-gray       57   male  mascu~
    ## # ... with 77 more rows, and 5 more variables: homeworld <chr>, species <chr>,
    ## #   films <list>, vehicles <list>, starships <list>

Okay, I don’t really like this presentation of data. I think it’s
strange and not relevant to split these data like that. So I have this
idea… I’m not a specialist of Star wars so I’m not sure if those who
have 2 skin colors is because their skin is split in 2 colors or if
their skins could be modified. Let me think that they could change their
skin or that when they are angry, their skin has an alternative color.
To make my separation more relevant I just want to rename columns in
original skin and alternative skin color. I hope that I don’t
misunderstood too much the Saga…

Let’s rename the columns

``` r
starwars_sep<-starwars %>% separate(skin_color, into=c("original_skin_color", "alternative_skin_color"), sep=",")
```

    ## Warning: Expected 2 pieces. Additional pieces discarded in 3 rows [47, 67, 76].

    ## Warning: Expected 2 pieces. Missing pieces filled with `NA` in 73 rows [1, 2, 4,
    ## 5, 6, 7, 9, 10, 11, 12, 13, 14, 15, 17, 18, 19, 20, 21, 22, 23, ...].

*One week after having published this data on the web* Okay, I received
too much critics about my idea that their skins could change when this
characters were angry…You really shouldn’t joke with star wars’ fans… I
decided to cancel my previous separation and unite these 2 columns
again. For that I used the formula unite().

## Unite

``` r
starwars_sep%>% unite(skin_color, original_skin_color, alternative_skin_color) 
```

    ## # A tibble: 87 x 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke Sk~    172    77 blond      fair_NA    blue            19   male  mascu~
    ##  2 C-3PO       167    75 <NA>       gold_NA    yellow         112   none  mascu~
    ##  3 R2-D2        96    32 <NA>       white_ bl~ red             33   none  mascu~
    ##  4 Darth V~    202   136 none       white_NA   yellow          41.9 male  mascu~
    ##  5 Leia Or~    150    49 brown      light_NA   brown           19   fema~ femin~
    ##  6 Owen La~    178   120 brown, gr~ light_NA   blue            52   male  mascu~
    ##  7 Beru Wh~    165    75 brown      light_NA   blue            47   fema~ femin~
    ##  8 R5-D4        97    32 <NA>       white_ red red             NA   none  mascu~
    ##  9 Biggs D~    183    84 black      light_NA   brown           24   male  mascu~
    ## 10 Obi-Wan~    182    77 auburn, w~ fair_NA    blue-gray       57   male  mascu~
    ## # ... with 77 more rows, and 5 more variables: homeworld <chr>, species <chr>,
    ## #   films <list>, vehicles <list>, starships <list>

Okay, the problem is that all NA are jointed and it’s not aesthetic.
Moreover, I don’t like the separation “\_“, and I’m sure that fans won’t
like too. Let’s do the changes.

``` r
starwars_sep%>% unite(skin_color, original_skin_color, alternative_skin_color, sep = ",", na.rm = TRUE) 
```

    ## # A tibble: 87 x 14
    ##    name     height  mass hair_color skin_color eye_color birth_year sex   gender
    ##    <chr>     <int> <dbl> <chr>      <chr>      <chr>          <dbl> <chr> <chr> 
    ##  1 Luke Sk~    172    77 blond      fair       blue            19   male  mascu~
    ##  2 C-3PO       167    75 <NA>       gold       yellow         112   none  mascu~
    ##  3 R2-D2        96    32 <NA>       white, bl~ red             33   none  mascu~
    ##  4 Darth V~    202   136 none       white      yellow          41.9 male  mascu~
    ##  5 Leia Or~    150    49 brown      light      brown           19   fema~ femin~
    ##  6 Owen La~    178   120 brown, gr~ light      blue            52   male  mascu~
    ##  7 Beru Wh~    165    75 brown      light      blue            47   fema~ femin~
    ##  8 R5-D4        97    32 <NA>       white, red red             NA   none  mascu~
    ##  9 Biggs D~    183    84 black      light      brown           24   male  mascu~
    ## 10 Obi-Wan~    182    77 auburn, w~ fair       blue-gray       57   male  mascu~
    ## # ... with 77 more rows, and 5 more variables: homeworld <chr>, species <chr>,
    ## #   films <list>, vehicles <list>, starships <list>

Okay great. I think everybody will be happy now.

## Plots

The last think I want to do in this practical is to create a plot with
the formula ggplot. It could be interesting to make a plot with height
and mass from all character in order to see where is the fattest; hehe.
I bet it will be Chewbacca (number 13) and for that I will select his
values and highlight it.

``` r
data <- starwars %>%rownames_to_column(var="Chewbacca")

ggplot(data, aes(x=height,y=mass))+geom_point()+geom_label(data=data %>% filter(height==228 & mass==112),aes(label=Chewbacca))
```

    ## Warning: Removed 28 rows containing missing values (geom_point).

![](week-5_files/figure-gfm/ggplot%20with%20height%20and%20mass-1.png)<!-- -->
Well, fortunately I didn’t bet too much. The problem with this graph is
that we don’t know which point belongs to which character. Previously I
add the number for each character but with so much data, this graph was
hard too understand. Each point was overlaying with the others. For our
question to know which character is the fattest we can see that one is
clearly isolated than all others. Do you see it ? Let me help you :)

``` r
data <- starwars %>%rownames_to_column(var="Jabba_Desilijic_Tiure")
 
ggplot(data,aes(x=height,y=mass))+geom_point()+geom_label(data=data %>%filter(height==175 & mass==1358),aes(label=Jabba_Desilijic_Tiure))
```

    ## Warning: Removed 28 rows containing missing values (geom_point).

![](week-5_files/figure-gfm/plot%20showing%20the%20fattest%20character%20of%20all%20the%20Saga-1.png)<!-- -->
The great, the best and the famous Jabba Desilijic Tiure is our winner
of this report ! congratulations Jabba !

<img src="https://www.nicepng.com/png/full/121-1219694_jabba-desilijic-tiure-of-tatooine-jabba-the-hutt.png" style="width:40.0%" />

Now that we see it, it’s obvious that it won the contest…
