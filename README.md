# experience
## General Info
This program simulates an atm program.  It checks the pin code and gives you the option for withdrawal, deposits or see the statement.

This interface is linked to an SQL database.  It has two tables.  One is a customer table and the other is a transaction table.  The customer table has a primary key that links to each transaction made by each customer.

We can look at the statement.  This shows the related information is transaction order.  It also gives a running total and final balance.  
We can withdraw and/or look at other accounts.
It has an admin panel that can be used to do different queries.  
This program has three classes.  
It has an “action” class used to supply values for the selected tasks to perform.
It has a “main” class to provide the main interface and give numeric values and sound to the buttons.
It has a “result” class that is under construction.
It has a “state” statement class to show the account in the database.

It has a data1 class that 
1.)	Does the math for deposits and withdrawals.
2.)	 Connects to the data base.   
3.)	It stores the pin codes and the comparison method to control secure access.

It has a test class which is inactive now.
The upgrade path for this is:

See the video at my portfolio site:  http://alvinrainhill.com/EXP-X3.html

1.)	Upgrade the admin panel
2.)	Create other built-in queries to generate reports and totals for the admin panel.
3.)	Code a “Create New Account” for new customers.
4.)	Finish or delete the “results” and “test” classes.

