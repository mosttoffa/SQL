## ✅ SQL Statement: 

<b>🔷 Definition:  </br>
    SQL Statement হলো এমন একটি নির্দেশনা (instruction) যা Database Management System-কে বলে দেয় — কী কাজ করতে হবে (যেমন ডেটা যোগ করা, পড়া, পরিবর্তন করা বা মুছে ফেলা)। </br>
	
🔷 Purpose / কেন SQL Statement দরকার:  </br>
    Database এর সাথে যোগাযোগ করতে SQL statements ব্যবহার হয়. ডেটা পরিচালনা (CRUD → Create, Read, Update, Delete) করতে সাহায্য করে.Database structure তৈরি, পরিবর্তন ও নিয়ন্ত্রণ করতে ব্যবহৃত হয়.Access control ও transaction management করতে ব্যবহৃত হয়.    </br>
🔷 SQL Statement এর প্রধান 4 টা ধরন (Category অনুযায়ী): </br>
	  1. DDL (Data Definition Language): CREATE,ALTER,DROP,TRUNCATE. DDL-Structure Level Statement. ডেটাবেসের structure / schema তৈরি, পরিবর্তন বা মুছে ফেলার জন্য ব্যবহার হয়। CREATE – নতুন table, database, view, index ইত্যাদি তৈরি করে. ALTER – কোনো table/view পরিবর্তন করে. DROP – কোনো object (table, view, index) মুছে ফেলে. TRUNCATE – টেবিলের সব ডেটা ডিলিট করে কিন্তু structure থাকে. </br>
	  2. DML (Data Manipulation Language): SELECT,INSERT,UPDATE,DELETE. MERGE- Insert/Update মিশিয়ে করা MERGE INTO Target USING Source .... DML-Data Level Statement. ডেটা insert, update, delete বা read করার জন্য ব্যবহার হয়।  SELECT – ডেটা পড়তে. INSERT – নতুন ডেটা যোগ করতে.  UPDATE – ডেটা পরিবর্তন করতে. DELETE – ডেটা মুছে ফেলতে.  </br>
	  3. DCL (Data Control Language): GRANT,REVOKE. DCL-Permission Statement. DENY- Access নিষিদ্ধ করা DENY DELETE ON Students TO UserB. ইউজারদের পারমিশন ও অ্যাক্সেস কন্ট্রোলের জন্য ব্যবহার হয়। GRANT – কোনো ইউজারকে পারমিশন দেওয়া. REVOKE – পারমিশন ফিরিয়ে নেওয়া. Example: GRANT SELECT, INSERT ON Students TO User1; </br>
	  4. TCL (Transaction Control Language): BEGIN TRANSACTION,COMMIT,ROLLBACK. SAVEPOINT- Transaction-এর মধ্যে checkpoint রাখা SAVE TRAN SavePoint1. TCL-Transaction Management Statement. Transaction ম্যানেজ করার জন্য ব্যবহার হয় — অর্থাৎ একসাথে একাধিক DML কাজ সেফলি করতে। BEGIN TRANSACTION- Start. COMMIT – পরিবর্তন স্থায়ী করে. ROLLBACK – পরিবর্তন বাতিল করে. </br>


🔷 Administrative Statements -  BACKUP DATABASE, RESTORE DATABASE. Purpose: Database maintenance. </br>
🔷 Utility Statements - USE, PRINT, EXEC. Purpose: Helper commands.  </br>
