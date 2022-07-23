# Challenge 9

## MongoDB

### Instructions

**Format:** text file with the queries made and the database folder compressed in a zip.

Using Mongo Shell, create a database called ecommerce that contains two collections: messages and products.

1) Add 10 documents with different values ​​to the messages and products collections. The format of the documents must be in correspondence with the one we have been using in the MariaDB database deliverable.
2) Define the keys of the documents in relation to the fields of the tables of that database. In the case of products, put values ​​in the price field between 100 and 5000 pesos (choosing intermediate values, eg: 120, 580, 900, 1280, 1700, 2300, 2860, 3350, 4320, 4990).
3) List all documents in each collection.
4) Show the number of documents stored in each of them.

5) Perform a CRUD on the product collection:
- Add one more product in the product collection
- Make a query by specific product name:
  - List the products with a price less than 1000 pesos.
  - List the products with a price between 1000 to 3000 pesos.
  - List the products with a price greater than 3000 pesos.
  - Make a query that brings only the name of the third cheapest product.
- Make an update on all the products, adding the stock field to all of them with a value of 100.
- Change the stock to zero of products with prices greater than 4000 pesos.
- Delete products with a price less than 1000 pesos
  
6) Create a user 'pepe' key: 'asd456' that can only read the ecommerce database. Verify that pepe cannot change the information.
