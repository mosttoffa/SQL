##                         Practice Based on the Scenario

✅  <b>Find 2nd Highest Salary of an Employee. </b><br> 
💠 ROW_NUMBER() use করে বের করা যায়, অথবা DENSE_RANK() use করেও বের করা যায় <br> 
💠 কোনটার কি কাজঃ <br> <b>ROW_NUMBER()- </b> প্রতিটা Row এর জন্য Unique Number Create করে যদিও Sylary/Value একই হয়, কন্ডিশন মতো ১টা ভেলু ই দিবে।  <b>DENSE_RANK()-</b> প্রতিটা Same Salary/Value এর জন্য Same Number Create করে, কন্ডিশন মতো Salary/Value Same হইলে সব ভেলু ই দিবে। যদি একই Salary এর যতগুলো Employee আছে বের করতে হয় তখন DENSE_RANK() use করতে হয়। 
<pre>
-- Better Way: 
  
Select RowNumber, BasicSalary From (
Select BasicSalary,
DENSE_RANK() OVER(ORDER BY BasicSalary DESC) as RowNumber
FROM HR_EmployeeInfo
) x where x.RowNumber=2

  
-- ROW_NUMBER() ব্যাবহার করে -  
SELECT  *
FROM ( select ROW_NUMBER() OVER(ORDER BY Salary DESC) RowNumber, salary 
FROM Employee) Employeeee
WHERE RowNumber=2
---------------------------------------------------------------------------------
-- DENSE_RANK() ব্যাবহার করে - 
SELECT  *
FROM ( select DENSE_RANK() OVER(ORDER BY Salary DESC) RowNumber, salary 
FROM Employee) Employeeee
WHERE RowNumber=2

</pre>
