
## SQL-Structured Query Language
✅ Database <br> Database হচ্ছে একটি container বা ধারক, যেখানে data রাখা হয় এবং data manage করা হয়। এটা হলো একটা বড় structure, যার মধ্যে অনেকগুলো object থাকে। SQL Server, MySQL, Oracle — প্রতিটিতে Database হলো data রাখার মূল জায়গা। <br>উদাহরণ: যদি একটা school management system তৈরি করো, তাহলে পুরো "SchoolDB" নামের একটা database থাকবে। এই database-এর ভিতরে থাকবে Table, View, Stored Procedure, Function ইত্যাদি। <br> <br>
✅ Database Object কী? <br> Database Object হলো — সেই সব structure বা element যেগুলো database-এর ভিতরে তৈরি করা হয় data সংরক্ষণ বা কাজ করার জন্য। <br> উদাহরণ Database Object: <br> Object Type (Table, View, Index, Stored Procedure, Function, Trigger, Constraint, Schema, Sequence / Synonym / Type), উদাহরণ- Students, Teachers. <br> কাজ:  ডেটা সংরক্ষণ করে.    <br><br>
✅ Database কি নিজেই Database Object? <br> না, Database নিজে object নয়, বরং Database হলো Object-এর Container (ধারক)। Database হচ্ছে একটা বড় Box. Database Object হচ্ছে সেই Box-এর ভিতরের item (Table, View, etc.)  <br><br>
✅ DataTable কী? <br> DataTable হলো memory-তে থাকা single table (rows + columns সহ)। <br> Excel/SQL table এর মতো but RAM-এ থাকে. <br> Data আসে সাধারণত database query থেকে. <br> 
Key parts: <br> 
```
  DataTable
    ├── Columns  (column list)
    └── Rows     (row list)
```
✅ DatabaseFactory কী? <br> DatabaseFactory হলো একটি ডিজাইন প্যাটার্ন (Factory Pattern) ব্যবহার করে ডেটাবেস সংযোগ (Connection) তৈরি করার ক্লাস। <br> 
সংজ্ঞা: এটি সাধারণত মাইক্রোসফটের এন্টারপ্রাইজ লাইব্রেরি ডেটা অ্যাক্সেস ব্লক (Data Access Block, DAB) এর অংশ। এটি কনফিগারেশন ফাইল থেকে ডেটাবেস কানেকশন স্ট্রিং পড়ে এবং সে অনুযায়ী সঠিক ডেটাবেস অবজেক্ট (যেমন SQL Server-এর জন্য SqlDatabase) তৈরি করে। <br>  ব্যবহার: এটি ডেটাবেস ব্যবহারের জন্য প্রয়োজনীয় অবজেক্টটি তৈরি করে, যাতে কোডে সরাসরি কানেকশন স্ট্রিং লেখা না লাগে। <br> 
কোডে উদাহরণ:
```
  Database db = DatabaseFactory.CreateDatabase();
```
✅ DbCommand কী? <br> DbCommand হলো ডেটাবেসে কার্যকর করার জন্য একটি SQL স্টেটমেন্ট বাStored Procedure-এর প্রতিনিধিত্ব। <br> সংজ্ঞা: এটি SQL কোড (যেমন SELECT, INSERT, UPDATE, DELETE) বা Stored Procedure-এর নাম ধারণ করে এবং ডেটাবেসকে নির্দেশ দেয় যে কী কাজ করতে হবে। <br> ব্যবহার: আপনার DAL কোডে, এটি আপনার তৈরি করা SQL স্ট্রিংটি ডেটাবেস এক্সিকিউশনের জন্য প্রস্তুত করে। <br> 
কোডে উদাহরণ:
```
  DbCommand dbCommand = db.GetSqlStringCommand(sql); // SQL স্ট্রিং কে কমান্ড অবজেক্টে পরিণত করা হচ্ছে
```
✅ DataSet কী? <br> DataSet হলো এক বা একাধিক DataTable-এর একটি সংগ্রহ। <br> সংজ্ঞা: এটি একটি সম্পূর্ণ ইন-মেমরি ডেটাবেস হিসেবে কাজ করতে পারে, যেখানে একাধিক টেবিল এবং তাদের সম্পর্ক (Relationship) সংরক্ষণ করা যায়। <br>
ব্যবহার: আপনার DAL (Data Access Layer) মেথডটিতে, db.ExecuteDataSet(dbCommand) ফাংশনটি ডেটাবেস থেকে একটি সম্পূর্ণ DataSet ফিরিয়ে আনে। যেহেতু আপনার মেথডটি শুধুমাত্র একটি টেবিল নিয়ে কাজ করে, তাই সেটি ds.Tables[0] (প্রথম টেবিল) রিটার্ন করে। <br> 
কোডে উদাহরণ:
```
  DataSet ds = db.ExecuteDataSet(dbCommand);
  return ds.Tables[0]; // DataSet থেকে প্রথম DataTable রিটার্ন করা হচ্ছে
```
✅ DataRow / DataTable.Rows[0] / DataRow row = table.Rows[i] কী? <br> DataRow হলো DataTable-এর মধ্যে থাকা একটি একক সারি (Row)। <br> সংজ্ঞা: এটি টেবিলের একটি নির্দিষ্ট রো-এর সমস্ত কলামের মান (Values) ধারণ করে। <br> 
ব্যবহার: আপনার কোডে, foreach লুপটি dtReq (DataTable)-এর প্রতিটি রো-এর উপর দিয়ে যায় এবং সেই একক রো-এর তথ্য dr (DataRow) ভ্যারিয়েবলে সংরক্ষণ করে। <br> 
কোডে উদাহরণ:
```
  foreach (DataRow dr in dtReq.Rows)
  {
   // dr["MCNo"] মানে বর্তমান রো-এর 'MCNo' কলামের মান
   TableData = TableData + "<td>" + dr["MCNo"] + "</td>";
  }
```
✅ TableData কী? <br> TableData SQL বা C# built-in কোনো type না। এটা সাধারণত developer-রা naming হিসেবে use করে। TableData হলো একটি কাস্টম (Custom) ভ্যারিয়েবল, যা আপনার কোডেই সংজ্ঞায়িত এবং ব্যবহৃত হয়েছে। <br> 
সংজ্ঞা: এটি একটি C# string ভ্যারিয়েবল, যা সম্পূর্ণ ডেটাবেস রিপোর্টটিকে HTML টেবিল স্ট্রাকচার (অর্থাৎ <table...> থেকে </table> পর্যন্ত) হিসাবে সংরক্ষণ করে। <br> ব্যবহার: এই HTML স্ট্রিংটি ফ্রন্ট-এন্ডে (যেমন ব্রাউজারে) JSON আকারে পাঠানো হয়, যাতে ইউজার এটি একটি সুন্দর টেবিল হিসেবে দেখতে পান। <br> 
কোডে উদাহরণ:
```
  string TableData = ""; // প্রথমে খালি স্ট্রিং হিসেবে শুরু
  // ... লুপের মধ্যে ডেটা যোগ হয় ...
  // ... সবশেষে JSON-এ পাঠানো হয় ...
  return Json(new { Tabdata = TableData }, JsonRequestBehavior.AllowGet);
```





