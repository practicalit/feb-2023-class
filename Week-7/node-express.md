# Node and Server Side Programing

Node.js is a runtime environment that lets you run JavaScript code on the server side, rather than in a web browser.

What is Server Side?

"Server-side" refers to operations that are performed by the server in a client-server relationship in computer networking

In simpler terms:

1. **Client**: This is typically your computer or mobile device. When you open a web browser and visit a website, you're acting as a client. The browser sends requests to a server to fetch and display web pages for you.
2. **Server**: This is a computer or system that hosts websites, applications, or data. It waits for requests from clients, processes them, and then sends back the appropriate response.

So, when we say "server-side," we're talking about the processes and operations that take place on the server rather than on the client's device. For example, when you log into an online account, your password verification likely happens server-side to ensure security.

In the context of web development:

- **Server-side programming** involves creating scripts that run on a web server and handle tasks like database queries, form submissions, or user authentication.
- **Client-side programming** is about creating scripts that run in the user's web browser, handling tasks like animations, form validation before submission, or interactive elements on a page.

What is RESTAPI?

A REST API (Representational State Transfer Application Programming Interface) is a set of rules and conventions for building and interacting with web services. REST is an architectural style, not a strict standard, but when used in the context of web services, it typically implies the following principles:

1. **Statelessness**: Each request from a client to a server must contain all the information needed to understand and process the request. The server should not retain any client state between requests. Any required state should be held on the client.
2. **Client-Server Architecture**: The client and the server should be separate and able to evolve independently. The client is responsible for the user interface and user experience, while the server is responsible for processing data and managing resources.
3. **Cacheability**: Responses from the server can be labeled as cacheable or non-cacheable. Cacheable resources can be reused, which improves performance and reduces server load.
4. **Uniform Interface**: One of the key aspects of REST. It simplifies and decouples the architecture, allowing each part to evolve separately. Key constraints for a uniform interface include:
   - **Resource-Based**: Resources (like users, products, or articles) are identified by URIs (typically URLs).
   - **Stateless Interactions**: As mentioned above.
   - **Use of Standard Methods**: Typically, HTTP methods like GET (retrieve), POST (create), PUT (update), DELETE (remove), etc.
   - **Self-descriptive messages**: Messages include enough information to describe how to process the message.
5. **Layered System**: This principle allows for an architecture to be composed of multiple layers, with each layer having a specific functionality. Clients don't necessarily know what layer they're interacting with, providing scalability and modularity.
6. **Code on Demand (optional)**: This allows the server to extend the functionality of a client by sending executable code to the client.

In practice, when someone says "REST API," they're typically referring to a web service that adheres to these principles and uses standard HTTP methods to perform CRUD (Create, Read, Update, Delete) operations on resources. For example, you might have a REST API for a book store where you can retrieve a list of books, add a new book, update the details of a book, or delete a book.

In the context of the discussion about REST, an API stands for "Application Programming Interface." At a high level, an API is a set of rules and protocols that allow one piece of software or program to interact with another. It defines the methods and data formats that software components should use to request and exchange information.

In the context of web services, such as a REST API, this typically means:

1. **Endpoints**: These are specific URIs (usually URLs) where the API can be accessed. For instance, in a book store API, there might be an endpoint like **`https://api.example.com/books`** to retrieve a list of books.
2. **HTTP Methods**: The type of operation you want to perform on the data. Common methods include GET (retrieve data), POST (submit data), PUT (update data), and DELETE (remove data).
3. **Data Formats**: APIs usually communicate using standard data formats. JSON (JavaScript Object Notation) and XML (Extensible Markup Language) are the most common formats for web-based APIs.
4. **Response Codes**: Standard HTTP response codes like **`200 OK`** for successful operations, **`404 Not Found`** for resources that can't be found, **`500 Internal Server Error`** for server errors, and many others.
5. **Authentication & Authorization**: Many APIs require some form of authentication, often using tokens, API keys, or more complex methods like OAuth, to ensure that the person or system making the request has the right to access or modify the data.

In essence, an API in this context provides a way for software systems to communicate with each other over the internet, allowing them to share data and functionality in a standardized way.
