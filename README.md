# Advanced SQL - Aggregate functions

## Description

In this exercise, we will practice on more elaborate uses of grouping and aggregation.

##

## Tasks

###

### Task 1

Create a new database and execute the file [src/data/task1.sql](src/data/task1.sql). This file contains the following tables:

- **webinar**
    - **id**. Identifier. `serial`, `PRIMARY KEY`
    - **name**. Name/topic of the webinar. `varchar(200)`
    - **teacher_id**. The ID of the person who conducted the webinar. `integer`
    - **visibility**. Whether it is public or private. `enum('Public', 'Private')`
    - **starts_on**. Date and time the seminar started. `timestamp`
    - **ends_on**. Date and time the seminar ended. `timestamp`
    - **audience**. Number of people who attended the webinar. `integer`

- **teacher**
    - **id**. Identifier. `serial`, `PRIMARY KEY`
    - **name**. Name of the teacher. `varchar(100)`
    - **city**. City where the teacher lives. `varchar(100)`

One same topic (name) is covered in more than one webinar, with different dates and audiences.

Your task is to write and execute an SQL statement to show the total number of webinars, first starting time, last ending time, total audience and average audience of the 10 most popular topics/names (those with the highest average audience).

- Your result should look like this:

| name                             | Total | First started on       | Last ended on          | Total audience | Average audience |
|----------------------------------|-------|------------------------|------------------------|----------------|------------------|
| Hands on Python                  | 7     | 2007-06-21 10:32:28+02 | 2020-04-26 10:56:00+02 | 243            | 34.7142857142857 |
| Advanced Django Admin            | 5     | 2006-03-21 10:30:57+01 | 2021-01-17 10:46:12+01 | 162            | 32.4             |
| Hands on Databases               | 6     | 2009-07-07 01:26:40+02 | 2014-03-01 13:11:49+01 | 194            | 32.3333333333333 |
| Hands on Python OOP              | 9     | 2005-01-15 09:03:36+01 | 2020-06-27 05:26:50+02 | 273            | 30.3333333333333 |
| Hands on Django ORM              | 6     | 2007-05-27 02:56:33+02 | 2021-03-01 17:55:20+01 | 172            | 28.6666666666667 |
| Hands on Django Admin            | 11    | 2005-09-01 07:14:09+02 | 2018-05-22 11:43:39+02 | 306            | 27.8181818181818 |
| Advanced Django                  | 16    | 2005-08-17 03:24:24+02 | 2020-03-29 09:50:55+02 | 442            | 27.625           |
| Introduction to Django Templates | 12    | 2007-10-09 00:31:38+02 | 2020-01-04 21:56:26+01 | 306            | 25.5             |
| Advanced Python Algorithms       | 15    | 2005-11-23 15:57:30+01 | 2021-04-04 18:34:24+02 | 382            | 25.4666666666667 |
| Hands on Computer                | 6     | 2009-07-16 10:17:40+02 | 2021-03-14 23:45:01+01 | 152            | 25.3333333333333 |

###

### Task 2

Now execute the file [src/data/task2.sql](src/data/task2.sql) on the same database to add the following tables:

- **student**
    - **id**. Local identifier of the student. `serial`, `PRIMARY KEY`
    - **name**. Name of the student. `varchar(25)`
    - **city**. Name of the city where the student lives. `varchar(25)`
    - **mentor_id**. ID of the student's mentor. `integer`

- **registration**
    - **student_id**. ID of the student registered. `integer`
    - **webinar_id**. ID of the webinar registered. `integer`
    - **date**. Date and time of the registration. `timestamp`

This file will also remove the field `audience` from the table `webinar`.

Your first task now is to calculate the audience of each webinar using the new `registration` table. Write an SQL statement that produces a list of all webinars with their total students registered.

> Each record in the table `webinar` must appear only once in the result.
>
> The result should include, at least, the fields `Webinar name`, `Started on` and `Audience` and should be sorted first by webinar name and, then, by the date they started.

- Your result should look like this:

| Webinar name       | Started on             | Audience |
|--------------------|------------------------|----------|
| Advanced Computer  | 2006-09-30 05:18:41+02 | 24       |
| Advanced Computer  | 2010-02-18 15:03:01+01 | 16       |
| Advanced Computer  | 2011-12-11 00:33:05+01 | 32       |
| Advanced Computer  | 2013-04-22 22:17:24+02 | 36       |
| Advanced Computer  | 2020-07-27 05:03:57+02 | 29       |
| Advanced Computer  | 2021-05-04 12:59:55+02 | 24       |
| Advanced Databases | 2005-07-11 20:34:23+02 | 20       |
| Advanced Databases | 2007-07-09 07:23:16+02 | 26       |
| Advanced Databases | 2008-07-26 16:38:37+02 | 28       |
| Advanced Databases | 2010-06-01 04:48:05+02 | 34       |
| ...                | ...                    | ...      |


###

### Task 3

Now find out how many students registered in, at least, one of their mentor's webinars.

- Your result should look like this:

| count |
|-------|
| 62    |


###

### Task 4

Now produce a list of all student names and webinar names they have been registered to.

Build this SQL statement first and then adapt it to show the total audience of that webinar in a third column.

> HINT: You may join another copy of the `registration` table to the first one, matching by webinar_id, to count the audience.

- Your result should be sorted by student's name first and then by webinar's name and should look like this:

| Student       | Webinar                          | Audience |
|---------------|----------------------------------|----------|
| Aaliyah Adams | Advanced Python Algorithms       | 29       |
| Aaliyah Adams | Hands on Python Algorithms       | 20       |
| Aaliyah Ahmas | Introduction to Computer         | 24       |
| Aaliyah Ahmas | Introduction to Django           | 19       |
| Aaliyah Ali   | Advanced Computer                | 24       |
| Aaliyah Ali   | Hands on Computer                | 24       |
| Aaliyah Ali   | Hands on Databases               | 35       |
| Aaliyah Ali   | Hands on Django Templates        | 24       |
| Aaliyah Ali   | Hands on Python Algorithms       | 20       |
| Aaliyah Allen | Advanced Databases               | 33       |
| Aaliyah Allen | Advanced Python OOP              | 27       |
| ...           | ...                              | ...      |
