# Challenge 4
## RESTful API

### Instructions

Make a server project based on node.js and express that offers a RESTful API of products. In detail, it incorporates the following routes:

- **GET** */api/products* -> returns all products.
- **GET** */api/products/:id* -> returns a product according to its id.
- **POST** */api/products* -> receives and adds a product, and returns it with its assigned id.
- **PUT** */api/products/:id* -> receives and updates a product according to its id.
- **DELETE** */api/products/:id* -> deletes a product according to its id.

- Each product will be represented by an object with the following format

```json
{
    "title": "(product name)",
    "price": "(price)",
    "thumbnail": "(url to logo or product photo)"
}
```
- Each stored item will have a numerical id provided by the backend, starting at 1, and which will increase as products are added. That id will be used to identify a product that will be listed individually.

- In the event that a product does not exist, the object will be returned:
{ error : 'product not found' }

- Implement the API methods in a separate class, using a container of those developed in previous classes for the persistence of its products.

- Incorporate the Express Router in the base url '/api/products' and configure all sub-routes based on it.

- Create a public server space that contains an index.html document with a product entry form with the appropriate data.

- The server must be based on express and must implement connection messages to port 8080 and, in case of error, represent its description.

- The responses from the server will be in JSON format. The functionality will be tested through Postman and the login form.

## To test API you can do the following

1. Be in the **'Delivery-4'** directory

2. Install dependencies with: `npm install`

3. Start the server with `npm run server`

----

### `GET | http://localhost:8080/api/products`

✅ *Answer:*

```json
[
    {
        "title": "Squad",
        "price": 75.66,
        "thumbnail": "someUrl.com",
        "id": 1
    },
    {
        "title": "Calculator",
        "price": 72.66,
        "thumbnail": "someUrl.com",
        "id": 2
    }
]
```
### `GET | http://localhost:8080/api/products/:id`

For `http://localhost:8080/api/products/3`

✅ *Answer:*

```json
{
    "title": "Pen",
    "price": 100,
    "thumbnail": "someUrl.com",
    "id": 3
}
```

For an ID that is not present, for example: `http://localhost:8080/api/products/321321`

❌ *Answer:*

```json
{
    "error": "Product not found"
}
```

### `POST | http://localhost:8080/api/products`

*Request:*

Body in JSON (not validated)

```json
{
    "title": "NewItem",
    "price": 3100,
    "thumbnail": "someNewUrl.com",
}
```

*Response:*

✅ `Product added with the ID: 5`


### `PUT | http://localhost:8080/api/products/:id`

For `http://localhost:8080/api/products/2`

*Request:*

Body in JSON (not validated, the 3 fields are required)

```json
{
    "title": "New Updated Title",
    "price": 125,
    "thumbnail": "someUpdatedUrl.com"
}

```

*Response:*

✅ `Product ID: 2 was updated`

For an ID that is not present, for example: `http://localhost:8080/api/products/321321`

*Response:*

❌ `The product was not updated because the ID: 3123 was not found`

### `DELETE | http://localhost:8080/api/products/:id`

For `http://localhost:8080/api/products/3`

*Response:*

✅ `Product ID: 3 was deleted`

For an ID that is not present, for example: `http://localhost:8080/api/products/321321`

*Response:*

❌ `The product was not deleted because the ID: 321321 was not found`
