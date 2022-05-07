---
layout: post
title:  "JDBC and JPA: What are the Differences"
author: hori75
date:   2022-05-07 16:10:00 +0700
background: '/images/GitGuideorCheatsheetorWhatever-image.png'
excerpt_separator: <!--more-->
---

For starters, you could use JPA for storing data into database in springboot.
<!--more-->
After sometime learning, you may found JDBC as a library to connect to database.
And while trying it, you have to deal with SQL queries.
You wonder how some developer prefer JDBC over JPA or the other way.
This will tell you the differences between JDBC and JPA.

### What are those

Java Persistence API (JPA) is an API high level standard for Object Relational Mapping.
JPA already encapsulated SQL statements so you don't encounter with SQL.
But instead, you would encounter interfaces of the repository and must set decorators (such as `@Entity`, `@Id`, `@OneToOne`, etc).
From those interfaces you only could get the data in form of object.

Java Database Connectivity (JDBC) is a basic low level standard for interacting with database.
JDBC provides functions to execute SQL query and return it in form of SQL statement.
The SQL statement needs to be mapped into an object if you want to get data in form of object.
This explains why you have to deal with SQL query when working with JDBC.

### What are their differences

JPA is easy to use for starters and those who don't want to deal with SQL.
This also means the application is guaranteed to be compatible with any databases.
Why? Because there are some differences that could break one of databases or the other way.
Aside from that, JPA also speed up development because there is no need to plan a query.
Altough, adding decorators on the model could cause problems for other libraries.
Also, migration could cause problem and needs knowledge on how the migration work out in JPA.

JDBC is more simple when it comes to working with database. 
Dealing with SQL means you have control over which data do you want to get and in what form.
Migration could be handled seamlessly using Flyway.
But it requires an experience in dealing with SQL queries.
Also it needs to map sql result to the data object manually (you implement it yourself).
This means many things needed to be setup and might take a while to develop.

Using either of these still needs to deal with **object relational impedance mismatch**.
This is a fancy way to tell that object (OOP) models and relational models don't work together well.
Relational models represent itself in tabular format (data of tables) and OOP represent itself as 
interconnected graph of objects. The mismatch between 2 models could cause problems in either JPA or JDBC.
In my opinion, this could be dealt with by avoiding connecting relation directly and using primitive data on model object.
The main concept of Object relational Mapping itself is the solution to few mismatches.

### When to use JPA or JDBC

As stated in the beginning, JPA is good for starters who don't want to deal with SQL query.
JPA is also good for entreprise level application, altough it needs several adjustment to handle it's weaknesses.
JDBC is good for those who want to have control on what data is being queried and don't want to deal with migration problem.
JDBC in professional developers could create more lighter queries instead of utilizing Hibernate in JPA.
JPA is good for quick development, JDBC is more of an investment to be paid off in the long term.

### Conclusion

JPA and JDBC has its own strong points and weak points. 
Hopefully, this explained differences could help to choose between these two.
