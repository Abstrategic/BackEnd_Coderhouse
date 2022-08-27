# Challenge 12

## Log-in by form and persistence of session data

### Instructions

- Continuing with the challenge of the previous class, we are going to incorporate a simple mechanism that allows a client to log in by name, through an entry form.
- After the user is logged in, a banner with the message "Welcome" and the user name will be displayed on the content of the site. This banner will have a log out button to its right.
- Verify that the client remains logged in when the page is restarted, as long as the inactivity time of one minute does not expire, which will be reloaded with each request. If that time is reached, the next user request will take us to the login form.
- When logging out, a view will be shown with the message 'See you later' plus the name and it will automatically return, after two seconds, to the user login view.

The delivered solution will need to persist user sessions in Mongo Atlas.

- Verify that on server restarts, active client sessions are not lost.
- Through the Mongo Atlas web client, review the session id corresponding to each client and their data.
- Delete a client session in the base and check that in the next request the user is presented with the login view.
- Set a session expiration time of 10 minutes rechargeable with each client visit to the site and verify that if this time of inactivity passes, the client is logged out.