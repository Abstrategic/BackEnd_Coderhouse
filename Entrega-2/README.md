# Challenge 2
## Handle files asynchronously with Node

### Instructions

1) Implement a program that contains a class called Container that receives the name of the file with which it is going to work and implements the following methods:
   
- **save(Object)**: Number - Receives an object, saves it to the file, returns the assigned id.
- **getById(Number)**: Object - Receives an id and returns the object with that id, or null if it is not present.
- **getAll()**: Object[] - Returns an array with the objects present in the file.
- **deleteById(Number)**: void - Deletes the object with the searched id from the file.
- **deleteAll()**: void - Deletes all objects present in the file.

2) **Aspects to include in the deliverable:**
   
- The save method will add a numeric id to the product, which must always be one more than the id of the last object added (or id 1 if it is the first object added) and cannot be repeated.

- Take into consideration the previous content of the file, in case of using an existing one.

- Implement file handling with the node.js fs module, using promises with async/await and error handling.

- Test the module by creating a product container, which is saved in the file: "products.txt"

- Include a test call to each method, and showing it on the screen as appropriate to verify the correct functioning of the built module.

- The format of each product will be:

```json
{
    "title": "(product name)",
    "price": "(price)",
    "thumbnail": "(product photo url)"
}
```
### Example

Content of "products.txt" with 3 stored products

```json
[                                                                                                                                                     
    {                                                                                                                                                    
      "title": "Escuadra",                                                                                                                                 
      "price": 123 45,                                                                                                                                     
      "thumbnail": "https://cdn3.iconfinder.com/data/icons/education-209/64/ruler-triangle-stationary-school-256.png",                                     
      "id": 1                                                                                                                                              
    },                                                                                                                                                   
    {                                                                                                                                                    
      "title": "Calculadora",                                                                                                                              
      "price": 234.56,                                                                                                                                     
      "thumbnail": "https://cdn3.iconfinder.com/data/icons/education-209/64/calculator-math-tool-school-256.png",                                          
      "id": 2                                                                                                                                              
    },                                                                                                                                                   
    {                                                                                                                                                    
      "title": "Globo Terráqueo",                                                                                                                          
      "price": 345.67,                                                                                                                                     
      "thumbnail": "https://cdn3.iconfinder.com/data/icons/education-209/64/globe-earth-geograhy-planet-school-256.png",                                   
      "id":3                                                                                                                                              
    }                                                                                                                                                    
  ]  

```

