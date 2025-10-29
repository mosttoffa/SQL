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
💪 এই সমস্যা রোধ করতেই আমরা Transaction ব্যবহার করি <br> 
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
👉 INSERT, UPDATE, DELETE এগুলো DDL (যেমন CREATE TABLE, DROP TABLE) এর সাথে কাজ করে না। <br> 




