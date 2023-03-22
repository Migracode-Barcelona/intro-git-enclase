# 2 - SQL with Node

### Learning Objectives <a href="#learning-objectives" id="learning-objectives"></a>

* Add and remove columns in a pre-existing table using PostgreSQL using `ALTER`
* Rename tables and columns in a pre-existing table using PostgreSQL using `DELETE`
* Update rows in a pre-existing table using PostgreSQL using `UPDATE`
* Combine tables together using PostgreSQL using `INNER JOIN`
* Connect a PostgreSQL database to a NodeJS application
* Retrieve data from a PostgreSQL database in a NodeJS application

### More SQL <a href="#more-sql" id="more-sql"></a>

For the following, use the file [`cyf_hotels_exercise5.sql`](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-MRebciU3NcuLgsX3ijf%2F-MctcbHxY10DZkAIDQgV%2F-MctcmUQUsQojl8HShEo%2Fcyf\_hotels\_exercise5.sql?alt=media\&token=a5ed1123-4d94-41a5-be33-869f9c8ab89d) from the previous class to reinitialise your database with `psql -d cyf_hotels -f cyf_hotels_exercise5.sql`.

#### Changing the definition of a table <a href="#changing-the-definition-of-a-table" id="changing-the-definition-of-a-table"></a>

Sometimes, you may need to change the definition of a table you created before without deleting it. Such changes include renaming a table, adding/removing a column, changing the name of a column, changing the type of a column etc... The general syntax to perform these operations is:

```
ALTER TABLE table_name action;
```

For example, to add a new column to the existing `customers` table:

```
ALTER TABLE customers ADD COLUMN date_of_birth DATE;
```

To delete an existing column from the `customers` table:

```
ALTER TABLE customers DROP COLUMN date_of_birth;
```

To rename the table `customers` into `clients`:

```
ALTER TABLE customers RENAME TO clients;
```

