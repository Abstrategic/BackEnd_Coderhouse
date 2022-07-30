# Challenge 10

## Second delivery of the final project
### Instructions

Based on the containers already developed (memory, files), create two more containers (that comply with the same interface) that allow basic CRUD operations to be carried out in MongoDb (either local or remote) and Firebase. Then, for each container, create two derived classes, one to work with Products and one to work with Carts.

### Aspects to include in the deliverable:
- The classes derived from the containers are known as DAOs (Data Access Objects), and they can all be included in the same 'daos' folder.
- In the data folder, include a file that imports all the classes and exports a product data instance and a cart data instance, as appropriate. This decision will be made based on the value of an environment variable loaded at server run time (optional: investigate the use of dynamic imports).
- Include a configuration file (config) that contains the corresponding data to connect to the related databases or means of persistence.

Optional:
Do the same for relational databases: MariaDB/SQLite3.

