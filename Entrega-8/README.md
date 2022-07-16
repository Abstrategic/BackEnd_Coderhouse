# Challenge 8
## Our first database

### Instructions

- Based on the Container classes in memory and in files, develop a new container with identical methods but that works on databases, using Knex for the connection. This class must receive in its constructor the Knex configuration object and the name of the table on which it will work. Then modify the challenge deliverable from class 6, and

    - change persistence of filesystem messages to SQLite3 database.
    - change persistence of memory products to MariaDB database.

- Also develop a script that, using knex, creates the necessary tables for the persistence in question (messages table in sqlite3 and products table in mariaDb).

*Grades:*
Define a DB folder to store the SQLite3 database called ecommerce

## Resolution

The following scheme is proposed so that each Cart can have products, only if the cart and the product exist. Also, if a product or a cart is deleted, it is cascaded in the relationship table.

![Basic table diagram][(https://raw.githubusercontent.com/Abstrategic/BackEnd_Coderhouse/blob/main/Entrega-8/currentSchema.png)](https://github.com/Abstrategic/BackEnd_Coderhouse/blob/main/Entrega-8/currentSchema.png)

### Create Tables and rows via script

With SQLite and/or MySQL configured, just run the following command via terminal and the tables will be created and populated automatically.

```console
.../delivery-8 $ npm run rebuildDB

    > release-8@1.0.0 rebuildDB
    > node ./src/dao/start/RebuildDB.js

    🟢 The table <product> has been created
    🟢 Table <cart> has been created
    🟢 The table <productCart> has been created
    🧪 Products were added to the table
    🛒 Carts were added to the table
    🛒<->🧪 Relationships were added to the table

```

### Example of the rows of each table

```console
SELECT * FROM producto;
+----+---------------------+----------------+-------+--------------------------+------+-------------------+-------+
| id | timestamp           | title          | price | description              | code | image             | stock |
+----+---------------------+----------------+-------+--------------------------+------+-------------------+-------+
| 1  | 2022-04-09 00:31:53 | Some Product 1 | 100.0 | Some dummy description 1 | XY-1 | someDummyUrl1.com | 150   |
| 2  | 2022-04-09 00:31:53 | Some Product 2 | 200.0 | Some dummy description 2 | XY-2 | someDummyUrl2.com | 250   |
| 3  | 2022-04-09 00:31:53 | Some Product 3 | 300.0 | Some dummy description 3 | XY-3 | someDummyUrl3.com | 350   |
+----+---------------------+----------------+-------+--------------------------+------+-------------------+-------+
```

```console
SELECT * FROM carrito;
+----+---------------------+
| id | timestamp           |
+----+---------------------+
| 1  | 2022-04-09 01:33:37 |
| 2  | 2022-04-09 01:34:00 |
| 6  | 2022-04-09 01:36:02 |
| 7  | 2022-04-09 01:36:03 |
+----+---------------------+
```

```console
SELECT * FROM productoCarrito;
+----+-----------+------------+
| id | carritoId | productoId |
+----+-----------+------------+
| 8  | 7         | 2          |
| 9  | 7         | 1          |
| 10 | 7         | 3          |
+----+-----------+------------+

The cart of id (7) has product 1, 2 and 3 inside

```
