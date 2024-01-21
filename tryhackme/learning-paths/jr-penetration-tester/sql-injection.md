---
description: Tenth section in Jr Penetration Tester learning path.
---

# SQL Injection

### Introduction

SQL (Structured Query Language) Injection (or SQLi) is an attack on a web app database that executes malicious queries. This occurs when a web app communicates with a database without sanitising or validating user input which is received.

A databse is storage of collections of data. A database is controlled by a DBMS (Database Managemnt System). There are two kinds of DBMS: Relational and Non-Relational. A relational database stores info in tables which often have info shared between them. The table contain a column with a unique ID (primary key) which can be used in other tables to reference it. Non-relational databases are any database which does not use tables, columns and rows to store data.

In a DBMS, there can be multiple databases containing their own related datasets. Information in databases is stored separately using tables, which each have unique identifiers.&#x20;

A table is made up of columns and rows. Each column (or field) has a unique name. Each column also has a type set for the data it will contain (e.g. integer, string, date). Each row (or record) contains the individual lines of data, when data is added to the table a new record is created, and when data is deleted a record is removed.

### Simple SQL Commands

* SELECT : `select * from users;`
* UNION : `select name,city,postcode from customers UNION SELECT company,city,postcode from suppliers;`
* INSERT : `insert into users (username,password) values ('bob','password');`
* UPDATE : `update users SET username='root',password='pass' where username='admin';`
* DELETE : `delete from users where username 'martin';`

### In-Band SQLi

Easiest type to detect and exploit. For example, an SQLi vulnerability on a website page which leads to extraction of data to the same page. In SQL injection, `;--` will end a query and comment out any additional code after it, for example, `' OR 1=1;--` will return true and end the query.

### Blind SQLi - Auth Bypass

Blind SQLi is where we get little to no feedback to confirm if our queries were successful. One of the most straightforward techniques is bypassing a login form. Login forms that are connected to a database of users are often developed so that the web app isn't interested in the content of the username and password but whether the two make a matching pair.&#x20;

### Blind SQLi - Boolean Based

This refers to the response received to an injection, which could be true/false, yes/no, on/off or any response with two outcomes.&#x20;

### Blind SQLi - Time Based

Tim ebased SQLi is similar to boolean based, but there is no visual indicator of right/wrong. Instead, our indication of success is howw long the query takes to complete, the delay can be invoked with methods like `SLEEP(x)` alongside `UNION`. The `SLEEP()` method will only ever be executed after a successful `UNION SELECT`.

