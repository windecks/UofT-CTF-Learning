# Week 3

## Introduction to SQLi
This week, we'll focus on SQL and SQL injection for web exploitation. SQL or "Structured Query Language" is the most common language used in relational databases. Databases can hold anything from user accounts and passwords to bank information. Here's the SQL hierarchy from highest to lowest:

* For every **Database**,
* There are 1+ **Tables**,
* which contain **Rows (Records)/Columns (Fields)**

To retrieve data from an SQL database, we can use what's called an "SQL Query". This is where the SQL language comes in - we use the language to select and choose what data we want to see!

So how can an attacker exploit a poorly protected SQL databse? This is where SQL injection comes in. Let's take an account login for example. Given the parameters `name` and `password`, with values `123` and `123pass` the web application forms an SQL query: `SELECT * FROM users WHERE name='123' AND password='123pass'`. Now, the system will look for (SELECT) all rows from the "users" where the name is "123" and the password is "123pass". If there is a row with these values, then great! We will log in. If not, then a login does not occur.

With SQL injection however, we may not need to know the password. SQL injection takes advantage of vulnerabilities where a web application may not "sanitize" the inputs provided, allowing an attacker to execute SQL queries in input fields that are normally intended for something else. Going back to the example, what if I do this:

```
Username is: 123
Password is: idkthepassword' OR 1=1--
```
This is what the SQL query will look like:
```
SELECT * FROM users WHERE name='123' AND password='idkthepassword' OR 1=1--'
```
Let's break it down. The SQL query is looking for a row with the username "123" (this is the account we want to break into) AND a password "idkthepassword". Obviously we don't know the password, but it will also select rows where the username is "123" AND 1=1! This is due to our injection of the OR operator. That is, it will select rows where the password is "idkthepassword" OR 1=1 (this is always true :3).

Now why did we include a quotation mark and double hyphen? This is where the real trickery comes in. The web application closes the password input with a quotation mark normally: If the password is 123, then the SQL query will be '123'. 

But what if we add one of our own quotation marks? Well then we'll have an extra quotation mark at the end and it'll make no sense: '123''. But if we comment out the quotation mark that the system adds automatically using the double hyphen, then we can end the input early and add anything we want after. Here's what it looks like:

If we input the password `123' [bad code here]--`, then the system will convert it into `'123' [bad code here that will be run]--'`! Notice that the quotation mark at the end is ignored as it becomes a comment due to the double hyphen.

This is the essence of SQL injection. How can we manipulate inputs that we're provided to run SQL queries in places where it isn't intended? This allows us to bypass authentications and log into accounts that we don't know the credentials of among other things. 

## Exercises

There are tons of SQL injection challenges available on the internet. picoCTF offers quite a few ones in varying difficulty, so try them out!
