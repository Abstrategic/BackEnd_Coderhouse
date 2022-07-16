# Challenge 1
## Review of classes(OOP) in JS

### Instructions

1) Declare a User class

2) Make User have the following attributes:

- **name**: String
- **surname**: String
- **books**: Object[]
- **Mascotas**: String[]

The values of the attributes must be loaded through the constructor, when creating the instances

3) Make User count with the following methods:

- **getFullName()**: String. Returns the full name of the user. Use template strings.
- **addPet(String)**: void. Receives a pet name and adds it to the pet array.
- **countMascotas()**: Number. Returns the number of pets the user has.
- **addBook(String, String)**: void. It receives a string 'name' and a string 'author' and must add an object: {name: String, author: String} to the array of books
- **getBookNames()**: String[]. Returns an array with only the names of the user's book array.

4) Create an object called user with arbitrary values ​​and call all its methods.

### Examples

- *countMascotas*: Assuming the user has these pets: ['dog', 'cat']. user.countMAscotas() should return 2
- *getBooks*: assuming the user has these books: [{name: 'Lord of the Flies', author: 'William Golding'}, {name: 'Foundation', author: 'Isaac Asimov'}]. user.getBooks() should return: ['Lord of the Flies', 'Foundation'].
- *getFullName*: Assuming the user has a first name 'Elon' and a last name 'Musk'. user.getFullName() should return 'Elon Musk'.
