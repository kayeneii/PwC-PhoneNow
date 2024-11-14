# PwC-PhoneNow
This data analysis was done for the PricewaterhouseCooper (PwC) Job Simulation program.

[Overview](#overview)
[Dataset](#dataset)
[Objectives](#objectives)
[Methods](#methods)
[Findings and Recommendations](#findings-and-recommendations)
[Visualizations](#visualizations)

## Call KPIs for PhoneNow 
### Overview
---
The goal of this analysis is to derive key performance indicators for a telecommunications company, PhoneNow, to understand the overall customer satisfaction level, resolved call rate, call agent performance and other relevant metrics.This analysis would help improve customer service and relations.


### Dataset
---
The dataset used in generating this report was obtained from the _PricewaterCooper House_ (PWC) Power BI Job Simulation Program. See [Forage](https://www.theforage.com/virtual-experience/a87GpgE6tiku7q3gu/pw-c-switzerland/power-bi-cqxg/introduction) for more.


### Objectives
---
To extract information on the following:
   * Overall customer satisfaction
   * Overall calls answered/abandoned
   * Calls by time
   * Average speed of answer
   * Agent’s performance quadrant -> average handle time (talk duration) vs calls answered


### Methods
---
The following tools were used in the creation of this report.
- **Microsoft Excel:** For data cleaning and preparation, initial exploration, and visualization.
  1. Data Cleaning and Preparation:
     - Data loading and inspection
     - Data cleaning
       
- **Microsoft Power BI:** For,
  1. Further Data Processing:
     - Data loading and quality inspection
     - Data sorting and transformation:
      ```DAX
       = Table.ReplaceValue(#"Sorted Rows","Y","Yes",Replacer.ReplaceText,{"Answered (Y/N)"})
     
       = Table.ReplaceValue(#"Replaced Value","N","No",Replacer.ReplaceText,{"Answered (Y/N)"})

       =  Table.ReplaceValue(#"Replaced Value1","Y","Yes",Replacer.ReplaceText,{"Resolved"})
     
       = Table.ReplaceValue(#"Replaced Value2","N","No",Replacer.ReplaceText,{"Resolved"})
     
       = Table.ReplaceValue(#"Changed Type",null,5,Replacer.ReplaceValue,{"Speed of answer in seconds"})

       = Table.ReplaceValue(#"Replaced Value",null,#datetime(1899, 12, 31, 0, 4, 44),Replacer.ReplaceValue,{"AvgTalkDuration"})

       = Table.ReplaceValue(#"Replaced Value1",null,1,Replacer.ReplaceValue,{"Satisfaction rating"})
      ```

  2. Data Analysis: Several Custom Columns and Measures were created in the Power Query during analysis of said data:
     
    **Custom Columns**
  
   Minutes
  ```DAX
  = Time.Minute([AvgTalkDuration])
  ```
   Seconds
  ```DAX
  = Time.Second([AvgTalkDuration])
  ```

  Talk Duration
  ```DAX
  = #duration(0, 0, [Minutes], [Seconds])
  ```

  MinSec
  ```DAX
  = [Minutes]*60
  ```

  Avg TalkTime
  ```DAX
  = [MinSec] + [Seconds]
  ```

  **Measures**

  ```DAX 
  No of Answered = CALCULATE(DISTINCTCOUNT('Call Center'[Call Id]), FILTER('Call Center', 'Call Center'[Answered (Y/N)] = "Y"))
  ```

  ```DAX 
  No of Resolved = CALCULATE(DISTINCTCOUNT('Call Center'[Call Id]), FILTER('Call Center', 'Call Center'[Resolved] = "Y"))
  ```

  ```DAX 
  Missed Call Rate = SUM('Call Center'[Percent Of Missed Calls]) / 100
  ```

  ```DAX 
  Target Value Satisfaction = 4
  ```

 3. Data Visualizations: Cards, Bar, Pie and Donut Charts was used to visually plot out the subscription service rates,  customer account and demographic information, among other summarized data.

- **GitHUb:** For,
  - Portfolio Building
  - Communication


### Findings and Recommendations
---
1. **Findings:** Following the conclusive analysis of the Churn Dataset, the following findings were made:
