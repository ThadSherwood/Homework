# The 7-day rolling average number of new cases per day for the last 30 days.

This query would be for a dynamic date.

'''sql
WITH tempTable AS (SELECT DATENAME(WEEKDAY, Date) AS weekDay, Date, new_results_reported from Homework)
Select weekDay, SUM(new_results_reported) / 7  as DailyAvg from tempTable
where Date >= (select getdate() - 30)
group by weekDay
'''  
  
Since the newest data in the data set is older than 30 days, the result would be NULL.
In this case I am running the query from the necessary date forward as written below.

'''sql
WITH tempTable AS (SELECT DATENAME(WEEKDAY, Date) AS weekDay, Date, new_results_reported from Homework)
Select weekDay, SUM(new_results_reported) / 7  as DailyAvg from tempTable
where Date >= '2024-05-02'
group by weekDay
'''
Results show that either less people are getting tested on the weekend.  Possibly trying to wait out the weekend in the hopes that they just have a cold and hoping that the symptoms will subside by monday.
