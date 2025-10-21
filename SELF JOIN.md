## SELF JOIN 
✅ <b>Self JOIN </b> <br> A table is joined with itself. This can be useful when modeling hierarchies.Another usage is to find duplicates within a table. <br> 
🔷 <b>Self JOIN Syntax: </b> 
<pre>SELECT column-names 
		FROM table-name T1 
		JOIN table-name T2 
		WHERE condition   </pre>		 
👉 Example: Match suppliers that are from the same country
<pre>SELECT A.CompanyName AS Company1, B.CompanyName AS Company2, A.Country 
		FROM Supplier A 
		JOIN Supplier B ON A.Id <> B.Id
		AND A.Country = B.Country
		ORDER BY A.Country    </pre>		 
👉 Example: Match customers that are from the same city and country
<pre>SELECT (B.FirstName+' '+B.LastName) Name1, (A.FirstName+' '+A.LastName)Name2, B.City, B.Country
		FROM Customer A 
		JOIN Customer B ON A.Id <> B.Id
		AND A.City = B.City
		AND A.Country = B.Country
		ORDER BY A.Country    </pre>		
👉 Example:finding DUPLICATES-  Find customers with the same first name (i.e. duplicates)
<pre>SELECT CONCAT(C1.FirstName,' ',C1.LastName)Name, CONCAT(C2.FirstName,' ',C2.LastName) Duplicate
		FROM Customer C1
		JOIN Customer C2 ON C1.Id <> C2.Id
		WHERE C1.FirstName = C2.FirstName
		ORDER BY C1.FirstName    </pre>		 


