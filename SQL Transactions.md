## SQL Transactions 

✅ <b>SQL Transactions  কী? </b> <br> 

<p>Transaction হলো একাধিক SQL operation-এর একটি সেট, যেগুলো সবগুলো একসাথে সফল (commit) হবে বা একসাথে ব্যর্থ (rollback) হবে। একে বলে — "All or Nothing" ইভেন্ট। “সব কাজ হবে একসাথে, না হলে কিছুই হবে না।”
অর্থাৎ, কোনো কিছু সফল আর কোনো কিছু ব্যর্থ — এমনটি হতে পারবে না। Transaction শুরু হয় BEGIN TRAN দিয়ে এবং শেষ হয় COMMIT TRAN দিয়ে। </p>

🎯 <b>উদ্দেশ্য (Why Transactions are used): </b> <br> 
<p>Transactions ব্যবহারের মূল উদ্দেশ্য হচ্ছে ডেটার সঠিকতা (data integrity) এবং consistency রক্ষা করা।</p> <br> 
🔸 উদাহরণ: 
ধরো, তুমি একটি Bank Transfer System বানাচ্ছো — <br> 
💰 A → B তে টাকা ট্রান্সফার হচ্ছে. এর জন্য দুইটা query চলবে: <br> 
1️⃣ A-এর account থেকে টাকা কমানো <br> 
2️⃣ B-এর account-এ টাকা যোগ করা <br> 
<pre>
UPDATE Accounts SET Balance = Balance - 500 WHERE AccountNo = 'A';
UPDATE Accounts SET Balance = Balance + 500 WHERE AccountNo = 'B';
</pre>
👉 এখন যদি মাঝখানে server crash হয় বা দ্বিতীয় query fail করে — তাহলে কী হবে? <br>
➡️ A-এর টাকা কমে যাবে <br>
➡️ কিন্তু B পাবে না ❌ <br>
➡️ ডেটা inconsistent হয়ে যাবে! <br>
💪 এই সমস্যা রোধ করতেই আমরা Transaction ব্যবহার করি <br> <br> 
🧠 <b>SQL Transaction কীভাবে কাজ করে: </b>  <br> 
Transaction সাধারণত তিনটি ধাপে চলে 👇 <br> 
<b>BEGIN TRANSACTION → Transaction শুরু </b> <br> 
<b>COMMIT TRANSACTION → সব কিছু সফল হলে save করা </b> <br> 
<b>ROLLBACK TRANSACTION → কোনো সমস্যা হলে সব কিছু বাতিল করা </b>   <br> 

🧾 <b>Example (Bank Transfer): </b> 
<pre>
BEGIN TRANSACTION;

UPDATE Accounts 
SET Balance = Balance - 500 
WHERE AccountNo = 'A';

UPDATE Accounts 
SET Balance = Balance + 500 
WHERE AccountNo = 'B';

-- সবকিছু ঠিকভাবে হলে save করো
COMMIT TRANSACTION;

-- কোনো error হলে
ROLLBACK TRANSACTION;

✅ যদি দুইটা query ঠিকভাবে execute হয় → COMMIT TRANSACTION
❌ যদি কোনো একটা fail করে → ROLLBACK TRANSACTION
</pre>

🔐 <b>Transaction এর ৪টি গুণ (ACID Properties): </b> <br> 
<pre>
Property	     |           ব্যাখ্যা
--------------------------------------------------------------------------
A - Atomicity	 |       পুরো transaction একক ইউনিট – সব হবে বা কিছুই হবে না
C - Consistency	 |       Transaction শেষে ডেটা valid অবস্থায় থাকতে হবে
I - Isolation	 |       একাধিক transaction একসাথে চললেও একে অপরকে প্রভাবিত করবে না
D - Durability	 |       Commit হয়ে গেলে server crash হলেও ডেটা থাকবে
</pre> 
🧩 <b>Practical Example (with Error Handling): </b> <br> 
<pre>
BEGIN TRY
    BEGIN TRANSACTION;

    UPDATE Orders SET Status = 'Shipped' WHERE OrderId = 1001;
    UPDATE Inventory SET Stock = Stock - 1 WHERE ProductId = 501;

    COMMIT TRANSACTION; -- সবকিছু ঠিক আছে ✅
END TRY
BEGIN CATCH
    ROLLBACK TRANSACTION; -- কোনো error হলে সব বাতিল ❌
    PRINT 'Error occurred, transaction rolled back';
END CATCH;

</pre>

<br>
🎯 উদাহরণ: <br> 
👉 সমস্যা: একটি নতুন order তৈরি করতে হবে — এবং নিশ্চিত করতে হবে যেন Order এবং তার OrderItems দুটোই সেভ হয় বা কিছুই না হয়। <br> 
<pre>
BEGIN TRAN;

INSERT INTO [Order] (OrderNumber, CustomerId, TotalAmount)
VALUES (543210, 23, 183.35);

