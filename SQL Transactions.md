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
👉 এখন যদি মাঝখানে server crash হয় বা দ্বিতীয় query fail করে — তাহলে কী হবে? 
<p>
➡️ A-এর টাকা কমে যাবে
➡️ কিন্তু B পাবে না ❌
➡️ ডেটা inconsistent হয়ে যাবে!
এই সমস্যা রোধ করতেই আমরা Transaction ব্যবহার করি 💪
</p> 

