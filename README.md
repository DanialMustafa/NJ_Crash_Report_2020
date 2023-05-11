NJ Car Crash Report (2020)
================

## Introduction

Finding an idea for this project was difficult as I had many ideas but
ran into many problems. The first time I tried starting this, I was
really eager on creating a map of National Parks and show lines of
people going into them from throughout the US, but I couldn’t find any
solid datasets. After a couple round of ideas, I decided to write about
NJ crashes.

In this notebook, I will be showing some of the major highways in NJ
combined with some data on crash statistics from 2020. Since I go on
Route 9 very frequently and it being the longest highway in NJ, I’ll be
starting with that!

## Creating Dataframes

To skip having to read the code, I imported a dataset from the Official
NJ website about crash statistics. I ended up getting a 256 page
document of many different things about crashes for nearly every single
route in NJ. After a little bit of researching online and a bit of trial
and error I finally managed to get my dataframe of Route 9 which you can
see below.

Additionally, this data has Milepost locations for each of its data
points so I decided it would be a good idea to also include another
datasets that turns Milepost locations into Longitude and Latitude
coordinates. I also obtained this data through NJ official website, but
it came in the form of a .shp file which can be downloaded from the url
below. I used the sf library to read it in and combine it with the Route
9 dataset so I could plot this data later on.

Website:
<https://www.state.nj.us/transportation/refdata/accident/20/route20.pdf>
<https://www.state.nj.us/transportation/refdata/gis/zip/NJ_Milepost10ths_shp.zip>

### Route 9 Dataframe

    ##   MP_Start MP_End Section_Length AADT Total_Crashes Fatal_Crashes
    ## 1      3.1    3.3           0.26 7176             5             0
    ## 2      3.3    3.4           0.08 7176             0             0
    ## 3      3.4    3.8           0.41 9533             1             0
    ## 4      3.8    6.6           2.82 9533             9             0
    ## 5      6.6    6.7           0.02 9533             0             0
    ##   Injury_Crashes Prop_Dam_Only_Crashes Crash_Rate   County
    ## 1              2                     3       7.32 CAPE MAY
    ## 2              0                     0       0.00 CAPE MAY
    ## 3              0                     1       0.70 CAPE MAY
    ## 4              2                     7       0.91 CAPE MAY
    ## 5              0                     0       0.00 CAPE MAY
    ##              Cross_Section LATITUDE  LONGTUDE Lanes Shoulder Median
    ## 1    2 Lanes With Shoulder 38.96705 -74.91490     2     With   <NA>
    ## 2 2 Lanes Without Shoulder 38.96986 -74.91422     2  Without   <NA>
    ## 3 2 Lanes Without Shoulder 38.97117 -74.91329     2  Without   <NA>
    ## 4    2 Lanes With Shoulder 38.97637 -74.90957     2     With   <NA>
    ## 5    2 Lanes With Shoulder 39.00895 -74.88151     2     With   <NA>

![](NJ_Car_Crash_Report_files/figure-gfm/Route%209%20Plot-1.png)<!-- -->

I originally planned to only have Route 9 on my NJ map, but in hindsight
I guess I was too optimistic. The graph above looks a bit lonely and
it’s definitely not fun looking at just one road in NJ.

So, I decided to add in Route 18, Route 1, Route 130, and Route 46. I
chose Route 18 because I commute on it every day to Rutgers and was just
curious on what I’d find. The others I chose because of the website
linked below. It claimed that those ones were one of the worst overall
roads in NJ. Website:
<https://www.nj.com/news/2015/04/the_10_roughest_stretches_of_state_roads_in_nj_map.html>

Anyways, with a little bit of experience, I was able to knock the others
out much faster as I reused a lot of the code that I used to get the
Route 9 dataframe. You can see a part of the dataframes below.

