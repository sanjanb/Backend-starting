# Lesson 3: Building Blocks of Backend Development

Welcome to Lesson 3 of the Complete Backend Course! In this lesson, we'll explore the essential building blocks for creating the backend of an application, focusing on backend languages, frameworks, and databases. Let's dive in!

## Backend Languages and Frameworks

To build APIs, you need a backend language. Several popular options include:

- **Python**
- **Ruby**
- **Java**
- **JavaScript**

### JavaScript Runtimes

JavaScript runtimes like **Node.js**, **Bun**, and **Deno** allow you to execute JavaScript code on the server side. In this course, we'll focus on **Node.js** due to its popularity and robust ecosystem.

### Writing a Simple Node.js Server

Writing a Node.js server from scratch can be complex. Here's a brief demonstration:

```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(3000, '127.0.0.1', () => {
  console.log('Server running at http://127.0.0.1:3000/');
});
```

### Backend Frameworks

Backend frameworks provide a structured foundation, handling repetitive tasks like routing, middleware, and error handling. Some popular frameworks include:

- **Express.js** (JavaScript)
- **Hono** (JavaScript)
- **NestJS** (JavaScript)
- **Django** (Python)
- **Ruby on Rails** (Ruby)
- **Spring** (Java)

In this course, we'll use **Express.js**, the most popular JavaScript framework, to build our backend.

## Databases

Managing data is a critical aspect of backend development. Storing data directly on the server is inefficient and doesn't scale. Therefore, every backend relies on dedicated storage solutions known as databases.

### Types of Databases

- **Relational Databases:** Store data in tables with predefined relationships (e.g., MySQL, PostgreSQL).
- **NoSQL Databases:** Offer flexible schemas and are designed for specific data models (e.g., MongoDB, Cassandra).

### Connecting Databases with APIs

Databases connect with APIs to manage data efficiently. In upcoming lessons, we'll explore how to set up a database, connect it to our Express.js application, and perform CRUD (Create, Read, Update, Delete) operations.

## Conclusion

In this lesson, we've introduced the core technologies required to build the server-side logic and manage data for a web application. We've discussed backend languages, frameworks, and the importance of databases. Stay tuned for the next lesson, where we'll start implementing these concepts!

Happy coding! 🚀
