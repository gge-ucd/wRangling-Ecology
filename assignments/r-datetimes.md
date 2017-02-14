---
layout: page
element: assignment
title: Web Data to Datetimes & Timeseries
language: R
exercises: ''
---

Historical C0<sub>2</sub> Record from Vostok Ice Cores
------------------------------------------------------

How do we know the C0<sub>2</sub> levels are higher now than compared with natural cycles observed through time? Thankfully we have ice cores that date back over 400,000 years ago. By analyzing the tiny bubbles trapped for eons deep (*cores have been drilled as deep as 3,623 m!*) within the ice at known points in time (based on the depth of the ice layer), it's possible to reconstruct a record of C0<sub>2</sub> on Earth over a very long period of time.

These data are publically available as a simple text file [here](http://cdiac.ornl.gov/ftp/trends/co2/vostok.icecore.co2), and a full description of the metadata is [here](http://cdiac.ornl.gov/trends/co2/vostok.html).

Let's download and take a look!

``` r
library(readr)
df <- read_tsv(file = "http://cdiac.ornl.gov/ftp/trends/co2/vostok.icecore.co2", skip = 20, col_names = c("depth_m","ice_age_yr_BP", "air_age_yr_BP", "C02_conc_ppmv"))
```

    ## Parsed with column specification:
    ## cols(
    ##   depth_m = col_double(),
    ##   ice_age_yr_BP = col_integer(),
    ##   air_age_yr_BP = col_integer(),
    ##   C02_conc_ppmv = col_double()
    ## )

### Making a Nice `ggplot`

If we want to make a basic plot, we can use the following code to simply show the data as is. It works, but compare with code for `ggplot`. Notice that the `with()` function is just a way to "attach" the data so we don't have to use the <data@column> convention when writing our function calls.

``` r
#plot(df$depth_m, df$ice_age_yr_BP)

# baseplot
with(df, plot(x=air_age_yr_BP/1000, y=C02_conc_ppmv,
              type = "l", col="darkblue",
              ylab=expression(paste("C0"[2] ," Concentration (ppmv)"), sep=""),
              xlab="Age of Entrapped Air (kyr BP)",
              main=expression(paste("C0"[2]," through Time: Vostok Ice Core Data", sep="")), ylim=c(180, 420)))

# add another "layer" (similar to using the geom_ in ggplot)
with(df, points(x=air_age_yr_BP/1000, y=C02_conc_ppmv,
                xlab=NULL, ylab=NULL, pch=21, col="gray50",
     bg="skyblue2"))

# plot modern CO2 levels (notice we aren't using a data frame but giving a single data point location)
points(x=0, y=406, pch=16, col="red", cex=1.7)

# add some text
text(x=0, y = 406, labels = "C02 Level \n on Jan 31, 2017!",
     font = 4, col = "maroon", pos = 4)
```

![]({{ site.baseurl }}/assignments/images/baseplot-1.png)

Remember, to use these base plot options, you have to always call a `plot()` first, and then `points()` or `lines()`. It won't work if you try to do it the other way around. Also, the use of the `expression()` is a way to make formulas, scientific notation, etc. look correct in your plots.

Ok, now let's try something similar in a **ggplot** version, notice the differences? Similarities?

``` r
library(ggplot2)
library(dplyr)
```


``` r
library(viridis) # for nice color scheme

ggplot() +
  geom_line(data=df, aes(x=air_age_yr_BP/1000, y=C02_conc_ppmv),
                     color="gray20") +
  geom_point(data=df, aes(x=air_age_yr_BP/1000, y=C02_conc_ppmv, fill=depth_m), pch=21) +
  scale_fill_viridis() +
  scale_y_continuous(limits = c(180, 420)) +
  labs(x="Age of Entrapped Air (kyr BP)", y=expression(paste(C0[2]," Concentration (ppmv)", sep=""))) +
  #geom_smooth(data=df, aes(x=air_age_yr_BP/1000, y=C02_conc_ppmv)) +
  geom_hline(yintercept=406, col="red", lty=2) +
  geom_label(data=NULL, aes(x=20, y=406, label="Current C02 Level"),
             col="red", nudge_x = 30) + theme_bw()
```

![]({{ site.baseurl }}/assignments/images/ggplot_version-1.png)

### Map Where This Is

**Vostok, Antarctica** **-78.4645° S, 106.8340° E** **3488 m above MSL**

``` r
library(maps) # a mapping package
library(mapdata) # map data
library(measurements) # for converting data

# change the degree symbol to a space
xlat <- gsub(pattern = '°', replacement = '',x = '-78.4645°')
xlon <- gsub('°', '','106.8340°')

ice<-data.frame("x"=as.numeric(xlon), "y"=as.numeric(xlat))

# convert from decimal deg to deg_minute_second
#xlat <- measurements::conv_unit(xlat, from = 'dec_deg', to = 'deg_min_sec')
#xlon <- measurements::conv_unit(xlon, from = 'dec_deg', to = 'deg_min_sec')

# here's a nice way to simply see where your point is verbally...
map.where(database = "world", x=ice$x, y=ice$y)
```

    ## [1] "Antarctica"

``` r
# and an actual world map
map(database = "world", plot=TRUE, fill = TRUE, col="gray80") # just the map, no points
map.axes() # add axes
points(x = ice$x, y = ice$y, pch=21, bg="red", cex=2) # add the points
title(main = "Vostok, Antartica", sub = "Location of ice core data") # add a title
```

![]({{ site.baseurl }}/assignments/images/maps-1.png)

What About C0<sub>2</sub> Today?
--------------------------------

A good site to check the current C0<sub>2</sub> emission level is [here](https://www.co2.earth/). NOAA's [site](https://www.esrl.noaa.gov/gmd/ccgg/trends/monthly.html) provides trends across different time stamps, dating back to **1959** using the Mauna Loa Observatory measurents.

Let's pull the annual measurements using the same commands we used above.

``` r
library(dplyr)
library(viridis) # for colors

# notice here we can use the base R read.table() function, it automatically ignores any lines that start with "#"
df2 <- read.table(file = "ftp://aftp.cmdl.noaa.gov/products/trends/co2/co2_mm_mlo.txt", col.names = c("year", "mon", "dec_date", "avg_C02", "interpolated_C02", "trend_seas_corr", "no_days"))

# use dplyr to filter and summarize daily data to annual, get rid of missing/NAs (values -99)
df_ann <- df2 %>%
  filter(avg_C02 > 0) %>%
  group_by(year) %>%
  summarize(ann_C02=mean(avg_C02, na.rm=T))

# plot
ggplot() + geom_line(data=df_ann, aes(x=year, y=ann_C02), color="darkblue") +
  labs(x="Year", y=expression(paste(C0[2]," Concentration (ppmv)", sep=""))) +
  geom_smooth(data=df_ann, aes(x=year, y=ann_C02)) +
  geom_point(data=df_ann, aes(x=year, y=ann_C02, fill=ann_C02), pch=21, cex=2.5, alpha=0.8) + scale_fill_viridis() +
    geom_hline(yintercept=406, col="red", lty=2) + geom_label(data=NULL, aes(x=1970, y=406, label="Current C02 Level"), col="red", nudge_x = 30)  +
  scale_x_continuous(breaks = seq(1955,2017,5), labels = seq(1955,2017,5)) + ggtitle("C02 At Mauna Loa Since 1958")
```

    ## `geom_smooth()` using method = 'loess'

![]({{ site.baseurl }}/assignments/images/getC02_currentdata-1.png)

Fine Scale Meterological Data
-----------------------------

There's an abundance of meterological data available for download now, but since we are still thinking about C0<sub>2</sub>, let's pull some fine-scale meterological data from the Mauna Loa station. This is met data collected every **minute** for a whole year.

Metadata for this is [here](ftp://aftp.cmdl.noaa.gov/data/meteorology/in-situ/README). Data used in this example is [here (minute scale met data)](ftp://aftp.cmdl.noaa.gov/data/meteorology/in-situ/mlo/2001/)

### Downloading lots of files from an FTP site

**Important...we didn't do this in class! Just showing it can be done**

To actually go download all these in one go, try using some UNIX/terminal code! This will most likely only work in OSX, but you should be able to install `wget` on most any platform. However, you don't have to do this, because this data is already available for download on github [here]()

``` r
# change directory to current dir
system("cd ~/Documents/github/teaching/wRangling_Lectures/data")

# get all files in a single dir
system("wget --no-verbose --no-parent --recursive --level=1 --no-directories ftp://aftp.cmdl.noaa.gov/data/meteorology/in-situ/mlo/2001/")
```

### Aggregating Lots of Data and Multiple Files

So we have 12 files, each a month worth of measurements taken every minute, which is roughly *(`44,000` measurements `*` `12` months)*, or about a half million lines of data. Give or take.

First step, how do we read in this many files at once and merge them?

### Read in [Multiple Files](http://serialmentor.com/blog/2016/6/13/reading-and-combining-many-tidy-data-files-in-R)

``` r
require(readr)  # for read_csv()
require(dplyr)  # for mutate()
require(tidyr)  # for unnest()
require(purrr)  # for map(), reduce()

folder <- "data/2001_mauna_loa_met_data" # the folder where the data lives
files_list <- dir(path = folder, pattern = "*.txt") # list all files in that folder ending with .txt

# Option 1:  Simple version, read all files in as one dataframe
data <- files_list %>%
  purrr::map(~read.table(file.path(folder, .), header = FALSE)) %>%    # read in all the files individually
  reduce(rbind)       # reduce with rbind into one dataframe

# add column names to the dataframe
colnames(data)<-c("siteID", "year", "month", "day", "hour24", "min", "windDir",   "windSpeed_m_s", "windSteady", "baro_hPa", "temp_C_2m", "temp_C_10m", "temp_C_towertop", "rel_humid", "precip_intens_mm_hr")

head(data)
dim(data)

## Option 2: read in files & add column with the filename along with all the data from that file, then combine into one dataframe
data <- data_frame(filename = files_list) %>% # create dataframe with column of the filenames
  mutate(file_contents = map(filename, # read files in
                             ~read.table(file.path(folder, .), header = FALSE))) %>%
  unnest # this unlists all the list of dataframe

# add column names
colnames(data)<-c("filename", "siteID", "year", "month", "day", "hour24", "min", "windDir",   "windSpeed_m_s", "windSteady", "baro_hPa", "temp_C_2m", "temp_C_10m", "temp_C_towertop", "rel_humid", "precip_intens_mm_hr")

dim(data)

# save this as an rds file and an rda file!
mloa_2001 <- data # remember with rda we can't rename the dataframe when we "load()".

dplyr::write_rds(mloa_2001, path = "data_output/mauna_loa_met_2001_minute.rds", compress = "gz")

save(mloa_2001, file = "data_output/mauna_loa_met_2001_minute.rda", compress = TRUE)
```

Wow that's cool!

Okay, but next steps will be playin with some of this data insanity...stay tuned for the actual DateTime lesson next lecture (or script shared in-between).


{% include reading.html %}

{% include assignment.html %}
