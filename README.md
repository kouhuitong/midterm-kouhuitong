Midterm.
--------

#### 1. Map the delay by destination.

Compute the average delay by destination, then join on the airports data
frame so you can show the spatial distribution of delays. Here’s an easy
way to draw a map of the United States. You are welcome to use this code
or some other code.

    library(tidyverse)

    ## -- Attaching packages ------------------------------------ tidyverse 1.3.0 --

    ## v ggplot2 3.2.1     v purrr   0.3.3
    ## v tibble  2.1.3     v dplyr   0.8.4
    ## v tidyr   1.0.2     v stringr 1.4.0
    ## v readr   1.3.1     v forcats 0.5.0

    ## -- Conflicts --------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    library(nycflights13)
    library(ggplot2)

    airports %>%
      semi_join(flights, c("faa" = "dest")) %>%
      ggplot(aes(lon, lat)) +
      borders("state") +
      geom_point() +
      coord_quickmap()

![](README_files/figure-markdown_strict/unnamed-chunk-1-1.png)

You might want to use the size or colour of the points to display the
average delay for each airport.

    flights

    ## # A tibble: 336,776 x 19
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 11 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>

    planes

    ## # A tibble: 3,322 x 9
    ##    tailnum  year type          manufacturer   model  engines seats speed engine 
    ##    <chr>   <int> <chr>         <chr>          <chr>    <int> <int> <int> <chr>  
    ##  1 N10156   2004 Fixed wing m~ EMBRAER        EMB-1~       2    55    NA Turbo-~
    ##  2 N102UW   1998 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ##  3 N103US   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ##  4 N104UW   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ##  5 N10575   2002 Fixed wing m~ EMBRAER        EMB-1~       2    55    NA Turbo-~
    ##  6 N105UW   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ##  7 N107US   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ##  8 N108UW   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ##  9 N109UW   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ## 10 N110UW   1999 Fixed wing m~ AIRBUS INDUST~ A320-~       2   182    NA Turbo-~
    ## # ... with 3,312 more rows

    airlines

    ## # A tibble: 16 x 2
    ##    carrier name                       
    ##    <chr>   <chr>                      
    ##  1 9E      Endeavor Air Inc.          
    ##  2 AA      American Airlines Inc.     
    ##  3 AS      Alaska Airlines Inc.       
    ##  4 B6      JetBlue Airways            
    ##  5 DL      Delta Air Lines Inc.       
    ##  6 EV      ExpressJet Airlines Inc.   
    ##  7 F9      Frontier Airlines Inc.     
    ##  8 FL      AirTran Airways Corporation
    ##  9 HA      Hawaiian Airlines Inc.     
    ## 10 MQ      Envoy Air                  
    ## 11 OO      SkyWest Airlines Inc.      
    ## 12 UA      United Air Lines Inc.      
    ## 13 US      US Airways Inc.            
    ## 14 VX      Virgin America             
    ## 15 WN      Southwest Airlines Co.     
    ## 16 YV      Mesa Airlines Inc.

    airports

    ## # A tibble: 1,458 x 8
    ##    faa   name                       lat    lon   alt    tz dst   tzone          
    ##    <chr> <chr>                    <dbl>  <dbl> <dbl> <dbl> <chr> <chr>          
    ##  1 04G   Lansdowne Airport         41.1  -80.6  1044    -5 A     America/New_Yo~
    ##  2 06A   Moton Field Municipal A~  32.5  -85.7   264    -6 A     America/Chicago
    ##  3 06C   Schaumburg Regional       42.0  -88.1   801    -6 A     America/Chicago
    ##  4 06N   Randall Airport           41.4  -74.4   523    -5 A     America/New_Yo~
    ##  5 09J   Jekyll Island Airport     31.1  -81.4    11    -5 A     America/New_Yo~
    ##  6 0A9   Elizabethton Municipal ~  36.4  -82.2  1593    -5 A     America/New_Yo~
    ##  7 0G6   Williams County Airport   41.5  -84.5   730    -5 A     America/New_Yo~
    ##  8 0G7   Finger Lakes Regional A~  42.9  -76.8   492    -5 A     America/New_Yo~
    ##  9 0P2   Shoestring Aviation Air~  39.8  -76.6  1000    -5 U     America/New_Yo~
    ## 10 0S9   Jefferson County Intl     48.1 -123.    108    -8 A     America/Los_An~
    ## # ... with 1,448 more rows

    weather

    ## # A tibble: 26,115 x 15
    ##    origin  year month   day  hour  temp  dewp humid wind_dir wind_speed
    ##    <chr>  <int> <int> <int> <int> <dbl> <dbl> <dbl>    <dbl>      <dbl>
    ##  1 EWR     2013     1     1     1  39.0  26.1  59.4      270      10.4 
    ##  2 EWR     2013     1     1     2  39.0  27.0  61.6      250       8.06
    ##  3 EWR     2013     1     1     3  39.0  28.0  64.4      240      11.5 
    ##  4 EWR     2013     1     1     4  39.9  28.0  62.2      250      12.7 
    ##  5 EWR     2013     1     1     5  39.0  28.0  64.4      260      12.7 
    ##  6 EWR     2013     1     1     6  37.9  28.0  67.2      240      11.5 
    ##  7 EWR     2013     1     1     7  39.0  28.0  64.4      240      15.0 
    ##  8 EWR     2013     1     1     8  39.9  28.0  62.2      250      10.4 
    ##  9 EWR     2013     1     1     9  39.9  28.0  62.2      260      15.0 
    ## 10 EWR     2013     1     1    10  41    28.0  59.6      260      13.8 
    ## # ... with 26,105 more rows, and 5 more variables: wind_gust <dbl>,
    ## #   precip <dbl>, pressure <dbl>, visib <dbl>, time_hour <dttm>

    # put your answer here.
    # x=flights %>% 
    #   group_by(dest) %>% 
    #   summarise(avedelay=mean(arr_delay,na.rm = T)) 
    # 
    # ggplot(data=x)+
    #   geom_point(mapping=aes(dest,avedelay,size=avedelay))

    # put your answer here.
    flights_delay = flights %>% 
      group_by(dest) %>% 
      summarise(ave_arr_delay = mean(arr_delay, na.rm = T))

    airports %>% 
      left_join(flights_delay, c("faa" = "dest")) %>%
      filter(lat >= 20 & lat<=70, lon>=-160 & lon <= -60) %>% 
      filter(!is.na(ave_arr_delay)) %>% 
      ggplot(aes(x=lon, y=lat, na.rm = T, colour = ave_arr_delay)) +
      borders("state") +
      geom_point() +
      coord_quickmap() +
      scale_colour_gradient(low = 'lightblue', high = 'darkblue')

