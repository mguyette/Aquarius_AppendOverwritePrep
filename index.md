
On rare occasions, the wrong template has been used on a [YSI
EXO2](https://www.ysi.com/EXO2) sonde and parameters get loaded into the
wrong time series in AQUARIUS Time-Series. When this happens, we would
rather overwrite the data from the wrong parameter with the data from
the correct parameter. The overwriteappend operation in the AQUARIUS
Time-Series Acquisition API allows you to completely overwrite data
within a time series. We use the Swagger UI for this process, and the
input is a JSON object that holds the unique ID for the time series, the
data points, and the time period. This project prepares a JSON object to
be input into the Swagger UI for the AQUARIUS Time-Series Acquisition
API.

The script (available on GitHub [here](OverwriteAppend_PrepDat.R))
requires a telemetry file (.dat), the time series Unique ID, and the
start and end time of the period you would like to overwrite with new
data.

Note that the script in the GitHub repo is designed to allow users to
easily jump to the lines of code that need to be changed for each use by
making use of the [Code
Sections](https://support.rstudio.com/hc/en-us/articles/200484568-Code-Folding-and-Sections)
functionality in RStudio (at least four \# in a row at the end of line
creates a new Section).

## Input data

The script is designed to accomodate .dat telemetry files downloaded
from EXO2 YSI deployments. The program we use results in the following
format:

``` r
dat <- read_csv("./dat_files/IRLML02_WQ_Hourly.dat", skip = 1)
```

|      TIMESTAMP      | RECORD | site\_id | batt\_volt | YSI\_TempC | YSI\_PH | YSI\_ODOmgL | YSI\_ODOpct | YSI\_SPConduScm | YSI\_Salppt | YSI\_Depthm | YSI\_ChlugL | YSI\_TurbFNU | YSI\_fDOMppb | YSI\_BattVolt | YSI\_CblVolt | YSI\_WipePos | YSITop\_TempC | YSITop\_PH | YSITop\_ODOmgL | YSITop\_ODOpct | YSITop\_SPConduScm | YSITop\_Salppt | YSITop\_Depthm | YSITop\_ChlugL | YSITop\_TurbFNU | YSITop\_fDOMppb | YSITop\_BattVolt | YSITop\_CblVolt | YSITop\_WipePos | SUNA\_NO3uM | SUNA\_NO3mgL | SUNA\_Ltspecavg | SUNA\_Dkspecavg | SUNA\_LampTempC | SUNA\_SpecTempC | SUNA\_LampTime | SUNA\_RelHumidty | SUNA\_IntVolt | SUNA\_RegVolt | SUNA\_SupVolt |
| :-----------------: | :----: | :------: | :--------: | :--------: | :-----: | :---------: | :---------: | :-------------: | :---------: | :---------: | :---------: | :----------: | :----------: | :-----------: | :----------: | :----------: | :-----------: | :--------: | :------------: | :------------: | :----------------: | :------------: | :------------: | :------------: | :-------------: | :-------------: | :--------------: | :-------------: | :-------------: | :---------: | :----------: | :-------------: | :-------------: | :-------------: | :-------------: | :------------: | :--------------: | :-----------: | :-----------: | :-----------: |
|         TS          |   RN   |    NA    |     NA     |     NA     |   NA    |     NA      |     NA      |       NA        |     NA      |     NA      |     NA      |      NA      |      NA      |      NA       |      NA      |      NA      |      NA       |     NA     |       NA       |       NA       |         NA         |       NA       |       NA       |       NA       |       NA        |       NA        |        NA        |       NA        |       NA        |     NA      |      NA      |       NA        |       NA        |       NA        |       NA        |       NA       |        NA        |      NA       |      NA       |      NA       |
|         NA          |   NA   |   Smp    |    Smp     |    Smp     |   Smp   |     Smp     |     Smp     |       Smp       |     Smp     |     Smp     |     Smp     |     Smp      |     Smp      |      Smp      |     Smp      |     Smp      |      Smp      |    Smp     |      Smp       |      Smp       |        Smp         |      Smp       |      Smp       |      Smp       |       Smp       |       Smp       |       Smp        |       Smp       |       Smp       |     Smp     |     Smp      |       Smp       |       Smp       |       Smp       |       Smp       |      Smp       |       Smp        |      Smp      |      Smp      |      Smp      |
| 2017-02-16 12:00:00 |   0    |   4526   |   13.82    |   20.06    |   7.7   |    6.04     |    82.1     |    53783.44     |    35.6     |    1.66     |    1.69     |     9.75     |    35.69     |     6.09      |    13.32     |     1.17     |     20.49     |    7.81    |      6.3       |      86.2      |      53788.04      |      35.6      |      0.65      |      2.64      |      10.6       |      35.89      |       6.34       |      13.33      |       1.2       |     NAN     |     NAN      |       NAN       |       NAN       |       NAN       |       NAN       |      NAN       |       NAN        |      NAN      |      NAN      |      NAN      |
| 2017-02-16 13:00:00 |   1    |   4526   |   13.82    |   20.15    |  7.71   |    6.08     |    82.7     |    53788.78     |    35.61    |    1.64     |    1.08     |     8.1      |    35.46     |     6.09      |    13.29     |     1.16     |     20.64     |    7.81    |      6.3       |      86.5      |      53813.8       |     35.62      |      0.64      |      2.31      |      9.37       |      36.05      |       6.34       |      13.3       |      1.19       |     NAN     |     NAN      |       NAN       |       NAN       |       NAN       |       NAN       |      NAN       |       NAN        |      NAN      |      NAN      |      NAN      |
| 2017-02-16 14:00:00 |   2    |   4526   |   13.88    |   20.64    |  7.74   |    6.11     |    83.9     |    53812.01     |    35.62    |    1.65     |    1.85     |     8.18     |    34.39     |     6.09      |    13.32     |     1.16     |     20.83     |    7.81    |      6.31      |      86.9      |      53831.82      |     35.63      |      0.64      |      1.94      |      8.34       |      36.03      |       6.34       |      13.36      |      1.19       |     NAN     |     NAN      |       NAN       |       NAN       |       NAN       |       NAN       |      NAN       |       NAN        |      NAN      |      NAN      |      NAN      |
| 2017-02-16 15:00:00 |   3    |   4526   |   13.82    |   20.92    |  7.76   |    6.21     |    85.8     |     53802.3     |    35.61    |    1.65     |    1.12     |     7.7      |    34.57     |     6.09      |    13.29     |     1.16     |     20.98     |    7.81    |      6.22      |      85.9      |      53828.55      |     35.63      |      0.65      |      1.87      |      7.67       |       36        |       6.34       |      13.33      |      1.19       |     NAN     |     NAN      |       NAN       |       NAN       |       NAN       |       NAN       |      NAN       |       NAN        |      NAN      |      NAN      |      NAN      |

## Clean the data

The structure of the telemetry file requires some very basic data
cleaning. Here we remove the first two rows, which do not contain value
data, and convert data types from character to POSIXct and numeric.

``` r
dat <- dat %>% 
  slice(3:n()) %>% 
  mutate(TIMESTAMP = as.POSIXct(TIMESTAMP, tz = "EST")) %>% 
  mutate_at(vars(RECORD:SUNA_SupVolt), as.numeric)
```

## Subset the data

After identifying the AQUARIUS parameter name and label used for the
time series in question, we use a [crosswalk
table](TelemetryParameters.csv) of AQUARIUS parameter names and labels
with telemetry column names to select the appropriate column from the
data frame and rename the columns. The new column names are required to
ensure that the Points section of the JSON object has the correct
labels. Note that you would need to customize the crosswalk table in
order to use this in your own AQUARIUS implementation.

``` r
# Use the Parameter and Label as shown in Aquarius
parameter <- "Sp Cond"
label <- "YSI"

# Load crosswalk table of telemetry file columns and parameter/label combinations
xwalk <- read.csv("TelemetryParameters.csv")

# Get column name
column <- as.character(xwalk$Telemetry_Column[xwalk$Parameter == parameter & 
                                              xwalk$Label == label])

# Subset the dat file to include only the datetime and the parameter of interest
# Rename the columns
dat <- dat %>% 
  select(Time = TIMESTAMP, Value = column)
```

|        Time         | Value |
| :-----------------: | :---: |
| 2017-02-16 12:00:00 | 53783 |
| 2017-02-16 13:00:00 | 53789 |
| 2017-02-16 14:00:00 | 53812 |
| 2017-02-16 15:00:00 | 53802 |
| 2017-02-16 16:00:00 | 53808 |
| 2017-02-16 17:00:00 | 53800 |

After identifying the start and end time for the period requiring
overwriting, we subset the data frame further.

``` r
# Start datetime of period requiring overwrite, inclusive
# Use format shown in the second argument
starttime <- as.POSIXct("2017-08-09 14:00:00", "%Y-%m-%d %H:%M:%S", tz = "EST")

# End datetime of period requiring overwrite, inclusive
# Use format shown in the second argument
endtime <- as.POSIXct("2017-08-10 07:00:00", "%Y-%m-%d %H:%M:%S", tz = "EST")

# Subset the data set based on the these time contraints
cut <- dat %>% 
  filter(Time >= starttime, Time <= endtime)
```

|        Time         | Value |
| :-----------------: | :---: |
| 2017-08-09 14:00:00 | 56438 |
| 2017-08-09 15:00:00 | 56275 |
| 2017-08-09 16:00:00 | 56173 |
| 2017-08-09 17:00:00 | 55672 |
| 2017-08-09 18:00:00 | 55703 |
| 2017-08-09 19:00:00 | 55525 |

## Store timestamps as ISO 8601 in GMT

Timestamps must be stored in ISO 8601 format in GMT in order to be
uploaded to the API.

``` r
cut$Time <- format(cut$Time,"%Y-%m-%dT%H:%M:%SZ", tz = "GMT")
starttime_iso <- format(starttime,"%Y-%m-%dT%H:%M:%SZ", tz = "GMT")
endtime_iso <- format(endtime + 60,"%Y-%m-%dT%H:%M:%SZ", tz = "GMT")
```

The starttime was originally 2017-08-09 14:00:00, and after conversion
it is 2017-08-09T19:00:00Z. The endtime follows the same pattern, and
the Date column in the dataframe is now formatted correctly for the API.

|         Time         | Value |
| :------------------: | :---: |
| 2017-08-09T19:00:00Z | 56438 |
| 2017-08-09T20:00:00Z | 56275 |
| 2017-08-09T21:00:00Z | 56173 |
| 2017-08-09T22:00:00Z | 55672 |
| 2017-08-09T23:00:00Z | 55703 |
| 2017-08-10T00:00:00Z | 55525 |

## Get the time series Unique ID

The API makes use of the 32-character time series Unique ID, found by
selecting View/Edit Details under the hamburger button for the time
series in question and navigating to the bottom of the Time Series
Attributes section.

``` r
uid <- "9259636e1fb9425f9934b355a785d7e4"
```

## Create a data frame that is built around the API’s JSON structure requirements

The JSON object that can be used in the API has three distinct parts: a
Unique ID, the data Points, and the Time Range. We first create a nested
data frame with the JSON structure.

``` r
## Part 1: Unique ID
df_json <- data.frame(UniqueID = uid)

## Part 2: Points
df_json$Points <- list(cut)

## Part 3: Time Range
df_json$TimeRange <- data.frame(Start = starttime_iso,
                              End = endtime_iso)

str(df_json)
```

    ## 'data.frame':    1 obs. of  3 variables:
    ##  $ UniqueID : Factor w/ 1 level "9259636e1fb9425f9934b355a785d7e4": 1
    ##  $ Points   :List of 1
    ##   ..$ :Classes 'spec_tbl_df', 'tbl_df', 'tbl' and 'data.frame':  18 obs. of  2 variables:
    ##   .. ..$ Time : chr  "2017-08-09T19:00:00Z" "2017-08-09T20:00:00Z" "2017-08-09T21:00:00Z" "2017-08-09T22:00:00Z" ...
    ##   .. ..$ Value: num  56438 56275 56173 55672 55703 ...
    ##  $ TimeRange:'data.frame':   1 obs. of  2 variables:
    ##   ..$ Start: Factor w/ 1 level "2017-08-09T19:00:00Z": 1
    ##   ..$ End  : Factor w/ 1 level "2017-08-10T12:01:00Z": 1

## Convert to a JSON object

Finally, we convert the nested data frame into a JSON object.

``` r
json_for_export <- jsonlite::toJSON(df_json, pretty = T)
json_for_export
```

    ## [
    ##   {
    ##     "UniqueID": "9259636e1fb9425f9934b355a785d7e4",
    ##     "Points": [
    ##       {
    ##         "Time": "2017-08-09T19:00:00Z",
    ##         "Value": 56437.59
    ##       },
    ##       {
    ##         "Time": "2017-08-09T20:00:00Z",
    ##         "Value": 56274.89
    ##       },
    ##       {
    ##         "Time": "2017-08-09T21:00:00Z",
    ##         "Value": 56172.57
    ##       },
    ##       {
    ##         "Time": "2017-08-09T22:00:00Z",
    ##         "Value": 55671.63
    ##       },
    ##       {
    ##         "Time": "2017-08-09T23:00:00Z",
    ##         "Value": 55702.83
    ##       },
    ##       {
    ##         "Time": "2017-08-10T00:00:00Z",
    ##         "Value": 55525.36
    ##       },
    ##       {
    ##         "Time": "2017-08-10T01:00:00Z",
    ##         "Value": 55425.31
    ##       },
    ##       {
    ##         "Time": "2017-08-10T02:00:00Z",
    ##         "Value": 55656.48
    ##       },
    ##       {
    ##         "Time": "2017-08-10T03:00:00Z",
    ##         "Value": 55573.25
    ##       },
    ##       {
    ##         "Time": "2017-08-10T04:00:00Z",
    ##         "Value": 54719.39
    ##       },
    ##       {
    ##         "Time": "2017-08-10T05:00:00Z",
    ##         "Value": 54777.54
    ##       },
    ##       {
    ##         "Time": "2017-08-10T06:00:00Z",
    ##         "Value": 55171.11
    ##       },
    ##       {
    ##         "Time": "2017-08-10T07:00:00Z",
    ##         "Value": 55200.8
    ##       },
    ##       {
    ##         "Time": "2017-08-10T08:00:00Z",
    ##         "Value": 55211.1
    ##       },
    ##       {
    ##         "Time": "2017-08-10T09:00:00Z",
    ##         "Value": 54981.19
    ##       },
    ##       {
    ##         "Time": "2017-08-10T10:00:00Z",
    ##         "Value": 56263.78
    ##       },
    ##       {
    ##         "Time": "2017-08-10T11:00:00Z",
    ##         "Value": 56230.38
    ##       },
    ##       {
    ##         "Time": "2017-08-10T12:00:00Z",
    ##         "Value": 55932.91
    ##       }
    ##     ],
    ##     "TimeRange": {
    ##       "Start": "2017-08-09T19:00:00Z",
    ##       "End": "2017-08-10T12:01:00Z"
    ##     }
    ##   }
    ## ]

## Use the JSON object in the AQUARIUS Time-Series Acquisition API

To execute the overwriteappend operation in the API using Swagger UI,
you simply paste the JSON object into the body of the Parameters
section, paste the Unique ID and Time Period from the JSON object into
their respective boxes, and run it.