DECLARE @OrderId INT;
SET @OrderId = SCOPE_IDENTITY();

INSERT INTO OrderItem(OrderId, ProductId, UnitPrice, Quantity)
VALUES (@OrderId, 5, 21.35, 1);

INSERT INTO OrderItem(OrderId, ProductId, UnitPrice, Quantity)
VALUES (@OrderId, 20, 81.00, 2);

COMMIT TRAN;

-- Result:
    3টি রেকর্ড insert হয়েছে।
🧠 কাজের প্রক্রিয়া:
    BEGIN TRAN → Transaction শুরু করে
    COMMIT TRAN → সব কাজ সফল হলে, চূড়ান্তভাবে ডেটা সেভ করে
    যদি কোনো INSERT ব্যর্থ হয়, তাহলে সবগুলো rollback (বাতিল) হয়ে যায়
    অর্থাৎ — আংশিক ডেটা সেভ হওয়ার কোনো সুযোগ নেই ✅
</pre>
⚙️ <b>Transactional Commands : </b> 
<pre>
Statement	     |   Description (বাংলায় ব্যাখ্যা)
------------------------------------------------------------------------------------------------------------------------------------
BEGIN TRAN	     |       Transaction শুরু করে
COMMIT TRAN	     |       Transaction সফলভাবে শেষ করে; সব ডেটা ডিস্কে সেভ করে
ROLLBACK TRAN	 |       Transaction-এর শুরু থেকে সব পরিবর্তন বাতিল করে
SAVE TRAN	     |       Transaction-এর মধ্যে এক বা একাধিক "save point" তৈরি করে, যেখানে কোনো সমস্যা হলে ওই পয়েন্ট পর্যন্ত ফিরে যাওয়া যায়
</pre> 

⚠️ <b>নোট: </b> <br>
Transactional command শুধুমাত্র নিচের statement-এর সাথে কাজ করে: <br> 
👉 INSERT, UPDATE, DELETE এগুলো DDL (যেমন CREATE TABLE, DROP TABLE) এর সাথে কাজ করে না। <br>  <br>


🔁 <b>Autocommit Mode কী? </b> <br> 
যদি তুমি BEGIN TRAN ব্যবহার না করো — তাহলে SQL Server প্রতিটি INSERT, UPDATE, DELETE statement-এর পর স্বয়ংক্রিয়ভাবে COMMIT করে দেয়।
এটাকে বলে 👉 Autocommit Mode।
তবে অনেক ক্ষেত্রে explicit transaction (ম্যানুয়ালি শুরু করা) দরকার হয় —
যেমনঃ <br> 
💳 ব্যাংকের ডেবিট/ক্রেডিট ট্রান্সফার <br> 
🛒 ই-কমার্সের অর্ডার বা পেমেন্ট সেভ <br> 
না হলে partial transaction হয়ে যেতে পারে, যার ফলে অসম্পূর্ণ অর্ডার বা অর্থনৈতিক ক্ষতি হতে পারে। <br> 
🧩 আরও একটি Example: <br> 
সমস্যা:
একটি নতুন supplier এবং তার products গুলো একসাথে ডাটাবেজে যোগ করতে হবে। <br> 
<pre>
BEGIN TRAN;

INSERT INTO [Supplier] (CompanyName, ContactName, City, Country, Phone)
VALUES ('Amsterdam Broodjeshuis', 'Jan van de Berge',
        'Amsterdam', 'Netherlands','(31) 1 2612 7769');

DECLARE @SupplierId INT;
SET @SupplierId = SCOPE_IDENTITY();

INSERT INTO Product(SupplierId, ProductName, UnitPrice, Package)
VALUES (@SupplierId, 'Krentebollen', 4.35, '6 in a bag');

INSERT INTO Product(SupplierId, ProductName, UnitPrice, Package)
VALUES (@SupplierId, 'Volkoren brood', 6.35, '1 loaf');

INSERT INTO Product(SupplierId, ProductName, UnitPrice, Package)
VALUES (@SupplierId, 'Roggebrood', 2.99, '20 slices per pkgs');

COMMIT TRAN;
    
👉 এখানে সবগুলো INSERT সফল হলে তবেই ডেটা সেভ হবে,
না হলে একটিও হবে না।
Result: ৪টি রেকর্ড insert হয়েছে ✅
</pre>

⚙️ <b>Where Transactions are used (Common Use Cases): </b> <br> 
<pre>
Use Case	              |          Description
-----------------------------------------------------------------------------
💳 Bank Transfer	            টাকা ট্রান্সফার — দুই দিকেই balance update
🛒 E-Commerce Checkout	        Order তৈরি, Payment deduct, Stock update
🏦 Payroll Processing	        একাধিক table update (Employee, Salary, Log)
📦 Inventory Update	            Stock increase/decrease operations
</pre>