### Route 18 Dataframe

    ##   MP_Start MP_End Section_Length  AADT Total_Crashes Fatal_Crashes
    ## 1      5.5    5.6           0.07 34603             0             0
    ## 2      5.6    5.7           0.15 35961             1             0
    ## 3      5.7    6.5           0.76 35961             5             0
    ## 4      6.5    6.8           0.27 39505             0             0
    ## 5      6.8    7.0           0.25 39505             8             0
    ##   Injury_Crashes Prop_Dam_Only_Crashes Crash_Rate   County
    ## 1              0                     0       0.00 MONMOUTH
    ## 2              1                     0       0.51 MONMOUTH
    ## 3              0                     5       0.50 MONMOUTH
    ## 4              0                     0       0.00 MONMOUTH
    ## 5              2                     6       2.21 MONMOUTH
    ##                                   Cross_Section Lanes Shoulder  Median LATITUDE
    ## 1 4 or More Lanes, Barrier Median With Shoulder     4     With Barrier 40.17251
    ## 2 4 or More Lanes, Barrier Median With Shoulder     4     With Barrier 40.17410
    ## 3   4 or More Lanes, Grass Median With Shoulder     4     With   Grass 40.17577
    ## 4   4 or More Lanes, Grass Median With Shoulder     4     With   Grass 40.18718
    ## 5 4 or More Lanes, Barrier Median With Shoulder     4     With Barrier 40.19033
    ##    LONGTUDE
    ## 1 -74.07212
    ## 2 -74.07257
    ## 3 -74.07278
    ## 4 -74.07174
    ## 5 -74.06771

### Route 1 Dataframe

    ##   MP_Start MP_End Section_Length  AADT Total_Crashes Fatal_Crashes
    ## 1      0.0    0.6           0.00     0           107             0
    ## 2      1.2    1.2           0.63 52607            28             0
    ## 3      1.2    1.6           0.42 60614            46             1
    ## 4      1.6    1.7           0.05 60614             3             0
    ## 5      1.7    1.8           0.05 50249             0             0
    ##   Injury_Crashes Prop_Dam_Only_Crashes Crash_Rate County
    ## 1             17                    90       0.00       
    ## 2              7                    21       2.31 MERCER
    ## 3             10                    35       4.94 MERCER
    ## 4              1                     2       2.70 MERCER
    ## 5              0                     0       0.00 MERCER
    ##                                      Cross_Section Lanes Shoulder  Median
    ## 1                                                   <NA>     <NA>    <NA>
    ## 2    4 or More Lanes, Barrier Median With Shoulder     4     With Barrier
    ## 3    4 or More Lanes, Barrier Median With Shoulder     4     With Barrier
    ## 4 4 or More Lanes, Barrier Median Without Shoulder     4  Without Barrier
    ## 5 4 or More Lanes, Barrier Median Without Shoulder     4  Without Barrier
    ##   LATITUDE  LONGTUDE
    ## 1 40.20912 -74.76761
    ## 2 40.22225 -74.75836
    ## 3 40.22225 -74.75836
    ## 4 40.22778 -74.75769
    ## 5 40.22877 -74.75626

### Route 130 Dataframe

    ##   MP_Start MP_End Section_Length  AADT Total_Crashes Fatal_Crashes
    ## 1      0.0    0.0           0.00     0            25             0
    ## 2      0.0    0.1           0.15 15195             1             0
    ## 3      0.1    0.3           0.15 15195             2             0
    ## 4      0.3    0.4           0.14 12993             3             0
    ## 5      0.4    0.5           0.05 12993             0             0
    ##   Injury_Crashes Prop_Dam_Only_Crashes Crash_Rate County
    ## 1              5                    20       0.00       
    ## 2              0                     1       1.20  SALEM
    ## 3              0                     2       2.40  SALEM
    ## 4              1                     2       4.51  SALEM
    ## 5              0                     0       0.00  SALEM
    ##              Cross_Section Lanes Shoulder Median LATITUDE  LONGTUDE
    ## 1                           <NA>     <NA>   <NA> 39.68024 -75.49266
    ## 2 2 Lanes Without Shoulder     2  Without   <NA> 39.68024 -75.49266
    ## 3    2 Lanes With Shoulder     2     With   <NA> 39.68132 -75.49194
    ## 4    2 Lanes With Shoulder     2     With   <NA> 39.68393 -75.49022
    ## 5    2 Lanes With Shoulder     2     With   <NA> 39.68525 -75.48935

