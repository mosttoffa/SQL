## INSERT 
✅ INSERT <br> SQL INSERT statement adds a new row to a table. INSERT can contain values for some or all of its columns. INSERT can be combined with a SELECT to insert records. <br>

🔷 <b>INSERT Syntax</b> 
<pre>INSERT INTO table-name (column-name)
		 VALUES (column-values)  </pre>
🔷 Example: Add Pakiza Knit to the list of Supplier 
<pre>INSERT INTO Supplier (CompanyName, ContactName, City, Country, Phone)
		VALUES ( 'Pakiza', 'Mr. Rajib', 'Dhaka, BD', 'Bangladesh', '880155555555' )    
	  --Check:
		SELECT CompanyName, ContactName, City, Country, Phone
		FROM Supplier 
		WHERE CompanyName = 'Pakiza'   </pre>	  
🔷 <b>INSERT with SELECT syntax</b> 
<pre>INSERT INTO table-name (column-names)
		SELECT column-names 
		FROM table-name
		WHERE condition    </pre> 
🔷 Example: Add new customer Craig Smith to the database 
<pre>INSERT INTO Customer(FirstName, LastName, City, Country, Phone)
		VALUES ('Craig','Smith','London','UK','880155555555')   
	  -- Check: 
		SELECT * FROM Customer WHERE FirstName='Craig' </pre>		 



