# Kickstarting with Excel

## Overview of Project

### This analysis aims to help an up-and-coming playwright, Louise, who wants to learn more about crowdfunding campaign after starting one for her upcoming play, *Fever*. This analysis will take a closer look at kickstarter data with a focus on kickstarters supporting theater and the production of plays. This report will advise Louise on when she should launch her next kickstarter campaign, as well as what goal she should set for it. Analysis for her first kickstarter campaign is listed at the bottom of the page. 


## Analysis and Challenges

### Analysis of Outcomes Based on Launch Date
- In order to perform this analysis, I first created a pivot table from the kickstarter data. I set rows to show date created conversion (so it just shows months) and columns to show outcomes. I set filters for years and categories, and also wanted a count of the different outcomes, so added outcomes to the value box so the pivot table would show a count. Secondly, I filtered the columns to show only successful, failed, and canceled outcomes, and filtered the category to theater only. 

<img width="1331" alt="Outcomes based on launch analysis" src="https://user-images.githubusercontent.com/10901980/186524291-bde603c3-c1d8-48cb-99e5-353acbfc52bb.png">

- Once the pivot table was set, I used the table to create a line graph with markers. Once the graph was made, it was easy to make conclusions such as that kickstarters started in May had the highest success rate, and I could reference my table to get corresponding numbers.