### Route 46 Dataframe

    ##   MP_Start MP_End Section_Length  AADT Total_Crashes Fatal_Crashes
    ## 1      0.0    0.6           0.00     0           107             0
    ## 2      1.2    1.2           0.63 52607            28             0
    ## 3      1.2    1.6           0.42 60614            46             1
    ## 4      1.6    1.7           0.05 60614             3             0
    ## 5      1.7    1.8           0.05 50249             0             0
    ##   Injury_Crashes Prop_Dam_Only_Crashes Crash_Rate County
    ## 1             17                    90       0.00       
    ## 2              7                    21       2.31 MERCER
    ## 3             10                    35       4.94 MERCER
    ## 4              1                     2       2.70 MERCER
    ## 5              0                     0       0.00 MERCER
    ##                                      Cross_Section Lanes Shoulder  Median
    ## 1                                                   <NA>     <NA>    <NA>
    ## 2    4 or More Lanes, Barrier Median With Shoulder     4     With Barrier
    ## 3    4 or More Lanes, Barrier Median With Shoulder     4     With Barrier
    ## 4 4 or More Lanes, Barrier Median Without Shoulder     4  Without Barrier
    ## 5 4 or More Lanes, Barrier Median Without Shoulder     4  Without Barrier
    ##   LATITUDE  LONGTUDE
    ## 1 40.93007 -75.09697
    ## 2 40.91663 -75.08119
    ## 3 40.91663 -75.08119
    ## 4 40.91202 -75.07684
    ## 5 40.91065 -75.07626

Now that we have all out datasets I’m going to combine them into one big
dataset so I can easily work with all of them at the same time. I also
included in this, code to export the combined dataframe into a .csv call
‘alldata.csv’.

### All Routes Dataset

    ##   MP_Start MP_End Section_Length AADT Total_Crashes Fatal_Crashes
    ## 1      3.1    3.3           0.26 7176             5             0
    ## 2      3.3    3.4           0.08 7176             0             0
    ## 3      3.4    3.8           0.41 9533             1             0
    ## 4      3.8    6.6           2.82 9533             9             0
    ## 5      6.6    6.7           0.02 9533             0             0
    ##   Injury_Crashes Prop_Dam_Only_Crashes Crash_Rate   County
    ## 1              2                     3       7.32 CAPE MAY
    ## 2              0                     0       0.00 CAPE MAY
    ## 3              0                     1       0.70 CAPE MAY
    ## 4              2                     7       0.91 CAPE MAY
    ## 5              0                     0       0.00 CAPE MAY
    ##              Cross_Section LATITUDE  LONGTUDE Lanes Shoulder Median route
    ## 1    2 Lanes With Shoulder 38.96705 -74.91490     2     With   <NA>  US 9
    ## 2 2 Lanes Without Shoulder 38.96986 -74.91422     2  Without   <NA>  US 9
    ## 3 2 Lanes Without Shoulder 38.97117 -74.91329     2  Without   <NA>  US 9
    ## 4    2 Lanes With Shoulder 38.97637 -74.90957     2     With   <NA>  US 9
    ## 5    2 Lanes With Shoulder 39.00895 -74.88151     2     With   <NA>  US 9

It would also be a good time to explain what each of these parameters
mean as well:

- MP_Start, - Start and end positions of each point on its respective
  road
- MP_End
- Section_Length - How long the section they are referring to in the
  datapoint (MP_End - MP_Start)
- AADT - Average Annual Daily Traffic; basically just the expected
  number of cars passing that section daily
