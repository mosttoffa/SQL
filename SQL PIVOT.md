## SQL PIVOT

✅ <b>SQL PIVOT কী? </b> <br> 
PIVOT হলো SQL-এর একটি relational operator, যা row (সারি) গুলোকে column (কলাম) এ রূপান্তর করে।
এটি সাধারণত বড় ডেটা সেটকে সংক্ষেপে এবং পাঠযোগ্য রিপোর্ট আকারে দেখানোর জন্য ব্যবহার করা হয়।
অর্থাৎ — যেখানে আগে প্রতি বছরের অর্ডার আলাদা সারিতে দেখানো হচ্ছিল, সেখানে এখন প্রতিটি বছরকে আলাদা কলাম হিসেবে দেখানো যাবে। <br> 
🔷 <b>কেন PIVOT ব্যবহার করা হয়? </b> <br> 
 * ডেটা report বা summary আকারে উপস্থাপন করতে।
 * যখন row-to-column transformation দরকার হয়।
 * বিশ্লেষণ (analysis) বা visualization এর জন্য ডেটা readable format এ আনতে।

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
-- এখানে দেখা যাচ্ছে, Year অনুযায়ী অর্ডার সংখ্যা এখন কলামে চলে এসেছে।  
⚙️ <b>PIVOT এর Syntax </b> 


