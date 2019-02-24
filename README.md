![Kickstart Coding Logo](./logo.png)

# Kickstart PostgreSQL: Getting Started

Tutorial for setting up PostgreSQL using Heroku.

## Who is this guide for

* This is for **brand new SQL programmers**, including **coding class
  students** who want a simple and to-the-point guide on connecting to
  a Heroku provisioned Postgres database.

* This guide assumes you already have fundamental Bash and Heroku knowledge. If
  you are new to Heroku, read our [Heroku Getting Started
  guide](http://github.com/kickstartcoding/heroku-getting-started/).

* This guide *does not* support Windows. It assumes you use either **macOS** or
  **Ubuntu GNU/Linux**.

> This was original created for Kickstart Coding, the affordable,
> inclusive, and intensive coding course teaching cutting-edge Python /
> Django and JavaScript / React web development in Oakland, CA.
> [Learn more and enroll here.](http://kickstartcoding.com/?utm_source=github&utm_campaign=cheatsheets)


# What is PostgreSQL?

Databases are how computers and web applications store thousands or millions of
items of data, and look them up quickly.  SQL is the most popular programming
language for talking to databases.

Postgres is one of the most popular and powerful databases systems out
there, and it uses a dialect of SQL.

Heroku is a hosting service that also provides a "free-tier" version of
Postgres that they will run for us.

### Key terms

* **database** - How web apps store lots and lots of data. In some ways,
  databases resemble Excel spreadsheets, because they store grids ("tables") of
  data.

* **SQL** - The programming language for talking to databases.

* **Postgres** - A popular and powerful database management system ("DBMS")
  that uses SQL.

### Database terminology

Note: See bottom of this guide for an spreadsheet analogy.

* **table** - A named collection of data. Consists of series of columns. A
  database can have multiple tables.

* **column** - A named column of data. A table must have 1+ columns.

* **row** - A single item of data. Found within tables, and has values (e.g.
  table data cells) for each column in that table. A table can have 0+ rows,
  such as one for each user.

### (Less) Key Terms

* **Sqlite** - A simple, limited version of SQL, that's great for learning and
  simple applications, but does not work for web apps with multiple users

* **MySQL** - Another popular database and SQL dialect (bought by Oracle).
  MariaDB is a truly free software spin-off of this.

* **MS SQL** - Another popular database and SQL dialect (by Microsoft).

* **schema** - A common and flexible term that more or less means the shape or
  layout of your database. In Postgres, also it means a way for a database to
  further "group together" it's tables (more or less).

* **Heroku** (the business) - a company that will run your HTTP server
  application for you, and expose it to the web. They also offer free Postgres
  servers, which is what we are using from them.

* `heroku` (the CLI command) - A tool that Heroku the company has developed
  which we will use for interacting with your Heroku account, including
  creating new Postgres databases.


# Guide

Now that you know a little about Postgres, it's time to install the client on
your system and get practice connecting to a Heroku hosted version of it.

## Installing Postgres client

Ubuntu Linux users, run the following command:
```bash
sudo apt-get install postgresql-client
```

macOS users can't install the client separately, so run the following command
to install everything:

```bash
brew install postgres
```

## Provisioning a Postgres database on Heroku

First you will need to have a Heroku app already created. This can be either a
project you are working on, or just a brand new thing. If you don't have an
app, you can use `heroku create` to create one.

1. Provision for that app a new Postgres Database (free "hobby" tier):

```bash
heroku addons:create heroku-postgresql:hobby-dev --app pure-crag-68
```

2. Connect to your database with the command-line client:

```bash
heroku pg:psql --app pure-crag-68
```


*NOTE:* For the these last commands, you will need to change "pure-crag-68" to
the similarly random name your app got when you created it.

## Connecting to your database

Connect to your database with the commandline client:

```bash
heroku pg:psql --app pure-crag-68
```


## Practicing SQL


For the second challenge, create the tables necessary to house the following
data. Add the data, and practice querying it.

Example code to run with Postgres:


* Create a new table

```sql
CREATE TABLE people (
    idnum int,
    first_name varchar(255),
    last_name varchar(255)
);
```

* Check which tables we have

```sql
\d
\d people
```

* Add data to a table

```sql
INSERT INTO people (id, first_name, last_name)
VALUES (1, 'Jane', 'Hacker');
```

* Check the data in a table

```sql
SELECT * FROM people;
```

* **Challenge:** Add data for a person with first name `"Dolan"` and last name
  `"Duck"`, and ID number `2`. Ensure it is added with `SELECT`.


# Playing with test data

Included in this repo is a SQL file that contains information on the 50 states
in the USA, including Puerto Rico and District of Columbia.

1. Copy & paste that SQL file into your window (or be clever and redirect it
into the Postgres prompt using Bash).

2. View the data:

```sql
SELECT * FROM states;
```

3. Try using `WHERE` in conjunction to `SELECT` to look for states with
different characteristics (will have to Google for more information on
`WHERE`). (e.g. Only mid-sized states, with population between 5 and 10
million).

4. Try using `ORDER BY` in conjunction to `SELECT` to sort the output by
different orderings. (e.g. Sorted by population, least populated first)

5. Try using `LIMIT` to only select the top state that matches a certain
ordering and criteria. (e.g. only the most populous state that starts with the
letter `M`).

# Extra challenges

* Look up remaining SQL commands. Get practice with all the different options
  for `SELECT`, `INSERT`, `DELETE`, `UPDATE`.

* If you have time, look up online tutorials on installing and running Postgres
  locally (as opposed to Heroku). This is something you may need to do at some
  point in the future, so doesn't hurt playing around with that now. It isn't
  too hard, though sometimes can have hang-ups.

# SQL Tips

* Don't forget to end all your SQL statements with ";"! Otherwise it will think
  you are still adding on to the same statement, and typically result in a
  syntax error.

* If you use an ORM, such as Django ORM, it is actually writing and reading the
  SQL code for you under the hood.  Even using an ORM, you will often need to
  know how to use SQL for certain operations, or at least understand what is
  happening.

* All versions (dialects) of SQL are about ~90% the same, so if you learn one,
  you'll be able to use others.

* If you are having a hard time understanding DBs, it might help to think of
  them as kind of like a spreadsheet software, such as Microsoft Excel.  This
  is a very rough analogy, but maybe this will help:

| SQL term      | Excel         |
| ------------- |--------------:|
| database      | .xlsx file    |
| table         | worksheet     |
| column        | column        |
| row           | row           |

