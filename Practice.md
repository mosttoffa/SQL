## SQL Practice Based on the Scenario

✅  Find 2nd Highest Salary of an Employee. 

<pre>
SELECT  *
FROM ( select ROW_NUMBER() OVER(ORDER BY Salary DESC) RowNumber, salary 
FROM Employee) Employeeee
WHERE RowNumber=2


</pre>
