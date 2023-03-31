---
layout: post
title: "Building an API with Firebase Authentication"
categories: "web development"
image: images/firebase.png
excerpt: "Firebase Authentication provides a secure and easy-to-use way to authenticate users and manage user sessions for your API. In this article, we'll cover the basics of building an API with Firebase Authentication."
---


Firebase is a powerful platform for building web and mobile applications, offering a wide range of services such as cloud storage, real-time databases, and user authentication. Firebase Authentication provides a secure and easy-to-use way to authenticate users and manage user sessions for your API. In this article, we'll cover the basics of building an API with Firebase Authentication.

## Prerequisites

Before we get started, you'll need to have the following set up:

- A Firebase project with Firebase Authentication enabled.
- A server-side language and framework, such as Node.js and Express.js.
- The Firebase Admin SDK for your server-side language.

## User Authentication

To allow users to authenticate with your API using Firebase Authentication, you'll need to create two endpoints: one for user registration and another for user login. These endpoints will handle user authentication and will allow your users to securely access your API resources.

### User Registration Endpoint

The registration endpoint typically accepts a new user's email address and password, creates a new user account in Firebase Authentication, and returns a response indicating success or failure. Here's an example of what the endpoint might look like in Node.js using the Firebase Admin SDK:


```javascript
const admin = require('firebase-admin');
const express = require('express');
const bodyParser = require('body-parser');

admin.initializeApp();

const app = express();

app.use(bodyParser.json());

app.post('/register', async (req, res) => {
  try {
    const { email, password } = req.body;
    const userRecord = await admin.auth().createUser({
      email,
      password,
    });
    res.status(201).send(userRecord.toJSON());
  } catch (error) {
    console.error(error);
    res.status(500).send(error);
  }
});

app.listen(3000, () => console.log('API listening on port 3000'));
```

### User Login Endpoint

The login endpoint accepts a user's email and password, verifies the credentials against Firebase Authentication, and returns an access token that the user can use to authenticate subsequent API requests. Here's an example of what the endpoint might look like:

```javascript
app.post('/login', async (req, res) => {
  try {
    const { email, password } = req.body;
    const userRecord = await admin.auth().getUserByEmail(email);
    await admin.auth().signInWithEmailAndPassword(email, password);
    const token = await admin.auth().createCustomToken(userRecord.uid);
    res.status(200).send({ token });
  } catch (error) {
    console.error(error);
    res.status(401).send(error);
  }
});
```

## API Authentication

Once your users are authenticated, you'll need to ensure that only authenticated users can access your API resources. You can use Firebase Authentication middleware to verify the user's authentication state and extract their user ID from the request headers. Here's an example of how you can use the Firebase Authentication middleware in Express.js:

```javascript
const admin = require('firebase-admin');
const express = require('express');
const app = express();

// Initialize Firebase Admin SDK
admin.initializeApp();

// Middleware to verify Firebase ID token and extract user ID
const authenticateUser = async (req, res, next) => {
  const authHeader = req.headers.authorization;
  if (!authHeader || !authHeader.startsWith('Bearer ')) {
    res.status(401).send('Unauthorized');
    return;
  }

  const idToken = authHeader.split('Bearer ')[1];
  try {
    const decodedToken = await admin.auth().verifyIdToken(idToken);
    req.user = decodedToken;
    next();
  } catch (error) {
    console.error(error);
    res.status(401).send('Unauthorized');
  }
};

// Example API endpoint that requires authentication
app.get('/api/protected', authenticateUser, (req, res) => {
  const userId = req.user.uid;
  res.send(`Hello, user ${userId}!`);
});

// Start the server
app.listen(3000, () => {
  console.log('Server listening on port 3000');
});
```

The `authenticateUser` middleware extracts the Firebase ID token from the `Authorization` header of the incoming request, verifies the token using the Firebase Admin SDK, and adds the decoded user ID to the `req.user` object. You can then use `req.user.uid` to retrieve the user's ID and perform further operations.

The `authenticateUser` middleware is then used as middleware in the `app.get('/api/protected', authenticateUser, ...)` endpoint, which requires the user to be authenticated before accessing the endpoint. If the user is not authenticated, the middleware will return a 401 Unauthorized response.

## Conclusion

In this article, we've covered the basics of building an API with Firebase Authentication. We've shown you how to create user registration and login endpoints, and how to use Firebase Authentication middleware to authenticate API requests. By using Firebase Authentication in your API, you can create a secure and reliable user authentication system without having to build it from scratch.

Firebase Authentication also provides support for other authentication providers like Google, Facebook, and Twitter, which makes it easy to add social login capabilities to your API. Additionally, Firebase Authentication provides client SDKs for web and mobile platforms, making it easy to integrate your API with your client-side applications.

If you're building an API with Firebase, we highly recommend using Firebase Authentication to handle user authentication. It's easy to use, secure, and scalable, and can save you a lot of time and effort in building your own authentication system.