- Total_Crashes, - Pretty self explanatory
- Fatal_Crashes,
- Injury_Crashes,
- Prop_Dam_Only_Crashes
- Crash_Rate - Crash Rate calculated by NJDOTS and NJTR-1
- County
- Cross_Section - Explanation of other conditions present during that
  stretch of road
- Lanes, Shoulder, Median - Cross_Section split up just for convenience
- LONGITUDE, LATITUDE - coordinates of MP at each data point
- route - which route the data point belongs to

I really hope I did a good job explaining these to you. Now that that’s
out of the way, we can finally get to the intersting things I found from
this project.

## Data Visualization

Let’s first just appreciate the newest map that we just made.

![](NJ_Car_Crash_Report_files/figure-gfm/Map%20of%20New%20Jersey%20with%205%20Major%20Roads-1.png)<!-- -->

Wow, doesn’t that look much better?

One of the first things I wanted to look at in this project was where am
I most likely to encounter accidents? Well it turns out that more
accidents tend to happen up in North Jersey and on the border of
Pennsylvania than it does in South Jersey. This is pretty reasonable as
many people could be traveling to New York City, Newark, Camden, or
Philadelphia.

![](NJ_Car_Crash_Report_files/figure-gfm/Number%20of%20Total%20Crashes%20Across%20Major%20Roads%20in%20NJ-1.png)<!-- -->

One thing I noticed was weird was how the bottom right of the mpa remain
almost accident free. Looking at other variables, I found that the Cross
Section matters shows a very familiar pattern.

![](NJ_Car_Crash_Report_files/figure-gfm/Cross%20Section%20Conditions%20of%20Routes%20in%20NJ-1.png)<!-- -->

And as I suspected, my hunch was right! Taking special note to the
number of lanes, we see below that there are much less total crashes for
roads who only have 2 or 3 lanes. I would make the inference that if
there are more lanes, then that means that the location has a higher
speed limit thus resulting in more crashes. However, without additional
data there’s no way to properly assert such a claim.

![](NJ_Car_Crash_Report_files/figure-gfm/Total%20Crashes%20by%20Cross%20Section%20and%20Number%20of%20Lanes-1.png)<!-- -->

One last thing I wanted to show was the crash rates by Shoulder and
Median condition. We already know that a road with 4 or more lanes
causes many accidents but is there anything else this data can tell us?
Looking at the Crash Rate by Shoulder for each route, we could argue
that roads Without Shoulders cause more accidents, but there’s nothing
really concrete.

![](NJ_Car_Crash_Report_files/figure-gfm/Crash%20Rate%20by%20Shoulder%20for%20each%20Route%20(Filtered%20to%204%20or%20More%20Lanes)-1.png)<!-- -->

Looking at this plot though we can see that roads in US 1, US 46, and US
9 with No Median clearly have the highest median (ironically) of Crash
Rates. Roads US 130 and NJ 18 don’t have data for Median conditions
however meaning that although the relationship isn’t concrete, it’s
something to surely look into.

![](NJ_Car_Crash_Report_files/figure-gfm/Crash%20Rate%20by%20Median%20for%20each%20Route%20(Filtered%20to%204%20or%20More%20Lanes)-1.png)<!-- -->

## Conclusion

This concludes my report on the five major roads in NJ that I chose to
survey. Although it’s reasonable to assume that more traffic results in
more crashes, I hope my maps gave a bit more insight into the issue. I’m
also shocked I was able to find a potentially relevant relationship from
this project. I never would have imagined that this project would have
turned out this way.

If I were to continue with this project I would certainly try to expand
my data by using all of the different routes in the Crash Statistics for
NJ in 2020 instead of just the 5 I decided to choose. On top of that, I
would especially try to get some related data set about the NJ Turnpike
and the Garden State Parkway as those two would give the best insight on
crashes as they have the most amount of traffic crossing it daily.

Some variables I would plan to get are the types of cars involved in the
crash, speed limits for each milepost, light post locations data or even
the weather at the time of the crash. From these I would be able to
perform a statistical analysis such as ANOVA or chi-square and possibly
find some correlations between accidents and what causes them.
