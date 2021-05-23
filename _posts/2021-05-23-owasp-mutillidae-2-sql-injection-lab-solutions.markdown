---
layout: post
title:  "OWASP Mutillidae 2 SQL Injection Lab Solutions"
date:   2021-05-23 18:00:00 +0300
tags: Security Practice Lab XSS Vulnerability OWASP
---

### Content
- **1 - GET/Select**
    1. Find column number of the SQL statement.
    2. Find name of the current database.
    3. Find version of the database.
- **2 - POST/Search**
    1. List table names and number of records in each table of the database.
    2. List columns names of each table.
- **3 - GET/Search**
    1. List all records in each table.
    2. Get credentials of a superhero by using id column of the related table. Go to SQL Injection (Login Form/Hero) bug and login with username and password of the superhero.
    3. Repeat the step 2 by not using the original password (In other words, you are expected to login without using the original password.). Interpret the result.
- **4 - Blind - Boolean-Based**
    1. Verify the name of the database found in GET/Select-2.
    2. Verify the version of the database found in GET/Select-3.
    3. Verify the e-mail address of a user listed in GET/Search-1.

## 1 - GET/Select

##### 1. Find column number of the SQL statement.

![Display error message](/img/mutillidae2/1-1.png)

This input has no filter so I continued the SQL query with “and 1=0” which will return false because I wanted to omit the results of the earlier query.

UNION ALL combines more than one SELECT query which is why I used it. 

I tried to fetch columns by incrementing the column number until I found the right column number. If it was not the right column number, the error which you can see above was displayed.

![Display column numbers](/img/mutillidae2/1-2.png)

##### 2. Find name of the current database.

![Display name of the database](/img/mutillidae2/1-3.png)

database() function outputs the name of the current database as seen above. This means that the current database name is bWAPP.

##### 3. Find version of the database.

![Display version of the database](/img/mutillidae2/1-4.png)

## 2 - POST/Search

##### 1. List table names and number of records in each table of the database.

![Table names and number of records](/img/mutillidae2/2-1.png)

| table_name | table_rows |
| :--------: | :--------: |
| blog       | 0          |
| heroes     | 6          |
| movies     | 10         |
| users      | 2          |
| visitors   | 0          |

##### 2. List columns names of each table.

![Column names](/img/mutillidae2/2-2.png)

![Column names](/img/mutillidae2/2-3.png)

| blog  | heroes   | movies         | users           | visitors   |
| :---: | :------: | :------------: | :-------------: | :--------: |
| id    | id       | id             | id              | id         |
| owner | login    | title          | login           | ip_address |
| entry | password | release_year   | password        | user_agent |
| date  | secret   | genre          | email           | date       |
|       |          | main_character | secret          |            |
|       |          | imdb           | activation_code |            |
|       |          | tickets_stock  | activated       |            |
|       |          |                | reset_code      |            |
|       |          |                | admin           |            |

## 3 - GET/Search

##### 1. List all records in each table.

-> blog

![blog records](/img/mutillidae2/3-1.png)

-> heroes

![heroes records](/img/mutillidae2/3-2.png)

-> visitors

![visitors records](/img/mutillidae2/3-3.png)

-> movies

![movies records](/img/mutillidae2/3-4.png)

![movies records](/img/mutillidae2/3-5.png)

-> users

![users records](/img/mutillidae2/3-6.png)

![users records](/img/mutillidae2/3-7.png)

![users records](/img/mutillidae2/3-8.png)

##### 2. Get credentials of a superhero by using id column of the related table. Go to SQL Injection (Login Form/Hero) bug and login with username and password of the superhero.

![get credentials of alice](/img/mutillidae2/3-9.png)

![use credentials of alice](/img/mutillidae2/3-10.png)

![login successful](/img/mutillidae2/3-11.png)

##### 3. Repeat the step 2 by not using the original password (In other words, you are expected to login without using the original password.). Interpret the result. 

![get error message to assess](/img/mutillidae2/3-12.png)

The original query was probably like this
```
“SELECT * FROM heroes WHERE login = ‘ $login ‘ AND password = ‘ $password ‘“
``` 

I changed it to 
```
“SELECT * FROM heroes WHERE login = ‘ alice’ OR ‘ AND password = ‘ ‘ ‘“ 
```
Since the login name is true, OR will return true.

![login without password](/img/mutillidae2/3-13.png)

## 4 - Blind - Boolean-Based

##### 1. Verify the name of the database found in GET/Select-2.

![get true message](/img/mutillidae2/4-1.png)

I could see that if the second part is true, the feedback would be “The movie exists in our database!”.

![get false message](/img/mutillidae2/4-2.png)

I could see that if the second part is false, the feedback would be “The movie does not exist in our database!”

![verify the name of the database](/img/mutillidae2/4-3.png)

Since the feedback is like that I confirmed that the database name is true.

##### 2. Verify the version of the database found in GET/Select-3.

![verify the version of the database](/img/mutillidae2/4-4.png)

##### 3. Verify the e-mail address of a user listed in GET/Search-1.

![example of false query output](/img/mutillidae2/4-5.png)

Subquery would return false because login was incorrect so the feedback was like this.

![verify the login credentials](/img/mutillidae2/4-6.png)

Subquery would return true since the login and emails were correct so I confirmed the email of the user “bee”.
