# DB

This folder contains the connection information the databases used by the application.

## Postgres.js

> Postgres connection setup

```javascript
const postgresClient = new Pool({
    connectionString: 'postgres://iudbbwehqhqsyb:eb217e6cd20552874c2fdf6ed6119c86daff30abd785131dcb2ddd6f7829eab9@ec2-54-204-26-236.compute-1.amazonaws.com:5432/dec3qk81t9ofb2', 
    ssl: { rejectUnauthorized: false },
    max: 20
});
```

This file creates the connection information for our Heroku Postgres database so that we can access it from our application. 

Due to a lack of a SSL certificate, ssl had to be disabled on the Heroku server. In real production, this value would need to be changed in order to make the connection secure from man in the middle attacks.

Max connections is set to 20 as this is the limit for the free Heroku Postgres database.

### Users Table

ID (pk) | Email | Password | Role (fk)
--------|-------|----------|----------
UUID | VARCHAR | VARCHAR | Int 

<aside class="notice">
UUID is the primary key which is generated by Postgres. Passwords are stored as an encrypted hash using the bcrypt library and the role column is a foreign key which references the primary key of the roles table
</aside>

### Roles Table

ID (pk)| Role
-------|-----|
Int | VARCHAR

<aside class="notice">
Currently, this only contains the roles of ADMIN and USER.
</aside>

## Redis.js

> Redis connection setup

```javascript
var redisClient = require('redis').createClient('redis://h:p343f46b6946ec0516ef9ace243e856e99223c708ff817633212d183ae46674f6@ec2-3-211-169-9.compute-1.amazonaws.com:25329');
```

This file creates the connection information for our Heroku Redis database so that we can access it from our application.

There is no setup for this database as everything is handled by the express-session library when this is designated as a session store in the [session.js](#session-js) file