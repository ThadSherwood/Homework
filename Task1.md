# Total Tests Performed Yesterday


Total number of tests performed as of yesterday
I used the sum of "New Results Reported" because summing the result types are always new and the "total tests reported" appears to be a running balance each day.


```sql
SELECT Sum(NEW_Results_Reported) as 'Total Tests performed' 
  FROM Homework
  where Date <= @Date -- added this line for dynamic date in SQL reporting
```