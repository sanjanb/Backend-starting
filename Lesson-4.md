# Lesson 4: Securing Your Backend with Authentication and Authorization

Welcome to Lesson 4 of the Complete Backend Course! In this lesson, we'll dive into securing your backend API by implementing user authentication and authorization using JSON Web Tokens (JWTs) and middleware. Let's get started!

## Understanding JWTs

JSON Web Tokens (JWTs) are a compact, URL-safe means of representing claims to be transferred between two parties. They are commonly used for authentication and authorization in web applications.

### Structure of a JWT

A JWT consists of three parts:

1. **Header:** Contains metadata about the token, such as the signing algorithm.
2. **Payload:** Contains the claims (e.g., user ID, expiration date).
3. **Signature:** Ensures the token hasn't been tampered with.

## Implementing User Registration

To register new users, follow these steps:

1. **Extract User Data:** Extract the email and password from the request body.
2. **Hash the Password:** Use a library like `bcrypt` to hash the password before storing it in the database.
3. **Store User Data:** Save the user's email and hashed password in the database.
4. **Generate JWT:** Create a JWT containing the user's ID and an expiration date.
5. **Return JWT:** Send the JWT back to the client in the response.

```javascript
const bcrypt = require('bcrypt');
const jwt = require('jsonwebtoken');

// Example registration route
app.post('/register', async (req, res) => {
  const { email, password } = req.body;
  const hashedPassword = await bcrypt.hash(password, 10);

  // Save user to database
  const user = await saveUserToDatabase(email, hashedPassword);

  const token = jwt.sign({ userId: user.id }, 'your_jwt_secret', { expiresIn: '1h' });
  res.json({ token });
});
```

## Implementing Signin Functionality

To authenticate existing users, follow these steps:

1. **Extract Credentials:** Extract the email and password from the request body.
2. **Verify User Existence:** Check if a user with the provided email exists in the database.
3. **Compare Passwords:** Use `bcrypt.compare` to verify the provided password against the stored hashed password.
4. **Generate JWT:** Upon successful validation, generate a new JWT.
5. **Return JWT:** Send the JWT back to the client in the response.

```javascript
// Example signin route
app.post('/signin', async (req, res) => {
  const { email, password } = req.body;
  const user = await getUserByEmail(email);

  if (user && await bcrypt.compare(password, user.password)) {
    const token = jwt.sign({ userId: user.id }, 'your_jwt_secret', { expiresIn: '1h' });
    res.json({ token });
  } else {
    res.status(401).json({ error: 'Invalid credentials' });
  }
});
```

## Implementing Authorization Middleware

To protect certain API endpoints, create an authorization middleware:

1. **Check for JWT:** Look for a JWT in the request headers (typically in the `Authorization` header as a Bearer token).
2. **Extract and Verify JWT:** Extract the JWT and verify its authenticity using the JWT secret key.
3. **Decode JWT:** Retrieve the user's ID from the JWT.
4. **Fetch User:** Get the user from the database using the ID.
5. **Attach User to Request:** Attach the user object to the request for subsequent route handlers.
6. **Handle Errors:** Return a 401 Unauthorized error if the token is invalid or missing.

```javascript
// Example authorization middleware
const authMiddleware = (req, res, next) => {
  const token = req.headers.authorization?.split(' ')[1];

  if (token) {
    jwt.verify(token, 'your_jwt_secret', async (err, decoded) => {
      if (err) {
        return res.status(401).json({ error: 'Invalid token' });
      }

      const user = await getUserById(decoded.userId);
      req.user = user;
      next();
    });
  } else {
    res.status(401).json({ error: 'Token missing' });
  }
};
```

## Protecting Routes

Apply the authorization middleware to specific routes to ensure only authenticated users can access them.

```javascript
// Example protected route
app.get('/protected', authMiddleware, (req, res) => {
  res.json({ message: 'This is a protected route', user: req.user });
});
```

## Conclusion

In this lesson, we've covered how to secure your backend API using JWTs for authentication and authorization. We've implemented user registration, signin functionality, and created middleware to protect routes. Stay tuned for the next lesson, where we'll explore more advanced backend concepts!

Happy coding! 🚀