For more examples, you can consult the following tutorial: [Postgres alter table](http://www.postgresqltutorial.com/postgresql-alter-table/).

**Exercise 1**

* Add a column `date_of_birth` of type `DATE` in the `customers` table.
* Rename the column `date_of_birth` to `birthdate` in the `customers` table.
* Delete the column `birthdate` from the `customers` table

#### Dropping a table <a href="#dropping-a-table" id="dropping-a-table"></a>

To delete the table `customers`:

```
DROP TABLE customers;
```

**Exercise 2:**

* Create a new table `test`
* Drop the table `test`

#### Updating a row <a href="#updating-a-row" id="updating-a-row"></a>

The general construction to update a row is:

```
UPDATE table SET column1 = value1, column2 = value2 WHERE condition;
```

For example, to update the name and country of the customers with ID 3:

```
UPDATE customers SET name='Bob Marley', country='Jamaica' WHERE id=3;
```

**Exercise 3**

* Update the postcode of the hotel named `Elder Lake Hotel` to `L10XYZ`
* Update the number of rooms of `Cozy Hotel` to `25`
* For the customer named `Nadia Sethuraman`, update her address to `2 Blue Street`, her city to `Glasgow` and her postcode to `G11ABC` in one query
* Update all the bookings of customer with ID `1` for the hotel with ID `1` to `5` nights in one query

#### Deleting a row <a href="#deleting-a-row" id="deleting-a-row"></a>

The syntax to delete a row is:

```
DELETE FROM table WHERE condition;
```

For example, to delete the booking with ID 4:

```
DELETE FROM bookings WHERE id=4;
```

**NOTE:** If you don't supply a `WHERE` clause with `DELETE` or `UPDATE` the command will be applied to **all** the rows in the table which is rarely what you want.

**Exercise 4**

* Delete the booking of customer ID `8` for the date `2020-01-03`
* Delete all the bookings of customer ID `6`
* Delete the customer with ID `6`

#### Joining tables <a href="#joining-tables" id="joining-tables"></a>

Sometimes, you will need to retrieve data which are spread in different tables in a single response. For this purpose, you will need to join tables together. The general syntax is:

```
SELECT A.column1, B.column2 FROM A INNER JOIN B ON A.b_id=B.id;
```

For example, to load all the bookings along with customer data:

```
SELECT * FROM customers INNER JOIN bookings ON customers.id=bookings.customer_id;
```

To load all the bookings along with customer data and hotel data:

```
SELECT * FROM bookings
INNER JOIN customers ON customers.id=bookings.customer_id
INNER JOIN hotels ON hotels.id=bookings.hotel_id;
```

To load the booking checkin dates for customer ID `1` along with the customer name and the hotel name:

```
SELECT bookings.checkin_date,customers.name,hotels.name FROM bookings
INNER JOIN customers ON customers.id=bookings.customer_id
INNER JOIN hotels ON hotels.id=bookings.hotel_id
WHERE customers.id=1;
```

**Exercise 5**

* Try and understand each of the queries above in your `psql` prompt
* Retrieve all the bookings along with customer data for bookings starting in 2020
* Retrieve the customer names, booking start dates and number of nights for all customers who booked the hotel name `Jade Peaks Hotel`
* Retrieve all the booking start dates with customer names and hotel names for all bookings for more than 5 nights

#### Other useful operations <a href="#other-useful-operations" id="other-useful-operations"></a>

Ordering the result:

```
SELECT * FROM table ORDER BY column;
```

This will sort the returned rows in the ascending order for "column". To sort them in descending order, use:

```
SELECT * FROM table ORDER BY column DESC;
```

Limiting the number of results returned:

```
SELECT * FROM table LIMIT 10;
```

Returning all customers whose ID is 1, 2, 3 or 4:

```
SELECT * FROM customers WHERE id IN (1,2,3,4);
```

Query by pattern matching, for example retrieve all customers whose name starts with Bob:

```
SELECT * FROM customers WHERE name LIKE 'Bob%';
```

You can combine different operations together, for example, if you want to retrieve all the booking start dates with the customer names and hotel names for customer names starting with the letter `M` ordered by hotel name with a limit of 3 results:

```
SELECT bookings.checkin_date,customers.name,hotels.name FROM bookings
INNER JOIN customers ON customers.id=bookings.customer_id
INNER JOIN hotels ON hotels.id=bookings.hotel_id
WHERE customers.name LIKE 'M%'
ORDER BY hotels.name
LIMIT 3;
```

**Exercise 6**

* Retrieve all customers whose name starts with the letter `S`
* Retrieve all hotels which have the word `Hotel` in their name
* Retrieve the booking start date, customer name, hotel name for the top 5 bookings ordered by number of nights in descending order

### Integration with NodeJS <a href="#integration-with-nodejs" id="integration-with-nodejs"></a>

#### Introduction to node-postgres <a href="#introduction-to-node-postgres" id="introduction-to-node-postgres"></a>

_"node-postgres is a collection of node.js modules for interfacing with your PostgreSQL database."_ - [https://node-postgres.com/](https://node-postgres.com/)

In the following, we will use _node-postgres_ to...

1. Connect to a database
2. Send SQL query to the database and get results

#### Loading data from a database with a GET endpoint <a href="#loading-data-from-a-database-with-a-get-endpoint" id="loading-data-from-a-database-with-a-get-endpoint"></a>

Let's build a brand new NodeJS application with a single GET endpoint to load the list of hotels that you already have in the `hotels` table of the `cyf_hotels` database.

First, create a new NodeJS application that we will call **cyf-hotels-api** (enter `server.js` when asking about the entry point):

```
mkdir cyf-hotels-api && cd cyf-hotels-api && npm init
```

As before, we will use the Express library to build our API, and the node-postgres library to connect with our database:

```
npm install express
npm install pg
```

Create a `server.js` file, import express, initialise the server and start listening for requests:

```
const express = require("express");
const app = express();

app.listen(3000, function() {
    console.log("Server is listening on port 3000. Ready to accept requests!");
});
```

Import pg library and create a new GET endpoint to load the list of hotels:

```
const { Pool } = require('pg');

const pool = new Pool({
    user: 'postgres',
    host: 'localhost',
    database: 'cyf_hotels',
    password: '',
    port: 5432
});

app.get("/hotels", function(req, res) {
    pool.query('SELECT * FROM hotels', (error, result) => {
        res.json(result.rows);
    });
});
```

In the code above:

* We first import the `Pool` class from the pg library, which is used to connect to a database. [Database connection Pooling](https://node-postgres.com/features/pooling) is a method used to keep database connections open so they can be reused. Pooling keeps the connections active so that, when a connection is later requested, one of the active ones is used in preference to having to create another one.
* We create a new pool where we specify the credentials to connect to the cyf\_hotels database
* We then create a new /hotels endpoint where we use the method `query()` to send a SQL query to load all the hotels from the table `hotels` and return the results with `result.rows`. You can write any valid SQL query that you learned in the `query()` method!

Start your server with `node server.js` and try to reach the `/hotels` endpoint to see the list of hotels currently available in your `hotels` table of your `cyf_hotels` database. You can try to create/update/delete hotels to verify that your API always returns what is stored in your database.
