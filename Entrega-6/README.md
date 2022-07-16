# Challenge 6
##websockets

### Instructions

1) Modify the last deliverable so that it has a websocket channel that allows to represent, below the entry form, a table with the list of products in real time.
   
   - There can be several clients connected simultaneously and in each one of them the changes made in the products will be reflected without having to reload the view.
   - When a client connects, he will receive the list of products to represent in the view.

**Aspects to include in the deliverable:**

To build the dynamic table with the data received by websocket, use Handlebars in the frontend. Consider using public files to hold the empty template, and fetch it using the fetch( ) function. Remember that fetch returns a promise.

2) We will add to the project a chat channel between the clients and the server.

   - At the bottom of the entry form, the message center stored on the server will appear, where the messages of all the users identified by their email will appear.
   - The format to be represented will be: email (bold text in blue) [date and time (DD/MM/YYYY HH:MM:SS)] (normal text in brown) : message (italic text in green)
   - Also incorporate two input elements: one for the user to enter their email (mandatory to be able to use the chat) and another to enter messages and send them using a button.
   - Messages must persist on the server in a file (see second deliverable).
