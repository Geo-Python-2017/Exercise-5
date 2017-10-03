# Exercise-5: Data analysis with Pandas 

The exercise for this week is meant to help you to understand how to use [Pandas - Python Data Analysis Library](http://pandas.pydata.org/)
to do some basic data analysis and data manipulations using **real data**. In this week's exercise you are asked to analyze
temperature data from Helsinki (in Southern Finland) and Rovaniemi (northest municipality in Finland)
and to explore how their summers have differed in 2016.

After making your changes, you will need to upload your files to GitHub.
The answers to the questions in this week's exercise should be given by modifying the document in places where asked.

 - **Exercise 5 is due by the start of lecture on 11.10.**
 - Don't forget to check out the [hints for this week's exercise](https://geo-python.github.io/2017/lessons/L5/exercise-5-hints.html) if you're having trouble.
 - Scores on this exercise are out of 20 points.

## Data

For the Exercise 5 we will use NOAA weather data obtained from https://www.ncdc.noaa.gov/cdo-web/search?datasetid=GHCND
(file format was converted to CSV for convenience). You should download the datafile into your own computer to do the
data analysis on it.

You can read the full description of our data from a [3505doc.txt] -file that
contains the description for each attribute.

The first five rows of the data looks like following:

```
USAF,WBAN,YR--MODAHRMN,DIR,SPD,GUS,CLG,SKC,L,M,H,VSB,MW,MW,MW,MW,AW,AW,AW,AW,W,TEMP,DEWP,SLP,ALT,STP,MAX,MIN,PCP01,PCP06,PCP24,PCPXX,SD
028450,99999,201705010000,174,10,14,***,***,*,*,*,2.2,**,**,**,**,67,**,**,**,8,31,31,1009.2,*****,984.1,***,***,*****,*****,*****,*****,35
028450,99999,201705010020,180,10,***,4,***,*,*,*,2.9,**,**,**,**,10,**,**,**,*,30,30,******,29.74,******,***,***,*****,*****,*****,*****,**
028450,99999,201705010050,190,10,***,4,***,*,*,*,2.1,**,**,**,**,10,**,**,**,*,30,30,******,29.74,******,***,***,*****,*****,*****,*****,**
028450,99999,201705010100,188,12,16,***,***,*,*,*,3.2,**,**,**,**,77,**,**,**,*,31,30,1009.1,*****,984.0,***,***,*****,*****,*****,*****,35
```

**NOTICE**: the data includes \*\*\* characters that represent NoData values.

The most important attributes for this exercise are:

 - **USAF** = the station ID number
   - 028450 : Rovaniemi
   - 029980 : Helsinki Kumpula
 - **YR--MODAHRMN** = Year-Month-Day-Hour-Minute in Greenwich Mean Time (GMT)
 - **TEMP** = Temperature in Fahrenheit
 - **MAX** = Maximum temperature in Fahrenheit
 - **MIN** = Minimum temperature in Fahrenheit

## Problem 1 - Basic statistics of the data (5 points)

In this problem your task is to explore the data [6153237444115dat.csv] by reading the data into Pandas
and conduct following tasks / answer to following questions:

- Read the data into a variable called `data`.
  - When reading the data, it is important that you tell to Pandas that no-data values are specified with varying number of \* characters.
  - You can do this by specifying a following parameter in the `read_csv()` -function: `na_values=['*', '**', '***', '****', '*****', '******']`
- How many rows is there in the data?
- What are the column names?
- What are the datatypes of the columns?
- What is the mean Fahrenheit temperature in the data? (`TEMP` column)
- What is the standard deviation of the Maximum temperature? (`MAX` column)
- How many unique stations exists in the data?

You should write your codes into a `data_exploration.py` file and print the answers for the questions above
inside the script.

- Upload the script to your GitHub repository for Exercise 5
- Remember to comment well your code!

## Problem 2 - Data manipulation (5 points)

Similarly as in earlier exercises the temperatures in our data are represented in Fahrenheit, hence,
you need to convert the temperatures into Celsius.

 - Select from the `data` columns `USAF, YR--MODAHRMN, TEMP, MAX, MIN` and assign them into a new variable called `selected`
 - Remove all rows from `selected` that has NoData in column `TEMP` using `dropna()` -function
 - Convert the Fahrenheit temperatures from `TEMP` column into a new column `Celsius` using the conversion formula:
   - ![](img/Fahrenheit_to_Celsius_formula.PNG)
 - Round the values in `Celsius` to have 0 decimals
 - Convert the `Celsius` values into integers

You can add your codes into a `data_exploration.py` file.

- Upload the script to your GitHub repository for Exercise-5
- Remember to comment well your code!

## Problem 3 - Data selection (5 points)

In this problem you should select specific columns from the data and divide the data into separate subsets for
different stations.

- Divide the selection into two separate datasets:
  - Select all rows from `selected` DataFrame into variable called `kumpula` where the `USAF` code is `29980`
  - Select all rows from `selected` DataFrame into variable called `rovaniemi` where the `USAF` code is `28450`
- Save `kumpula` DataFrame into `Kumpula_temps_May_Aug_2017.csv` file (CSV format) (separated with `,`)
- Save `rovaniemi` DataFrame into `Rovaniemi_temps_May_Aug_2017.csv` file (CSV format) (separated with `,`)
- Upload your csv files into your GitHub repository for Exercise 5

You can add your codes into a `data_exploration.py` file.

- Upload the script to your GitHub repository for Exercise-5
- Remember to comment well your code!

## Problem 4 - Data analysis (5 points)

In this problem the aim is to understand how different the summer temperatures has been in Helsinki Kumpula and Rovaniemi.
Using the data from Problem 3 in `kumpula` and `rovaniemi` DataFrames answer to following questions:

**Part 1**

- What was the median temperature in:
  - Helsinki Kumpula?
  - Rovaniemi?

**Part 2**

Part 1 considers data from quite long period of time (May-Aug), hence the differences might not be so clear.
Let's find out what were the mean temperatures during June in Kumpula and Rovaniemi:

- Select from `rovaniemi` and `kumpula` DataFrames such rows from the DataFrames where ``YR--MODAHRMN`` values are from May 2017 (see hints for help)
and assign them into variables `rovaniemi_may` and `kumpula_may`
- Do similar procedure for June and assign those values into variables `rovaniemi_june` and `kumpula_june`
- Using those new subsets print the mean, min and max temperatures for both places in May and June.

You can add your codes into a `data_exploration.py` file.

- Upload the script to your GitHub repository for Exercise-5
- Remember to comment well your code!

Interpreting the results after the data analysis is one of the most important steps in a process called knowledge discovery.
Hence, use the information above to discuss shortly about following questions here (answer to this .md file)
(justify your answers with the data analysis results):

- Does there seem to be large difference in temperatures between the months?
- Is Rovaniemi much colder place than Kumpula?

## Problem 5 (optional) - Parse daily temperatures

This optional task is for more advanced students (minimal guidance given).
Our current dataset contains hourly temperatures.

Your task here is to:

  - create a new DataFrame where you have calculated mean, max and min temperatures for each day separately using the
  hourly values from Rovaniemi and Helsinki Kumpula.
  - this problem is a classical data aggregation problem

Find help from [Pandas Official documentation](https://pandas.pydata.org/pandas-docs/stable/) and using Google to find information
about solving this issue. If you think you can handle this but don't know how to proceed, ask in Slack for tips.


