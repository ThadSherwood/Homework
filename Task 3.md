# Task 3
The 10 states with the highest test positivity rate (positive tests / tests performed) for tests performed in the last 30 days.

This is the version that is written specifically for 30 days from the last reported data.

```SQL
WITH tempTable1 AS (SELECT state_name,COALESCE(SUM(new_results_reported),0) as PosTest from homework where overall_outcome = 'positive'and date >= '2024-05-02' group by state_name),
 tempTable2 AS (SELECT state_name, COALESCE(SUM(new_results_reported),0) as TotalTest from homework where date >= '2024-05-02' Group by state_name)
Select Top 10 a.state_name, (a.PosTest * 1.0 / nullif(b.TotalTest,0)*100) as ResultPercent
	from tempTable1 a
	inner join tempTable2 b on a.state_name = b.state_name
group by a.state_name, a.PosTest, b.TotalTest
order by ResultPercent desc
```

This would be the version that is written for a dynamic date

```SQL
WITH #tempTable1 AS (SELECT state_name,COALESCE(SUM(new_results_reported),0) as PosTest from homework where overall_outcome = 'positive'and and Date >= (select getdate() - 30) group by state_name),
 #tempTable2 AS (SELECT state_name, COALESCE(SUM(new_results_reported),0) as TotalTest from homework where Date >= (select getdate() - 30) Group by state_name)
Select Top 10 a.state_name,a.PosTest,b.TotalTest, (a.PosTest * 1.0/nullif(b.TotalTest,0)*100) as ResultPercent
	from #tempTable1 a
	inner join #tempTable2 b on a.state_name = b.state_name
group by a.state_name, a.PosTest, b.TotalTest
order by ResultPercent desc
```