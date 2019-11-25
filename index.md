
This project prepares a json object to be input into the Swagger UI for the AQUARIUS Acquisition API. This script requires a telemetry file (.dat), the time series Unique ID, and the start and end time of the period you would like to overwrite with new data.

Note that the \[script\] in the GitHub repo is designed to allow users to easily jump to the lines of code that need to be changed for each use by making use of the [Code Sections](https://support.rstudio.com/hc/en-us/articles/200484568-Code-Folding-and-Sections) functionality in RStudio (at least four \# in a row at the end of line creates a new Section).

The script is designed to accomodate .dat telemetry files downloaded from EXO2 YSI deployments. The format of these files is like this:

``` r
dat <- read_csv("./dat_files/SJR_US_Hell_N_Blazes_CM_WQ_Hourly.dat", skip = 1)
```

<table style="width:100%;">
<colgroup>
<col width="5%" />
<col width="2%" />
<col width="2%" />
<col width="2%" />
<col width="2%" />
<col width="2%" />
<col width="3%" />
<col width="4%" />
<col width="3%" />
<col width="3%" />
<col width="2%" />
<col width="2%" />
<col width="3%" />
<col width="3%" />
<col width="3%" />
<col width="3%" />
<col width="3%" />
<col width="3%" />
<col width="3%" />
<col width="4%" />
<col width="4%" />
<col width="4%" />
<col width="4%" />
<col width="3%" />
<col width="4%" />
<col width="3%" />
<col width="3%" />
<col width="3%" />
</colgroup>
<thead>
<tr class="header">
<th align="center">TIMESTAMP</th>
<th align="center">RECORD</th>
<th align="center">site_id</th>
<th align="center">batt_volt</th>
<th align="center">YSI_TempC</th>
<th align="center">YSI_PH</th>
<th align="center">YSI_ODOmgL</th>
<th align="center">YSI_SPConduScm</th>
<th align="center">YSI_Depthm</th>
<th align="center">YSI_RelChlRFU</th>
<th align="center">YSI_BGAPC</th>
<th align="center">YSI_BGAPE</th>
<th align="center">YSI_TurbFNU</th>
<th align="center">YSI_fDOMppb</th>
<th align="center">YSI_BattVolt</th>
<th align="center">YSI_CblVolt</th>
<th align="center">YSI_WipePos</th>
<th align="center">SUNA_NO3uM</th>
<th align="center">SUNA_NO3mgL</th>
<th align="center">SUNA_Ltspecavg</th>
<th align="center">SUNA_Dkspecavg</th>
<th align="center">SUNA_LampTempC</th>
<th align="center">SUNA_SpecTempC</th>
<th align="center">SUNA_LampTime</th>
<th align="center">SUNA_RelHumidty</th>
<th align="center">SUNA_IntVolt</th>
<th align="center">SUNA_RegVolt</th>
<th align="center">SUNA_SupVolt</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="center">TS</td>
<td align="center">RN</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">NA</td>
</tr>
<tr class="even">
<td align="center">NA</td>
<td align="center">NA</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
<td align="center">Smp</td>
</tr>
<tr class="odd">
<td align="center">2019-05-29 09:00:00</td>
<td align="center">0</td>
<td align="center">6000</td>
<td align="center">13.84</td>
<td align="center">29.47</td>
<td align="center">7.33</td>
<td align="center">3.74</td>
<td align="center">746.75</td>
<td align="center">0.41</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">192.9</td>
<td align="center">6.23</td>
<td align="center">12.96</td>
<td align="center">1.19</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
</tr>
<tr class="even">
<td align="center">2019-05-29 10:00:00</td>
<td align="center">1</td>
<td align="center">6000</td>
<td align="center">13.86</td>
<td align="center">29.85</td>
<td align="center">7.38</td>
<td align="center">4.49</td>
<td align="center">784.93</td>
<td align="center">0.4</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">188</td>
<td align="center">6.23</td>
<td align="center">13.48</td>
<td align="center">1.21</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
</tr>
<tr class="odd">
<td align="center">2019-05-29 11:00:00</td>
<td align="center">2</td>
<td align="center">6000</td>
<td align="center">13.44</td>
<td align="center">30.82</td>
<td align="center">7.45</td>
<td align="center">5.06</td>
<td align="center">784.8</td>
<td align="center">0.39</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">187.2</td>
<td align="center">6.24</td>
<td align="center">13.05</td>
<td align="center">1.2</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
</tr>
<tr class="even">
<td align="center">2019-05-29 12:00:00</td>
<td align="center">3</td>
<td align="center">6000</td>
<td align="center">13.41</td>
<td align="center">31.73</td>
<td align="center">7.48</td>
<td align="center">5.4</td>
<td align="center">765.88</td>
<td align="center">0.38</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">0</td>
<td align="center">187.2</td>
<td align="center">6.24</td>
<td align="center">13.02</td>
<td align="center">1.19</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
<td align="center">NAN</td>
</tr>
</tbody>
</table>

Classes 'spec\_tbl\_df', 'tbl\_df', 'tbl' and 'data.frame': 25 obs. of 28 variables: $ TIMESTAMP : chr "TS" NA "2019-05-29 09:00:00" "2019-05-29 10:00:00" ... $ RECORD : chr "RN" NA "0" "1" ... $ site\_id : chr NA "Smp" "6000" "6000" ... $ batt\_volt : chr NA "Smp" "13.84" "13.86" ... $ YSI\_TempC : chr NA "Smp" "29.47" "29.85" ... $ YSI\_PH : chr NA "Smp" "7.33" "7.38" ... $ YSI\_ODOmgL : chr NA "Smp" "3.74" "4.49" ... $ YSI\_SPConduScm : chr NA "Smp" "746.75" "784.93" ... $ YSI\_Depthm : chr NA "Smp" "0.41" "0.4" ... $ YSI\_RelChlRFU : chr NA "Smp" "0" "0" ... $ YSI\_BGAPC : chr NA "Smp" "0" "0" ... $ YSI\_BGAPE : chr NA "Smp" "0" "0" ... $ YSI\_TurbFNU : chr NA "Smp" "0" "0" ... $ YSI\_fDOMppb : chr NA "Smp" "192.9" "188" ... $ YSI\_BattVolt : chr NA "Smp" "6.23" "6.23" ... $ YSI\_CblVolt : chr NA "Smp" "12.96" "13.48" ... $ YSI\_WipePos : chr NA "Smp" "1.19" "1.21" ... $ SUNA\_NO3uM : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_NO3mgL : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_Ltspecavg : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_Dkspecavg : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_LampTempC : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_SpecTempC : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_LampTime : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_RelHumidty: chr NA "Smp" "NAN" "NAN" ... $ SUNA\_IntVolt : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_RegVolt : chr NA "Smp" "NAN" "NAN" ... $ SUNA\_SupVolt : chr NA "Smp" "NAN" "NAN" ... - attr(\*, "spec")= .. cols( .. TIMESTAMP = col\_character(), .. RECORD = col\_character(), .. site\_id = col\_character(), .. batt\_volt = col\_character(), .. YSI\_TempC = col\_character(), .. YSI\_PH = col\_character(), .. YSI\_ODOmgL = col\_character(), .. YSI\_SPConduScm = col\_character(), .. YSI\_Depthm = col\_character(), .. YSI\_RelChlRFU = col\_character(), .. YSI\_BGAPC = col\_character(), .. YSI\_BGAPE = col\_character(), .. YSI\_TurbFNU = col\_character(), .. YSI\_fDOMppb = col\_character(), .. YSI\_BattVolt = col\_character(), .. YSI\_CblVolt = col\_character(), .. YSI\_WipePos = col\_character(), .. SUNA\_NO3uM = col\_character(), .. SUNA\_NO3mgL = col\_character(), .. SUNA\_Ltspecavg = col\_character(), .. SUNA\_Dkspecavg = col\_character(), .. SUNA\_LampTempC = col\_character(), .. SUNA\_SpecTempC = col\_character(), .. SUNA\_LampTime = col\_character(), .. SUNA\_RelHumidty = col\_character(), .. SUNA\_IntVolt = col\_character(), .. SUNA\_RegVolt = col\_character(), .. SUNA\_SupVolt = col\_character() .. )

Data Cleaning
-------------

The \#\# Clean up the data frame dat &lt;- dat\[-c(1:2),\] dat*T**I**M**E**S**T**A**M**P* &lt; −*a**s*.*P**O**S**I**X**c**t*(*d**a**t*TIMESTAMP,tz = "EST") dat\[,2:length(dat)\] &lt;- sapply(dat\[,2:length(dat)\], as.numeric)

==&gt; CHANGE THE PARAMETER AND LABEL HERE
------------------------------------------

Use the Parameter and Label as shown in Aquarius
------------------------------------------------

parameter &lt;- "Sp Cond" label &lt;- "YSI"

Load crosswalk table of telemetry file columns and
--------------------------------------------------

parameter/label combinations
----------------------------

xwalk &lt;- read.csv("TelemetryParameters.csv")

Get column name
---------------

column &lt;- as.character(xwalk*T**e**l**e**m**e**t**r**y*<sub>*C*</sub>*o**l**u**m**n*\[*x**w**a**l**k*Parameter == parameter & xwalk$Label == label\])

Subset the dat file to include only the datetime and the
--------------------------------------------------------

parameter of interest
---------------------

dat &lt;- dat\[,c("TIMESTAMP",column)\]

==&gt; CHANGE THE UNIQUE ID HERE
--------------------------------

Go to the hamburger button for the time series and select
---------------------------------------------------------

View/Edit Details. Cut and paste the Unique ID from the
-------------------------------------------------------

bottom of the Time Series Attributes section of the
---------------------------------------------------

uid &lt;- "9259636e1fb9425f9934b355a785d7e4"

==&gt; CHANGE THE START TIME FOR PERIOD REQUIRING
-------------------------------------------------

#### OVERWRITE HERE

Start datetime of period requiring overwrite
--------------------------------------------

Use format shown in the second argument
---------------------------------------

starttime &lt;- as.POSIXct("2019-05-29 08:00:00","%Y-%m-%d %H:%M:%S", tz = "EST")

==&gt; CHANGE THE END TIME FOR PERIOD REQUIRING
-----------------------------------------------

#### OVERWRITE HERE

End datetime of period requiring overwrite
------------------------------------------

Use format shown in the second argument
---------------------------------------

endtime &lt;- as.POSIXct("2019-05-30 07:00:00","%Y-%m-%d %H:%M:%S", tz = "EST")

Cut down data set
-----------------

cut &lt;- dat\[dat$TIMESTAMP &gt;= starttime & dat$TIMESTAMP &lt;= endtime,\]

Change column names
-------------------

names(cut) &lt;- c("Time","Value")

Format Time to ISO 8601 timestamp and convert to GMT (from EST)
---------------------------------------------------------------

cut*T**i**m**e* &lt; −*f**o**r**m**a**t*(*c**u**t*Time,"%Y-%m-%dT%H:%M:%SZ", tz = "GMT") starttime\_iso &lt;- format(starttime,"%Y-%m-%dT%H:%M:%SZ", tz = "GMT") endtime\_iso &lt;- format(endtime + 60,"%Y-%m-%dT%H:%M:%SZ", tz = "GMT")

Create a data frame that is built around the json structure
-----------------------------------------------------------

requirements as defined by Aquatic Informatics
----------------------------------------------

Part 1: Unique ID
-----------------

df\_json &lt;- data.frame(UniqueID = uid)

Part 2: Points
--------------

df\_json$Points &lt;- list(cut)

Part 3: Time Range
------------------

df\_json$TimeRange &lt;- data.frame(Start = starttime\_iso, End = endtime\_iso)

Create a JSON object holding the new data
-----------------------------------------

json\_for\_export &lt;- jsonlite::toJSON(df\_json,pretty = T)

==&gt; CHANGE JSON FILE LOCATION AND FILE NAME HERE
---------------------------------------------------

You MUST include .json at the end of the file name
--------------------------------------------------

Save file to disk
-----------------

write(json\_for\_export, file = "./JSON\_files/HBI\_SpCond.json")
