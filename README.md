# PwC-PhoneNow
This data analysis was done for the PricewaterhouseCooper (PwC) Job Simulation program.

[Overview](#overview)
[Data Source](#data-source)
[Objectives](#objectives)
[Methods](#methods)
[Findings](#findings)
[Visualizations](#visualizations)
[Conclusion](#conclusion)
## Call KPIs for PhoneNow 
### Overview
---
The purpose of this analysis was to derive key performance indicators for a telecommunications company called PhoneNow, that help them understand the overall customer satisfaction level, resolved call rate, call agent performance and other relevant metrics obtainable from the data provided. The goal is to help improve customer service and relations by
communicating my findings in a manner that can easily be understood by technical and non-technical staff.

### Data Source
---
The dataset used in generating this report is the Call-Center Dataset.xlsx procured from the _PricewaterhouseCooper_ (PWC) Power BI Job Simulation Program. See [Forage](https://www.theforage.com/virtual-experience/a87GpgE6tiku7q3gu/pw-c-switzerland/power-bi-cqxg/introduction) for more.


### Objectives
---
To extract information on the following:
   * Overall customer satisfaction
   * Overall calls answered/abandoned
   * Calls by time
   * Average speed of answer
   * Missed call rate
   * Agent’s performance quadrant -> average handle time (talk duration) vs calls answered


### Methods
---
The following tools were used in the creation of this report.
1. **Microsoft Excel:** For data cleaning and preparation.
       
2. **Microsoft Power BI:**
 * Further Data Processing: including data loading, quality inspection, sorting and transformation. This required the use of the following DAX functions:
   
      ```DAX
       = Table.ReplaceValue(#"Sorted Rows","Y","Yes",Replacer.ReplaceText,{"Answered (Y/N)"})
     
       = Table.ReplaceValue(#"Replaced Value","N","No",Replacer.ReplaceText,{"Answered (Y/N)"})

       =  Table.ReplaceValue(#"Replaced Value1","Y","Yes",Replacer.ReplaceText,{"Resolved"})
     
       = Table.ReplaceValue(#"Replaced Value2","N","No",Replacer.ReplaceText,{"Resolved"})
     
       = Table.ReplaceValue(#"Changed Type",null,5,Replacer.ReplaceValue,{"Speed of answer in seconds"})

       = Table.ReplaceValue(#"Replaced Value",null,#datetime(1899, 12, 31, 0, 4, 44),Replacer.ReplaceValue,{"AvgTalkDuration"})

       = Table.ReplaceValue(#"Replaced Value1",null,1,Replacer.ReplaceValue,{"Satisfaction rating"})
      ```

 * Data Analysis: Several Custom Columns and Measures were created in the Power Query during analysis of said data.
     
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


 * Data Visualizations: Guage, Matrix, Cards, Area and Bar Charts were used to visualize customer satisfaction, answered and resolved call rates, agent statistics, overall calls, call topics and other summarized data.

3. **GitHUb:** For portfolio building and communication.


### Findings
---
After a conclusive analysis of the Call Center Dataset, the following findings were made:
  * Average customer satisfaction was 2.76, falling short of the 4.0 target.
  * A total number of 5000 calls were made to the Call Center.
  * 18.92% of these calls were missed.
  * The total rate of answered calls was 81.08%.
  * The call agents failed to resolve 27.08% of the calls received.
  * Received calls were the highest on January 11.
  * The least number of calls received was on March 31.
  * The average speed of answer is 55.69 seconds.
  * Of the total calls received, 1,022 were regarding Streaming, making it the most popular topic.
  * Jim had the highest number of resolved calls and an average satisfaction rating of 3.4. 


### Visualizations
---
![image](https://github.com/kayeneii/PwC-PhoneNow/blob/main/PWC_PhoneNow%20Call%20KPIs.png)


### Conclusion
---
You made it to the end of the PhoneNow Call Center analysis.🥳
Until my next report, you may find me [here.](https://www.linkedin.com/in/kayeneii/) I look forward to hearing from you.😄
