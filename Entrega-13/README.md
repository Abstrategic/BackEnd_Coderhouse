# Challenge 13

## Login with Facebook

### Instructions

Implement on the deliverable that we have been carrying out an authentication mechanism. For it:
- A registration view will be included, where email and password are requested. This data will be persisted using MongoDb, in a (new) user collection, taking care that the password is encrypted (hint: use the bcrypt library).
- A login view, where email and password are requested, and that performs server-side authentication through a local passport strategy.
- Each of the views (login - register) must have a button to be redirected to the other.
- Once the user is logged in, he will be redirected to the beginning, which will now also show his email, and a button to unhook.
- In addition, a session space controlled by the passport session will be activated. This will be active for 10 minutes and in each access this time will be recharged.
- Add also error views for login (invalid credentials) and registration (user already registered).
- The rest of the functions must remain as they were in the original project.


