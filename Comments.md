## ✅ Comments 

🔷 <br>Comments are used by developers to describe SQL statements or logic.Comments may appear anywhere in the code which is ignored by SQL Server.Single-line comments start with a double dash: --. Multi-line comments start with a /* and end with a */  
	<br> 🔷 Single-line syntax
	<br> 🔷 Multi-line syntax

<br> 
	🔷 Single-line syntax: <br> 
		<pre> // SQL description  </pre>
	🔷 Multi-line syntax: <br>  
<pre>    	/* SQL description
	       SQL description 
	       SQL description 
           SQL description */ </pre>

<pre>	/*   
		* List all customers from Sweden  
		*/   </pre>

<pre>	/************************************************ 
		 * List the monthly orders for American customers 
		 * for the year 2013. Order the list by month. 
		 ************************************************/  </pre>


<pre> sql /* * List all customers from Sweden */ SELECT * FROM Customers WHERE Country = 'Sweden';  </pre>
		 

