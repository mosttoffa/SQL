## SQL PIVOT

✅ <b>SQL PIVOT কী? </b> <br> 
PIVOT হলো SQL-এর একটি relational operator, যা row (সারি) গুলোকে column (কলাম) এ রূপান্তর করে।
এটি সাধারণত বড় ডেটা সেটকে সংক্ষেপে এবং পাঠযোগ্য রিপোর্ট আকারে দেখানোর জন্য ব্যবহার করা হয়।
অর্থাৎ — যেখানে আগে প্রতি বছরের অর্ডার আলাদা সারিতে দেখানো হচ্ছিল, সেখানে এখন প্রতিটি বছরকে আলাদা কলাম হিসেবে দেখানো যাবে। <br> 
🔷 <b>কেন PIVOT ব্যবহার করা হয়? </b> <br> 
 * ডেটা report বা summary আকারে উপস্থাপন করতে।
 * যখন row-to-column transformation দরকার হয়।
 * বিশ্লেষণ (analysis) বা visualization এর জন্য ডেটা readable format এ আনতে।
 * কোথায় ব্যবহার করা হয় ?: রিপোর্টিং, ডেটা এনালাইসিস, Dashboard তৈরিতে.
 * Aggregation - SUM, COUNT, AVG ইত্যাদি ফাংশন দিয়ে করা হয়. 

🧮 Example: (সহজভাবে বোঝানো) This example lists the total number of orders by year (ধরা যাক, আমরা প্রতি বছরের অর্ডারের সংখ্যা জানতে চাই।)  <br> 
🔹 Step 1: সাধারণ GROUP BY কুয়েরি <br> 
<pre>
SELECT YEAR(OrderDate) AS Year, COUNT(Id) AS Count
FROM [Order]
GROUP BY YEAR(OrderDate)
ORDER BY YEAR(OrderDate);
</pre>
🔹 Step 2: PIVOT ব্যবহার করে একই ডেটা “Column আকারে” 
<pre>
SELECT '# Orders' AS Year, [2012], [2013], [2014]
  FROM (
        SELECT Id, DATEPART(YEAR, OrderDate) AS Year 
          FROM [Order]
       ) AS t
  PIVOT (
        COUNT(Id) 
        FOR Year IN ([2012], [2013], [2014])
  ) AS PivotTable;
</pre>
 - এখানে দেখা যাচ্ছে, Year অনুযায়ী অর্ডার সংখ্যা এখন কলামে চলে এসেছে।

⚙️ <b>PIVOT এর Syntax </b> 
<pre>
  SELECT first_column AS alias,
       pivot_value1, pivot_value2, ... pivot_value_n
  FROM source_table AS table_alias
 PIVOT 
 (
   aggregate_function
   FOR pivot_column
    IN (pivot_value1, pivot_value2, ... pivot_value_n)
 ) AS pivot_table_alias;
🔸 Syntax ব্যাখ্যা:
অংশ                                	অর্থ
first_column	      পিভট টেবিলের প্রথম কলাম বা ক্যাটেগরি কলাম
pivot_values	      যেসব ভ্যালু কলামে রূপান্তরিত হবে
source_table	      আসল ডেটা টেবিল বা সাব-কুয়েরি
aggregate_function	ডেটা অ্যাগ্রিগেট করার ফাংশন যেমন SUM, COUNT, AVG ইত্যাদি
pivot_column	      যে কলামের ভ্যালু দিয়ে কলাম তৈরি হবে
pivot_table_alias	  পিভট টেবিলের নাম (অ্যালিয়াস)
</pre>
📘 আরও একটি Example : <br> 
Problem: প্রতি supplier কতগুলো product দিয়েছে তা তালিকাভুক্ত করা। <br> 
🔹 Step 1: সাধারণ GROUP BY query 
<pre>
  SELECT CompanyName, COUNT(P.Id) AS Count
  FROM Product P
  JOIN Supplier S ON P.SupplierId = S.Id
  GROUP BY CompanyName;
</pre>
🔹 Step 2: PIVOT ব্যবহার করে Supplier গুলোকে Column আকারে দেখা
<pre>
SELECT '# Products' AS 'Supplier', * 
  FROM (
        SELECT CompanyName
          FROM Product P
         INNER JOIN Supplier S ON P.SupplierId = S.Id
         GROUP BY P.Id, CompanyName
       ) t 
PIVOT (
  COUNT(CompanyName) 
  FOR CompanyName IN (
    [Aux joyeux ecclésiastiques], 
    [Bigfoot Breweries], 
    [Cooperativa de Quesos 'Las Cabras'], 
    [Escargots Nouveaux], 
    [Exotic Liquids], 
    [Forêts d'érables]
  )
) AS PivotTable;
</pre>








