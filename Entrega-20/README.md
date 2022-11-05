# Challenge 20

## Improve the architecture of our API

### Instructions

- Modify the persistence layer incorporating the concepts of Factory and DAO.
- The DAOs must present the same interface towards the business logic of our server.
- The selected DAO (by a command line parameter as we did before) will be returned by a Factory for the business layer to operate with.
- Each of these cases of persistence must be implemented using the singleton pattern that prevents the creation of new instances of these data access mechanisms.
- Check that if I call the factory twice, with the same option chosen, it returns the same instance.
- Implement the Repository pattern for message persistence.
