# Total Tests Performed Yesterday

I used the sum of "New Results Reported" because summing the result types are always new and the "total tests reported" appears to be a running balance each day.


```sql
SELECT Sum(NEW_Results_Reported) as 'Total Tests performed' 
  FROM Homework
  where Date = (select getdate() -1)
```