![](README_files/figure-markdown_strict/unnamed-chunk-2-1.png)

#### 2. Do planes trade ownership?

You might expect that there’s an implicit relationship between plane and
airline, because each plane is flown by a single airline. Confirm or
reject this conjecture using data.

    # put your answer here. 
    x2=flights %>% 
      group_by(tailnum,carrier) %>% 
      summarise(count=n()) %>% 
      group_by(tailnum) %>% 
      summarise(count=n())
    x2

    ## # A tibble: 4,044 x 2
    ##    tailnum count
    ##    <chr>   <int>
    ##  1 D942DN      1
    ##  2 N0EGMQ      1
    ##  3 N10156      1
    ##  4 N102UW      1
    ##  5 N103US      1
    ##  6 N104UW      1
    ##  7 N10575      1
    ##  8 N105UW      1
    ##  9 N107US      1
    ## 10 N108UW      1
    ## # ... with 4,034 more rows

    x2[x2$count!=1,]

    ## # A tibble: 18 x 2
    ##    tailnum count
    ##    <chr>   <int>
    ##  1 N146PQ      2
    ##  2 N153PQ      2
    ##  3 N176PQ      2
    ##  4 N181PQ      2
    ##  5 N197PQ      2
    ##  6 N200PQ      2
    ##  7 N228PQ      2
    ##  8 N232PQ      2
    ##  9 N933AT      2
    ## 10 N935AT      2
    ## 11 N977AT      2
    ## 12 N978AT      2
    ## 13 N979AT      2
    ## 14 N981AT      2
    ## 15 N989AT      2
    ## 16 N990AT      2
    ## 17 N994AT      2
    ## 18 <NA>        7

    #We found some planes are flown by 2 airlines

