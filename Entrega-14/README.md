# Challenge 14

## Using the Process object

### Setpoints

On top of the project from the last challenge deliverable, move all the keys and credentials used to an .env file, and load it using the dotenv library.

The only configuration that is not going to be handled with this library is going to be the listening port of the server. This should be read from the arguments passed on the command line, using some library (minimist or yargs). In the case of not passing this parameter by command line, connect by default to port 8080.

Observation: for the moment you can leave the choice of session and persistence explicit in the code itself. Later we will also make this configuration parameterizable.

Add a route '/info' that presents in a simple view the following data:
- input arguments
- Path of execution
- Platform name (operating system)
-Process id
- version of node.js
- Project folder
- Total reserved memory (rss)

Add another route '/api/randoms' that allows to calculate a number of random numbers in the range 1 to 1000 specified by query parameters.

For example: /randoms?cant=20000.

If such a parameter is not entered, calculate 100,000,000 numbers.

The data returned to the frontend will be an object that will contain as keys the random numbers generated along with the number of times each one came out. This route will not be blocking (use the fork method of child process). Check for non-blocking with a quantity of 500,000,000 randoms.

Remark: use separate routers and apis for this functionality.
