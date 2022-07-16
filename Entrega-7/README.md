# Challenge 7
## First delivery of the final project

### Instructions

You must deliver the progress status of your eCommerce Backend application, which implements an application server based on the Node.js platform and the express middleware. The server will implement two sets of routes bundled into routers, one with the base url '/products' and the other with '/cart'. The listening port will be 8080 for development and process.env.PORT for production on glitch.com

1) The base router '/api/products' will implement four functionalities:
   
    -GET: '/:id?' - It allows me to list all available products or a product by its id (available for users and administrators)
    -POST: '/' - To add products to the list (available for administrators)
    -PUT: '/:id' - Update a product by its id (available for administrators)
    -DELETE: '/:id' - Delete a product by its id (available for administrators)

2) The base router '/api/cart' will implement three routes available for users and administrators:
    - POST: '/' - Creates a cart and returns its id.
    - DELETE: '/:id' - Empty a cart and delete it.
    - GET: '/:id/products' - Allows me to list all the products saved in the cart
    - POST: '/:id/products' - To add products to the cart by their product id
    - DELETE: '/:id/products/:id_prod' - Remove a product from the cart by its cart and product id
  
  
3) Create an administrator boolean variable, whose value we will configure later with the login system. Depending on its value (true or false) it will allow me to reach or not the indicated routes. In the case of receiving a request to a route not allowed by the profile, return an error object. Example: { error : -1, description: path 'x' method 'y' not authorized}

4) A product will have the following fields: id, timestamp, name, description, code, photo (url), price, stock.

5) The shopping cart will have the following structure:
id, timestamp(cart), product: { id, timestamp(product), name, description, code, photo (url), price, stock }
6) The timestamp can be implemented with Date.now()
7) Start working with the product listing and shopping cart in server memory, then persist them to the filesystem.

**To consider:**

1) To perform the functionality test there are two options:
    - Test with postman each of the endpoints (products and cart) and their operation as a whole.
    - Make a simple frontend application, using HTML/CSS/JS or any preferred framework, that represents the list of products in the form of cards. Each card contains the product data, which, in the case of being administrators, we can edit your information. For the latter case, add the update and delete buttons. We will also have a new product entry form with the corresponding fields and a submit button. Likewise, build the cart view where you can see the added products and incorporate products to buy by their product id. This frontend application must send get, post, put and delete requests to the server using fetch and must be offered in your public space.

2) In all cases, the dialog between the frontend and the backend must be in JSON format. The server must not generate any views.
3) In the case of requesting a route not implemented in the server, it must answer an error object: eg { error : -2, description: route 'x' method 'y' not implemented}
4) The programming structure will be ECMAScript, separated into three basic modules (router, business logic/api and persistence). Later we will implement layered development. Preferably use classes, let and const variable constructors and arrow function.
5) Perform full functionality test at local scope (port 8080) and at glitch.com
