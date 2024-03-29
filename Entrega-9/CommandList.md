# List of commands used

- Creating the database

```console
use ecommerce;
```

- Creating the collections

```console
db.createCollection('productos');
db.createCollection('carritos');
```

- Inserting rows in products

```console
db.productos.insertMany([
    {
        "timestamp": ISODate(),
        "title": "Product 1",
        "price": 100,
        "description":"Some description for product 1",
        "code": "XP-1",
        "image": "someUrlProduct1.com",
        "stock": 100
    },
    {
        "timestamp": ISODate(),
        "title": "Product 2",
        "price": 320,
        "description":"Some description for product 2",
        "code": "XP-2",
        "image": "someUrlProduct2.com",
        "stock": 200
    },
    {
        "timestamp": ISODate(),
        "title": "Product 3",
        "price": 930,
        "description":"Some description for product 3",
        "code": "XP-3",
        "image": "someUrlProduct3.com",
        "stock": 300
    },
    {
        "timestamp": ISODate(),
        "title": "Product 4",
        "price": 1140,
        "description":"Some description for product 4",
        "code": "XP-4",
        "image": "someUrlProduct4.com",
        "stock": 400
    },
    {
        "timestamp": ISODate(),
        "title": "Product 5",
        "price": 2250,
        "description":"Some description for product 5",
        "code": "XP-5",
        "image": "someUrlProduct5.com",
        "stock": 500
    },
    {
        "timestamp": ISODate(),
        "title": "Product 6",
        "price": 3360,
        "description":"Some description for product 6",
        "code": "XP-6",
        "image": "someUrlProduct6.com",
        "stock": 600
    },
    {
        "timestamp": ISODate(),
        "title": "Product 7",
        "price": 4470,
        "description":"Some description for product 7",
        "code": "XP-7",
        "image": "someUrlProduct7.com",
        "stock": 700
    },
    {
        "timestamp": ISODate(),
        "title": "Product 8",
        "price": 5000,
        "description":"Some description for product 8",
        "code": "XP-8",
        "image": "someUrlProduct8.com",
        "stock": 800
    },
    {
        "timestamp": ISODate(),
        "title": "Product 9",
        "price": 3450,
        "description":"Some description for product 9",
        "code": "XP-9",
        "image": "someUrlProduct9.com",
        "stock": 900
    },
    {
        "timestamp": ISODate(),
        "title": "Product 10",
        "price": 2860,
        "description":"Some description for product 10",
        "code": "XP-10",
        "image": "someUrlProduct10.com",
        "stock": 1000
    }
]);
```

- Inserting some products in cart

```console
db.carritos.insertMany([{timestamp: ISODate()}, {timestamp: ISODate()}])
```

- Listing the products of the cart

```console
db.productos.find();
```



- Counting the quantity of product document

```console
db.productos.countDocuments();
```

- Add more products in 'Product' section
```console
db.productos.insertOne({
        "timestamp": ISODate(),
        "title": "Product 11",
        "price": 3860,
        "description":"Some description for product 11",
        "code": "XP-11",
        "image": "someUrlProduct11.com",
        "stock": 1100
    });
```

- Retrieve the **title** of the product which have the code **XP-11**

```console
db.productos.find({code: "XP-11"}, {title: 1, _id:0});
```

- Listing the product which minor price of $1000 :

```console
db.productos.find({price: {$lt: 1000}});
```

- Listing the product with the price between $1000 to $3000.

```console
db.productos(find {price: {$gt: 1000, $lt: 3000 });
```

- Listing thie product with the price more than $3000.

```console
db.productos.find({price: {$gt: 3000}});
```


- Make a query that brings only the name of the third cheapest product.

```console
db.productos.find({},{title:1, _id:0}).sort({price:1}).skip(2).limit(1);
```


- Make an update on all the products, adding the stock field to all of them with a value of 100.

```console
db.productos.updateMany({}, {$inc: {stock: 100}});
```


- Change the stock to zero of products with prices greater than $4,000. 

```console
db.productos.updateMany({price: {$gt: 4000}}, {$set: {stock: 0}});
```


- Delete products with a price less than $1000

```console
db.productos.deleteMany({price: {$lt: 1000}});
```


- Creation of user **pepe**, with password: **asd456**. read-only permission
  
```console
db.createUser({user: "pepe", pwd: "asd456", roles: [{role: "read", db: "ecommerce"}]});
```

- Login of the previously created user

```console
mongo -u pepe -p --authenticationDatabase ecommerce 
```

- View of the DBs you have access

```console
> show dbs
ecommerce  0.000GB
```

- Attempting to add a *product* to the **product** collection in the **ecommerce** db

```console
> use ecommerce
switched to db ecommerce
> db.productos.insertOne({nombre: "someName"})
uncaught exception: WriteCommandError({
	"ok" : 0,
	"errmsg" : "not authorized on ecommerce to execute command { insert: \"productos\", ordered: true, lsid: { id: UUID(\"0472ecf7-1bf2-47c1-8616-00278992617c\") }, $db: \"ecommerce\" }",
	"code" : 13,
	"codeName" : "Unauthorized"
})
```
### Important disclaimer❗❗❗

In my case I am using:

- MongoDB shell version **v5.0.6**
- MongoDB server version: **5.0.6**
  
For authorization to take effect, the following config must be in **mongod.conf**

```console
security:
  authorization: "enabled"
```
