# Week 4

This week, we'll be going over a more advanced SQL injection technique that is used more commonly in real-world situations. This week's content assumes knowledge of basic SQL techniques, mainly covered in Week 3.

## Blind SQL - An Introduction

Basic SQL injection usually relies on detailed error messages that provide the attacker enough information to create a working payload. The issue is that these errors are usually not shown to the user in web applications. Blind SQL forgoes the need for detailed error messages by asking a series of True/False questions. This specific technique is called boolean-based blind SQL injection. Ever played 20 questions? Blind SQL works similarly by getting information through queries that either may or may not produce a generic "Error".

How can we test for SQL vulnerabilities? Here's an example:

Here's a vulnerable site: 
```
http://www.shop.test/item.php?id=5
```
The URL displays the item with `id` 5 through an SQL query. The SQL query could look like this (we don't actually know!):
```
SELECT * FROM items where ID = 5
```
We can then add something to see how the webapp responds if an SQL query is false:
```
http://www.shop.test/item.php?id=5 and 1=2
This produces the SQL query:
SELECT * FROM items where ID = 5 and 1=2
```
Obviously, 1=2 is false! Perhaps we are taken to an error page. We now know what to expect when an SQL query is false. We can do the same thing with a true statement using `...item.php?id=5 and 1=1` and see the response. Now, we can craft our attack!
```
5 and (
    SELECT TOP 1 substring(name, 1, 1) FROM sysobjects --Selects the first row, extracting from the string object "name" - the first position with length 1
    WHERE id=(
        SELECT TOP 1 id FROM (
            SELECT TOP 1 id FROM sysobjects ORDER BY id)
        AS subq ORDER BY id DESC)
    ) = 'a'
```
`sysobjects` is a special table containing data about the tables in a database. There's a lot going on here, but basically we are checking if the character 'a' is the first character of the name of the first table. Our URL would look like this:
```
https://www.shop.test/item.php?id=5 and (select top 1 substring(name, 1, 1) from sysobjects where id=(select top 1 id from (select top 1 id from sysobjects order by id) as subq order by id desc))='a'
```
If we don't get the response we did for a statement that was false, then we know that the first character is a! If we do get a false response, then we can iterate through the alphabet until reaching the correct letter. After getting the correct letter, we can change the substring function arguments to `(name, 2, 1)` to look for the second character. This can continue until reaching the entire length of the word.

This is the basic idea to boolean-based blind SQL injection. We can use the same idea to determine a lot more information about an SQL database!

## Exercise

I couldn't find any boolean-based blind SQLi challenges that were hosted on an instance online... perhaps read a writeup of [this picoCTF challenge from 2018.](https://ctftime.org/task/6790)

