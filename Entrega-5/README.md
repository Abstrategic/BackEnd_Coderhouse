# Challenge 5
## Template Engines

### Instructions


1) Using the same product API of the deliverable project of the previous class, build a web server (not REST) ​​that incorporates:

   - A product upload form in the root path (set the '/products' path to receive the POST, and redirect to the same form).

   - A view of the products loaded (using handlebar templates) in the GET route '/products'.

   - Both pages will have a button that redirects to the other.

2) Keeping the same functionality replace the handlebars templating engine with **pug**.
   
3) Keeping the same functionality replace the template engine handlebars with **ejs**.

4) In writing, indicate which of the three template engines you prefer for your project and why.

#### Aspects to include in the deliverable:

- Make the corresponding templates that allow you to go through the array of products and represent it in the form of a dynamic table, with the headers being the name of the product, the price and its photo (the photo will be shown as an image in the table)

- If no data is found, display the message: 'There are no products'.

#### Suggestions:

- Use iconfinder (https://www.iconfinder.com/free_icons) to get the url of the product images (right click on the image -> copy image address)