![Theater_Outcomes_vs_Launch](https://user-images.githubusercontent.com/10901980/186524324-4ebfd685-771f-4fda-a5d2-8acb16a84932.png)


### Analysis of Outcomes Based on Goals
- To do analysis of outcomes based on goals, I first set up a table as specified in the directions. I didn't want to filter with kickstarter data for different outcomes, so instead used one COUNTIFS statement with multiple conditions. The first condition would check to see if the goal value in the kickstarter sheet was within a specific goal range, ex:

        COUNTIFS(Kickstarter!D$2:D$4115, ">=1000", Kickstarter!D$2:D$4115, "<5000"
        
    This would check within the kickstarter's goal column if the value was greater than or equal to 1000 and less than 5000 (aka is it a value between 1000 and 4999 since we're only working with whole numbers).
    
    The second conditional was to check the outcome of that goal, ex:
    
        Kickstarter!F$2:F$4115, "successful"
        
    This would check within the kickstarter's outcome column to see if the outcome matched "successful".
    
    The last conditional I used was to check the subcategory of that goal, ex:
    
        Kickstarter!R$2:R$4115, "plays"
        
    This would check within the kickstarter's subcategory column to see if the subcategory matched "plays".
    
    The finished COUNTIFS statement would look like this (shown in red on the screenshot):
    
    ```
    =COUNTIFS(Kickstarter!D$2:D$4115, ">=1000", Kickstarter!D$2:D$4115, "<5000", Kickstarter!F$2:F$4115, "successful", Kickstarter!R$2:R$4115, "plays")
    ```
    

    <img width="1331" alt="Outcomes based on goals analysis" src="https://user-images.githubusercontent.com/10901980/186524804-a80944e6-40bf-4f4c-8e63-ef0200bfce8e.png">

    Only if all three conditions are true would a count be added to the total amount of successful play kickstarters with a goal of 1000 to 4999. I repeated the same logic to fill out the columns for failed and canceled kickstarters as well, then summed the counts from all three outcomes to get the total count of kickstarter campaigns within that goal range. 
    
    ```
    =SUM(B3:D3)
    ```
    
    Lastly, to get percentages successful, failed, and canceled, I simply divided the individual successful/failed/canceled count by the total projects count respectively. Ex. for percentage successful kickstarters with a goal of 1000 to 4999:
    
    ```
    =B3/E3
    ```
    
    The final step was to create a line graph that showed percentage on the y-axis and goal ranges on the x-axis for all outcomes of successful, failed, and canceled play kickstarters. I selected all the data and created a line graph, then right clicked on the data to 'select data' and specify the conditions I wanted the line graph to display. 
    
  <img width="512" alt="Outcomes based on goal line graph setup" src="https://user-images.githubusercontent.com/10901980/186524945-34613002-b5f3-4c14-9754-0bb11b682788.png">

One the line graph was made, I could generally see that kickstarters with smaller monetary goals usually did better than those with large goals. Further conclusions could be made by referencing the table.

![Outcomes_vs_Goals](https://user-images.githubusercontent.com/10901980/186525074-d244ff6c-a6fa-472a-ad49-b978dd10e030.png)


### Challenges and Difficulties Encountered
- I didn't encounter any particular challenges in this analysis. Perhaps a challenge someone might face would be to successfully count the number of successful/failed/canceled kickstarters, as it requires multiple conditionals to be met. Simply filtering the main kickstarter data may lead to mistakes due to the multiple filters. Someone might also have had trouble with showing just the months a kickstarter was launched in as the date created has multiple aspects to it including the month, day, and year a kickstarter was created. Trying different combinations of conditionals is what I would have done if I encountered any of these issues!


## Results

- Looking at the theater outcomes by launch date analysis, it's clear that campaigns launched in May are the most successful, with 67% of them resulting in success. December is the least successful month with only 49% of theater kickstarters achieving their goal. However, it is encouraging that regardless of the month the kickstarter was launched in, theater kickstarters always have more successful than failed kickstarters. I would recommend Louise stick to the summer months when launching her next campaign. 

- When analysing the outcomes based on kickstarter fundraising goals, it's apparent that there is no clear-cut trend of whether or not a kickstarter is successful based on its goal. Kickstarters with goals less than 15,000 (unit of currency) are typically more successful than goals higher than 15,000 with success rates of over 50%. Goals that are less than 1,000 (unit of currency) achieved the highest rate of success at 76%, and goals that were over 45,000 (unit of currency) had the lowest success rates of 0-13%. I would recommend Louise to set a fundraising goal of $5000 or less for her next US kickstarter to maximize her chances of success.


### Data limitations
- The data from outcomes by goal and launch date would be more useful if it was filtered better. For example, outcomes based on goals looks at all countries, which in turn means the data set is filled with amounts of various global currencies. With the current exchange rate, 40,000 USD equates to ~58,000 AUD, but currently the way the data is presented 40,000 USD and 40,000 AUD are grouped together in the same 40,000-44,999 category. This could end up incorrectly skewing the data. Additionally, not all of the data categories are explained as to what they are such as staff_pick or spotlight, so it was not possible to use them to further analyze the data. Lastly, this data wasn't cleaned up at all; for examples, outliers still exist in the original dataset we were doing our analysis on. This can once again skew the data and lead to incorrect conclusions. 


### What other analysis could be done to help Louise?
- I think it would be interesting to also look at kickstarter duration (how long did the kickstarter fundraise for) so Louise can be more informed on what month she should end her kickstarter on too. This could be done via another line graph displaying what end month was most successful, as well as simply adding an additional column to the kickstarter data that calculates campaign duration. Additionally, it would be interesting to see what the average donation and average backer count was for successful campaigns to help Louise know how she should plan her outreach strategies. 


___________________________________________________________________________________________________________________________________________________________


Previous Read.me for 1.6.1; Recommendations for Louise


# An Analysis of Kickstarter Campaigns
Module 1 Kickstarter

This analysis aims to help an up-and-coming playwright, Louise, who wants to start a crowdfunding campaign to help fund her play, *Fever*. She's estimating a budget of over $10,000 and is understandably hesitant about jumping into her first fundraising campaign. Louise also mentioned that she's also interested in Great Britain's theater market, especially musicals. While she's committed to creating a play in the U.S., she's also interested in researching musicals in Great Britain for a future project with an estimated budget of £4,000. This analysis uses Excel to organize, sort, and analyze crowdfunding data to determine whether there are specific factors that make a project's campaign successful. Project viability, campaign start date, and campaign goal will all be discussed in this analysis.

### Analysis:
Given the Kickstarter data, which gives a wide variety of information of kickstarters between 2009-2017, Louise is positioned well to start a kickstarter for her play. The number of theater kickstarters far exceeded the amount of other kickstarter categories and a majority of them (57.5%) successfully raised the funds to get their project off the ground. 
![Parent_Category_Analysis](https://user-images.githubusercontent.com/10901980/186225124-56de68ba-96b5-4678-9f08-92904d715d04.png)

Taking an even deeper look within the space of theater kickstarters, many kickstarters for plays were successful within the US (61.4%), so I would advise Louise to be less nervous about raising the necessary funds.  
![US_Theater_Kickstarter_Analysis](https://user-images.githubusercontent.com/10901980/186225764-1aa90ce9-2c72-4e5e-90c8-608283a492e4.png)

So far we've established that Louise has a good chance of completing a successful kickstarter; the next important aspect is to inform Louise when would be an ideal time to start her fundraising campaign. Looking at theater kickstarters launched in the US by month, May was the most successful month with 67.7% of kickstarters launched that month resulting in a met goal. Most successful kickstarters had a fundraising period of about a month, so I would advice Louise to start her campaign in May and end her campaign in June! 
![US_Theater_Date_Created_Outcomes](https://user-images.githubusercontent.com/10901980/186230004-e1f23416-00c7-49c2-b257-e1dba5ca0b3c.png)

In regards to her budget, I would recommend Louise stick to a budget of around $3000. In the US, the average goal for a successful theater play kickstarter was $2500 (excluding outliers; an outlier was considered a goal amount of Q3+1.5IQR). The average amount pledged for these successful kickstarters was $2930. 75% of successful kickstarters had a goal amount of <=$4500, so setting a goal of around $3000 gives Louise a great chance of achieving fundraising success. 
![GoalvPledged_US_Successful_Kickstarters](https://user-images.githubusercontent.com/10901980/186241533-4d2ce1e2-6ba7-4208-be23-28f574fdafaf.png)

Lastly, Louise was also curious about musical kickstarters in Great Britain. Once again, Louise has picked a target fundraising goal that is too high. According to successful musical kickstarters in GB, the average goal was £1250 and the average amount raised was £1328. 75% of GB musical kickstarters had a fundraising goal of <=£2000. As it seems like most musical kickstarters almost exactly meet their goals when successful, I would recommend Louise to set a kickstarter goal of ~£1250 so she has the best possible chance of meeting her goal. 
![GoalvPledged_GB_Musical_Kickstarter_Statistics png](https://user-images.githubusercontent.com/10901980/186243882-69104c2d-3424-4f0f-9674-8e65c61a06ee.png)


### Conclusion
In conclusion, I recommend Louise to set a fundraising goal of $3000 and have her campaign run from May to June if she wants to set up a kickstarter for her upcoming play *Fever*. If one day she wishes to expand into the musical field in Great Britain, she should lower that goal to £1250.
