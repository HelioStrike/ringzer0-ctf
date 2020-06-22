# SQL Injection

## 	Most basic SQLi pattern.

- Entering `admin' or '1'='1` gets us in.

## Random Login Form

- I entered the default `admin' or '1'='1` username in the register form, with an empty password. This, oddly enough, created a user with the name `admin' or '1'='1`!
- But entering the same data in the login form doesn't work, i.e, the username was not being escaped or, some characters are being filtered.
- I played around with the second idea, by trying to register and then login with ' admin ', and that gives us the flag.

## Po po po po postgresql

- Entering `admin' or '1'='1` gives us `Illegal characters detected.`.
- We reiterate using `admin' or '1'<>'2`
- This gives an error displaying most of the query string: `ERROR: invalid input syntax for type boolean: "admin" LINE 1: SELECT * FROM users WHERE (username = ('admin' or '1'<>'2') ... ^`.
- `admin') or ('1'<>'2` finishes the job!

## Login portal 1

- Entering `admin' or '1'='1` gives us `Illegal characters detected.`.
- Trying again with `admin' or '1'<>'2` gets us in.

## ACL rulezzz the world.

- Clicking the 'List' button sends a post request to the server, and retrieves details about the selected option.
- I captured the request using Burpsuite to see the field: `username=admin`.
- Changing this to the magical `admin' or '1'='1` gives us the entire table, containing the flag.
- You can also change the HTML to reflect this instead of using Burpsuite.