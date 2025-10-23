## SQL Practice Based on the Scenario

✅  Find 2nd Highest Salary of an Employee. 
💠 ROW_NUMBER() use করে বের করা যায়, অথবা DENSE_RANK() use করেও বের করা যায়
💠 কোনটার কি কাজঃ ROW_NUMBER()- প্রতিটা Row এর জন্য Unique Number Create করে যদিও Sylary/Value একই হয়, কন্ডিশন মতো ১টা ভেলু ই দিবে।  DENSE_RANK()- প্রতিটা Same Salary/Value এর জন্য Same Number Create করে, কন্ডিশন মতো Salary/Value Same হইলে সব ভেলু ই দিবে। যদি একই Salary এর যতগুলো Employee আছে বের করতে হয় তখন DENSE_RANK() use করতে হয়। 
- <pre>
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
