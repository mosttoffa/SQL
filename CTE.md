## SQL WITH CTE (Common Table Expression) 

✅ CTE : <br> 
CTE মানে হলো Common Table Expression, যেটা SQL Server-এ একটা temporary named result set (অর্থাৎ একটি অস্থায়ী টেবিলের মতো ফলাফল)। <br> 
🔹 <b>CTE কী করে? </b> <br> 
CTE তোমাকে এমন একটা query block তৈরি করতে দেয় যেটা তুমি পরে SELECT, INSERT, UPDATE, DELETE, MERGE—এইসব স্টেটমেন্টে ব্যবহার করতে পারো। <br> 
📌 <b>এক কথায়: </b> CTE হলো Subquery-এর একটা cleaner এবং readable বিকল্প। <br> 
✅ <b>CTE ব্যবহারের উদ্দেশ্য: </b>  <br>
🔹 জটিল query-কে সহজ করা  <br>
🔹 Nested Subquery-এর পরিবর্তে readable কাঠামো দেওয়া  <br>
🔹 একই dataset একাধিকবার ব্যবহার করা যায়  <br>
🔹 Recursive query (যেমন tree structure, hierarchy) বানানো যায়  <br>
🧩 <b>CTE-এর Basic Syntax: </b> 
<pre>
WITH CteName (column1, column2, ..., columnN) AS (
    SELECT statement
)
SELECT column1, column2
FROM CteName
WHERE ...
🔸 ব্যাখ্যা:
CteName → CTE-এর নাম
(column1, column2, ...) → SELECT statement-এর কলামগুলোর নাম
SELECT statement → যে query-এর ফলাফলটা CTE হিসেবে save হবে
</pre>
🧮 Example 1: Basic CTE <br> 
👉 সমস্যা: List annual sales with the best years first. (বছরে মোট বিক্রির পরিমাণ দেখাও (বছরভিত্তিক, বেশি থেকে কম সাজানো)). 
<pre>
 WITH Cte (Year, Count, Amount) AS (
  SELECT YEAR(OrderDate) AS Year,
         COUNT(Id) AS Count,
         SUM(TotalAmount) AS Amount
    FROM [Order]
   GROUP BY YEAR(OrderDate)
)
SELECT Year, Amount 
  FROM Cte
 ORDER BY Amount DESC;
🔍 এখানে কী হলো:
প্রথমে WITH Cte এর ভেতরের SELECT চালানো হলো → বছরে বছরে sales summary
তারপর বাইরের SELECT দিয়ে ঐ temporary Cte থেকে data নিলাম
ORDER BY দিয়ে বেশি sales আগে দেখালাম
</pre>
🧩 Example 2: Monthly Min–Max Order Value <br> 
👉 সমস্যা: List the smallest and largest orders by month in 2013.  (২০১৩ সালের প্রতিমাসে সবচেয়ে ছোট ও বড় order বের করো)
<pre>
WITH Cte (Month, Min, Max) AS (
  SELECT MONTH(OrderDate) AS Month,
         MIN(TotalAmount) AS Min,
         MAX(TotalAmount) AS Max
    FROM [Order]
   WHERE YEAR(OrderDate) = 2013
   GROUP BY MONTH(OrderDate)
)
SELECT Month, Min AS MinOrder, Max AS MaxOrder
  FROM Cte
 ORDER BY Month; 
</pre>
🧩 Example 3: Multiple CTE (একাধিক CTE) <br> 
👉 সমস্যা:  List customers in the US and their order counts and order amounts for 2013.  (USA দেশের customer দের ২০১৩ সালের order count ও amount বের করো) 
<pre>
WITH CteOrder (CustomerId, OrderCount, OrderAmount) AS (
  SELECT CustomerId, COUNT(Id), SUM(TotalAmount)
    FROM [Order]
   WHERE YEAR(OrderDate) = 2013
   GROUP BY CustomerId
),
CteCustomer (Id, FirstName, LastName) AS (
  SELECT Id, FirstName, LastName
    FROM Customer
   WHERE Country = 'USA'
)
SELECT FirstName, LastName, OrderCount, OrderAmount
  FROM CteOrder O
  JOIN CteCustomer C ON O.CustomerId = C.Id
 ORDER BY LastName;
</pre>
🔍 <b>CTE কখন ব্যবহার করবে</b> <br> 
জটিল subquery আছে, Query readable করতে, একই dataset একাধিকবার দরকার, বারবার subquery না লিখে reuse করতে, Recursive data দরকার (যেমন parent-child), Hierarchical query তৈরি করতে, Aggregation বা summary table দরকার, Clean, modular report তৈরি করতে. 







