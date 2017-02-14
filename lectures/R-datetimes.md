---
layout: page
element: lecture
title: Web Data to Datetimes & Timeseries
language: R
---

#### Learning Objectives

> Following this assignment students should be able to:
>
> - understand the 3 date/datetime classes in R
> - convert data between the three classes (e.g., using `lubridate`)
> - work with date & datetime data efficiently

Since we didn't really get to the datetime stuff last lesson, let's dive straight in here.

Datetimes (aka Insanity)
------------------------

First, please read:

-   this lesson on [dates & spreadsheets](http://www.datacarpentry.org/spreadsheet-ecology-lesson/03-dates-as-data.html)
-   <https://www.stat.berkeley.edu/~s133/dates.html>
-   <https://cran.r-project.org/web/packages/lubridate/vignettes/lubridate.html>
-   <http://www.noamross.net/blog/2014/2/10/using-times-and-dates-in-r---presentation-code.html>

Various commands and functions available. There are **3** basic time classes in R:

-   Dates (just dates, i.e., 2012-02-10)
-   POSIXct ("**ct**" == calendar time, best class for dates with times)
-   POSIXlt ("**lt**" == local time, enables easy extraction of specific componants of a time, however, remember that POXIXlt objects are lists)

### Working with Dates

-   `as.Date("2016-01-01")` = 2016-01-01
-   `lubridate::ymd("2016-01-01")` or `lubridate::mdy` or `lubridate::dmy` = 2016-01-01

### Working with Datetimes & Timezones

-   `as.POSIXct("2016-01-01 12:00", "UTC")` = 2016-01-01 12:00:00
-   `strptime("2016/01/01 12:00",format = "%Y/%m/%d %H:%M")` = 0, 0, 12, 1, 0, 116, 5, 0, 0, PST, NA
-   `lubridate::ymd_hms("2016/01/01 21:22:22")` = 2016-01-01 21:22:22
-   `lubridate::ymd_hms("20160101 21:22:22")` = 2016-01-01 21:22:22
-   `lubridate::ymd_hms("2016-01-01 21:22:22", tz = "America/Los_Angeles")` = 2016-01-01 21:22:22

### Datetimes without Timezones (and `chron`)

The `chron` package may be helpful for these tasks, however, this may also be a suitable use of the POSIXlt class.

-   `chron::as.chron("2013-07-24 23:55:26")` = 1.591099710^{4}
-   `chron::as.chron("07/25/13 08:32:07", "%m/%d/%y %H:%M:%S")` = 1.591135610^{4}

### Using the `lubridate` package

The data we'll be using is from our lecture, but can be downloaded [here]({{ site.baseurl }}/data/mauna_loa_met_2001_minute.rda)

``` r
# let's load our climate data from our previous lesson:

load("data_output/mauna_loa_met_2001_minute.rda")

library(lubridate, warn.conflicts = F)
library(dplyr, warn.conflicts = F)

# we need to make a datetime column...let's use paste
mloa_2001$datetime <- paste0(mloa_2001$year,"-", mloa_2001$month, "-", mloa_2001$day," ", mloa_2001$hour24, ":", mloa_2001$min) # this makes a character column

# we can nest this within a lubridate function to convert directly to POSIXct
mloa_2001$datetime <- ymd_hm(paste0(mloa_2001$year,"-", mloa_2001$month, "-", mloa_2001$day," ", mloa_2001$hour24, ":", mloa_2001$min))

summary(mloa_2001)
```

    ##    filename         siteID            year          month
    ##  Length:459769      MLO:459769   Min.   :2001   Min.   : 1.000
    ##  Class :character                1st Qu.:2001   1st Qu.: 3.000
    ##  Mode  :character                Median :2001   Median : 6.000
    ##                                  Mean   :2001   Mean   : 6.474
    ##                                  3rd Qu.:2001   3rd Qu.:10.000
    ##                                  Max.   :2001   Max.   :12.000
    ##       day            hour24           min           windDir
    ##  Min.   : 1.00   Min.   : 0.00   Min.   : 0.00   Min.   :-999.0
    ##  1st Qu.: 8.00   1st Qu.: 5.00   1st Qu.:15.00   1st Qu.: 115.0
    ##  Median :15.00   Median :11.00   Median :30.00   Median : 156.0
    ##  Mean   :15.44   Mean   :11.43   Mean   :29.51   Mean   : 144.5
    ##  3rd Qu.:22.00   3rd Qu.:18.00   3rd Qu.:45.00   3rd Qu.: 236.0
    ##  Max.   :31.00   Max.   :23.00   Max.   :59.00   Max.   : 360.0
    ##  windSpeed_m_s       windSteady    baro_hPa        temp_C_2m
    ##  Min.   :-99.900   Min.   :-9   Min.   :-999.9   Min.   :-999.900
    ##  1st Qu.:  1.900   1st Qu.:-9   1st Qu.:-999.9   1st Qu.:   4.400
    ##  Median :  3.500   Median :-9   Median :-999.9   Median :   6.900
    ##  Mean   :  1.229   Mean   :-9   Mean   :-999.9   Mean   :   4.747
    ##  3rd Qu.:  5.900   3rd Qu.:-9   3rd Qu.:-999.9   3rd Qu.:   9.400
    ##  Max.   : 20.500   Max.   :-9   Max.   :-999.9   Max.   :  18.900
    ##    temp_C_10m      temp_C_towertop      rel_humid      precip_intens_mm_hr
    ##  Min.   :-999.90   Min.   :-999.900   Min.   :-99.00   Min.   :-99.0000
    ##  1st Qu.:   4.90   1st Qu.:   5.600   1st Qu.: 14.00   1st Qu.:  0.0000
    ##  Median :   6.90   Median :   7.200   Median : 28.00   Median :  0.0000
    ##  Mean   : -46.69   Mean   :   1.539   Mean   : 31.82   Mean   : -0.8066
    ##  3rd Qu.:   8.60   3rd Qu.:   8.800   3rd Qu.: 57.00   3rd Qu.:  0.0000
    ##  Max.   :  16.90   Max.   :  16.200   Max.   :138.00   Max.   : 60.0000
    ##     datetime
    ##  Min.   :2001-01-01 00:00:00
    ##  1st Qu.:2001-03-29 06:57:00
    ##  Median :2001-06-24 06:13:00
    ##  Mean   :2001-06-30 15:28:42
    ##  3rd Qu.:2001-10-07 00:34:00
    ##  Max.   :2001-12-31 23:59:00

``` r
# clean up the NA data (NA's are = -99 or -999 depending on data col)
df <- mloa_2001 %>%
  filter(!rel_humid == -99,
         !temp_C_2m == -999,
         !windSpeed_m_s == -99.9)


library(ggplot2)

df %>% sample_n(size=20000) %>%
  ggplot(.) +
  geom_point(aes(x=datetime, y=rel_humid, color=temp_C_2m), alpha=0.5) +
  viridis::scale_color_viridis() + ylim(0, 100)
```

    ## Warning: Removed 28 rows containing missing values (geom_point).

![pointplot]({{ site.baseurl }}/lectures/images/lubridate_basics-1.png)