#### 3. Plane’s average speed.

Notice that `flights$air_time` is in minutes. Make a new column that is
the air time in hours.

    # put your answer here. 
    flights %>% 
      mutate(air_time_hour=air_time/60)

    ## # A tibble: 336,776 x 20
    ##     year month   day dep_time sched_dep_time dep_delay arr_time sched_arr_time
    ##    <int> <int> <int>    <int>          <int>     <dbl>    <int>          <int>
    ##  1  2013     1     1      517            515         2      830            819
    ##  2  2013     1     1      533            529         4      850            830
    ##  3  2013     1     1      542            540         2      923            850
    ##  4  2013     1     1      544            545        -1     1004           1022
    ##  5  2013     1     1      554            600        -6      812            837
    ##  6  2013     1     1      554            558        -4      740            728
    ##  7  2013     1     1      555            600        -5      913            854
    ##  8  2013     1     1      557            600        -3      709            723
    ##  9  2013     1     1      557            600        -3      838            846
    ## 10  2013     1     1      558            600        -2      753            745
    ## # ... with 336,766 more rows, and 12 more variables: arr_delay <dbl>,
    ## #   carrier <chr>, flight <int>, tailnum <chr>, origin <chr>, dest <chr>,
    ## #   air_time <dbl>, distance <dbl>, hour <dbl>, minute <dbl>, time_hour <dttm>,
    ## #   air_time_hour <dbl>

#### 4. Average speed

For each flight, compute the average speed of that flight (in miles per
hour). Then, for each plane, compute the average of those average
speeds. Display it in a histogram. You can use a base R histogram `hist`
or ggplot’s `geom_histogram`.

    # put your answer here.  
    x4=flights %>% 
      mutate(air_time_hour=air_time/60) %>% 
      mutate(ave_speed=distance/air_time_hour) %>% 
      group_by(tailnum) %>% 
      summarise(speed=mean(ave_speed,na.rm = T))
    x4  

    ## # A tibble: 4,044 x 2
    ##    tailnum speed
    ##    <chr>   <dbl>
    ##  1 D942DN   381.
    ##  2 N0EGMQ   391.
    ##  3 N10156   385.
    ##  4 N102UW   394.
    ##  5 N103US   388.
    ##  6 N104UW   400.
    ##  7 N10575   356.
    ##  8 N105UW   383.
    ##  9 N107US   391.
    ## 10 N108UW   399.
    ## # ... with 4,034 more rows

    hist(x4$speed,breaks = length(x4$speed),xlab = 'average_speed',freq = T)

![](README_files/figure-markdown_strict/unnamed-chunk-5-1.png)

#### 5. What correlates with average speed?

To examine if there is anything in the plane data that correlates with
average speed, use `geom_boxplot` with average speed of the plane (in
previous question) on the y-axis and `planes$engine` on the x-axis. Do
the same for `planes$engines` and `planes$type`.

    # put answer here
    x5=x4 %>% 
      left_join(planes,by='tailnum') 

    ggplot(data=x5,mapping = aes(x=x5$engine,y=speed.x))+
      geom_boxplot()

    ## Warning: Removed 7 rows containing non-finite values (stat_boxplot).

![](README_files/figure-markdown_strict/unnamed-chunk-6-1.png)

    ggplot(data=x5,mapping = aes(x=as.factor(x5$engines),y=speed.x))+
      geom_boxplot()

    ## Warning: Removed 7 rows containing non-finite values (stat_boxplot).

![](README_files/figure-markdown_strict/unnamed-chunk-6-2.png)

    ggplot(data=x5,mapping = aes(x=x5$type,y=speed.x))+
      geom_boxplot()

    ## Warning: Removed 7 rows containing non-finite values (stat_boxplot).

![](README_files/figure-markdown_strict/unnamed-chunk-6-3.png)

PLEASE REMEMBER TO ALSO COMMIT AND PUSH YOUR FIGURES!!!
