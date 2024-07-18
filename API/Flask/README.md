# Flask tutorial

<p align="center">
  <img src="Images/flask.png" width="400"/>
</p>

## Table of Contents

- [Installation](#installation)
- [Introduction](#introduction)
- [Section One: basics](#section-one-basics)
- [Section Two: URL](#section-two-url)
- [Section Three: HTML Interface](#section-three-html-interface)

## Installation

Run the following command to install `flask` in your environment:

```bash
pip install flask
```

## Introduction

### What is API?

An API, or Application Programming Interface, is a set of rules and tools that allows different software applications
to communicate and interact with each other.

Here are different types of APIs commonly used in software development:

- RESTful APIs: Utilizes HTTP methods to perform operations on resources, widely used for web services due to its
  flexibility and scalability.

- SOAP APIs (Simple Object Access Protocol): Implements a protocol-based approach using XML for message format,
  providing built-in security and transaction support in enterprise systems.

- GraphQL APIs: Allows clients to specify the structure of the response they need, providing a single endpoint for
  efficient data fetching in modern applications.

- RPC APIs (Remote Procedure Call): Facilitates communication between distributed systems by invoking procedures or
  functions across different processes or computers.

- WebSocket APIs: Enables real-time interactive communication between client and server over a single TCP connection,
  suitable for applications requiring frequent data exchange.

- Library-Based APIs: Provides functionalities and methods within a programming language or framework, enhancing
  developer productivity by integrating specific features or services directly into applications.

<p align="center">
  <img src="Images/restapi.png" width="600"/>
</p>

### Rest API

* `HTTP (Hypertext Transfer Protocol)`: is a system used on the internet to send and receive information between a web
  browser and a server.

* `Request`: In a REST API, a request is an HTTP message sent by a client to the server, asking for a specific
  operation such as create, retrieve, update, or delete (`CRUD`) a resource.

In a REST API, a typical HTTP request consists of several key parts:

1. HTTP Method: Specifies the action to be performed on the resource. Common methods include:

    - GET: to get data from a resource.
    - POST: to create a data at a resource.
    - PUT: to update a data at a resource.
    - DELETE: to delete a data at a resource.
    - PATCH: to partially update a data at a resource.
    - HEAD: to get data from a resource without the body.
    - OPTIONS: to describe the communication options for a resource.

2. Resource URL: Defines the location of the resource on the server.
3. Headers: Provide additional information about the request and its content. Common headers include:

    - Content-Type: Specifies the media type of the request body (e.g., application/json).
    - Authorization: Contains credentials for authenticating the client with the server.
    - Accept: Specifies the expected media types that the client can understand in the response.

4. Body: Contains data sent to the server for operations like creating or updating a resource.

For instance, a POST request to create a new user might look like this:

```bash
POST /api/users
Content-Type: application/json
Authorization: Bearer <access_token>

{
  "username": "john_doe",
  "email": "john.doe@example.com",
  "password": "secret123"
}
```

* `Response`: In a REST API, a response is an HTTP message sent by the server back to the client, providing the result
  of the requested operation, including any requested data or status information.

    - 200 OK
    - 201 Created
    - 204 No Content
    - 400 Bad Request
    - 401 Unauthorized
    - 403 Forbidden
    - 404 Not Found
    - 500 Internal Server Error

* `Resource`: refers to any identifiable entity that can be accessed and manipulated over the internet. It can represent
  both physical entities (such as a file or an image) and abstract concepts (such as a user profile or a blog post).
  Each resource is typically identified by a unique URL (Uniform Resource Locator) and is accessed using standard HTTP
  methods. For example:

    - User Profile: /users/{user_id}
    - Blog Post: /posts/{post_id}
    - Product Listing: /products/{product_id}
    - File or Image: /files/{file_id}
    - Order Transaction: /orders/{order_id}
    - Comment or Review: /posts/{post_id}/comments/{comment_id}
    - API Endpoint: /api/{endpoint_name}

### Flask

Flask is a lightweight and flexible web framework for Python that provides tools, libraries, and patterns to build web
applications. It is designed to be simple and easy to use, allowing developers to create web applications quickly and
efficiently. Flask is based on the WSGI (Web Server Gateway Interface) toolkit and Jinja2 template engine, and it
supports various HTTP methods and extensions, making it suitable for developing RESTful APIs, websites, and more complex
web applications.

Flask acts as the intermediary layer that handles the communication between the frontend (e.g. HTML) and the backend (
e.g. database, ML core, etc.).

## Section One: Basics

### Overview

Here you can see an overview of how to create a flask API `without an HTML interface`:

```python
from flask import Flask

app = Flask(__name__)


@app.route('/')
def hello_world():
    return 'Hello World'


if __name__ == '__main__':
    app.run()
```

* `from flask import Flask`: Importing flask module in the project is mandatory.
* `app = Flask(__name__)`: initializes a new Flask web application, using the current module's name to set up the
  application's configuration and resource paths.

* `Note`: In Python, `__name__` is a special variable that indicates whether a module is being run as the main program
  or being imported into another module. If the module is run directly, `__name__` is set to `__main__`, allowing
  specific code to execute only in this context. If the module is imported, `__name__` is set to the module’s name,
  preventing that code from running. This helps manage script behavior based on how the module is used.

* `@app.route('/')`: This decorator tells Flask to execute the following function when the root URL ('/') of the web
  application is accessed. In other words, it sets up a route for the homepage of the application.
* `app.run()`: starts the Flask development server, allowing you to test and develop your web application by handling
  incoming requests and serving responses.

### Routing

The route() function of the Flask class is a decorator, which tells the application which URL should call the associated
function.

```python
app.route(rule, **options)
```

* The rule parameter represents URL binding with the function.

* The options is a list of parameters to be forwarded to the underlying Rule object. Common Options:

    - methods: Specifies the HTTP methods (e.g., GET, POST) that the route should accept.
  ```python
  @app.route('/submit', methods=['GET', 'POST'])
  ```
    - endpoint: Explicitly sets the endpoint name for the route, which can be used for URL generation.
  ```python
  @app.route('/hello', endpoint='hello_endpoint')
  ```
    - strict_slashes:
  ```python
  @app.route('/hello/', strict_slashes=False)
  ```

* `HTTP methods`: a set of request methods used by web browsers and servers to communicate over the HTTP.

* `endpoint`: The endpoint parameter assigns a unique name to the route, which can be used to reference the route
  internally for URL generation and other purposes.

* `strict_slashes`: controls whether Flask routes should strictly differentiate between URLs with and without a trailing
  slash.

* `Note`: The add_url_rule() function of an application object is also available to bind a URL with a function.

```python
def hello_world():
    return 'hello world'


app.add_url_rule('/', 'hello', hello_world)
```

### Running

run() method of Flask class runs the application on the local development server.

```python
app.run(host, port, debug)
```

* `host`: The hostname or IP address where the server should listen for requests.

    - Default: '127.0.0.1' (localhost), meaning the server is only accessible from the same machine.
    - Example: host='0.0.0.0' to make the server accessible externally.

* `port`: The port number where the server should listen for requests.

    - Default: 5000.
    - Example: port=8000 to run the server on port 8000.

* `debug`: Enables or disables debug mode.

    - Default: False.
    - Example: When True, provides detailed error messages and auto-reloads the server on code changes, useful during
      development.

### Debugging

A Flask application is started by calling the run() method. However, while the application is under development, it
should be restarted manually for each change in the code. To avoid this inconvenience, enable debug support. The server
will then reload itself if the code changes. It will also provide a useful debugger to track the errors if any, in the
application.

```python
app.debug = True
app.run()
app.run(debug=True)
```

## Section Two: URL

### Variable Rules

Variable rules in Flask allow the creation of dynamic and flexible URLs by marking variable parts with angle brackets.

Examples:

```python
@app.route('/hello/<name>')
def hello(name):
    return f"Hello {name}"
```

`http://localhost:5000/hello/TutorialsPoint` => `Hello TutorialsPoint`

```python
@app.route('/blog/<int:postID>')
def show_blog(postID):
    return f"Blog Number: {postID}"
```

`http://localhost:5000/blog/11` => `Blog Number: 11`

```python
@app.route('/rev/<float:revNo>')
def revision(revNo):
    return f"Revision Number: {revNo}"
```

`http://localhost:5000/rev/1.1` => `Revision Number: 1.100000`

### URL Building

The `url_for()` function in Flask is used to generate URLs dynamically based on the view function names and their
arguments.

```python
from flask import Flask, redirect, url_for

app = Flask(__name__)


@app.route('/admin')
def hello_admin():
    return 'Hello Admin'


@app.route('/guest/<guest>')
def hello_guest(guest):
    return f"Hello {guest} as Guest"


@app.route('/user/<name>')
def hello_user(name):
    if name == 'admin':
        return redirect(url_for('hello_admin'))
    else:
        return redirect(url_for('hello_guest', guest=name))


if __name__ == '__main__':
    app.run(debug=True)
```

* `url_for`: generates a URL by calling a function.
* `redirect`: is used to redirect users to a different route or URL.

## Section Three: HTML Interface

### HTTP methods

Now, we want to create an HTML file that has an input box and an interface. This makes us able to implement GET and POST
methods:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Login</title>
</head>
<body>
<h2>Login Form</h2>
<form action="/login" method="post">
    <label for="name">Username:</label>
    <input type="text" id="name" name="nm">
    <input type="submit" value="Login">
</form>
</body>
</html>
```

As you can see this interface is located in the `/login` URL by action, and the considered method is `POST`. So, we have
to define a function that is responsible for this URL and also has the POST method in addition to GET.

```python
from flask import Flask, redirect, url_for, request

app = Flask(__name__)


@app.route('/success/<name>')
def success(name):
    return f"welcome {name}"


@app.route('/login', methods=['POST', 'GET'])
def login():
    if request.method == 'POST':
        user = request.form['nm']
        return redirect(url_for('success', name=user))
    elif request.method == 'GET':
        user = request.args.get('nm')
        return redirect(url_for('success', name=user))


if __name__ == '__main__':
    app.run(debug=True)
```

Here, we created a function that handles the /login URL. Since our method in the HTML file is POST, we just get the
entered name and redirect to another URL that says welcome to that name. But if we specified the name previously, we can
change the method to GET in order to get the name from our arguments and pass it to the welcome page.

### Templates folder

By running `render_template('your_file.html', variable = Value)` Flask will try to find the your_file.html in
the `templates/` folder and pass the value to the defined variable in that file.

The jinja2 template engine uses the following delimiters for escaping from HTML and running python syntax in an HTML
file:

```html
{{ variable_name }}


{# This is a comment #}


{% if user %}
<h1>Hello, {{ user.username }}!</h1>
{% else %}
<h1>Hello, Guest!</h1>
{% endif %}


{% for item in items %}
<li>{{ item }}</li>
{% endfor %}
```

For example, assume that this is the structure of your project:

```text
Project_folder
├── main.py
└── templates
    └── result.html
```

And these are our main Python and HTML files:

Python:

```python
from flask import Flask, render_template

app = Flask(__name__)


@app.route('/result')
def result():
    dict = {'phy': 50, 'che': 60, 'maths': 70}
    return render_template('result.html', result=dict)


if __name__ == '__main__':
    app.run(debug=True)
```

HTML:

```html
<!doctype html>
<html>
<body>
<table border=1>
    {% for key, value in result.items() %}
    <tr>
        <th> {{ key }}</th>
        <td> {{ value }}</td>
    </tr>
    {% endfor %}
</table>
</body>
</html>
```

### Static folder

In web development, a static folder is a directory where you store static files such as JavaScript (.js) and Cascading
Style Sheets (.css). These files are used to enhance the functionality and styling of your web application.

For example, assume that this is the structure of your project:

```text
Project_folder
├── main.py
└── templates
│   └── index.html
└── static
    └── hello.js
```

And these are our main Python, HTML, and JavaScript files:

Python:

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route("/")
def index():
   return render_template("index.html")

if __name__ == '__main__':
   app.run(debug = True)
```

HTML:

```html
<html>
   <head>
      <script type = "text/javascript" 
         src = "{{ url_for('static', filename = 'hello.js') }}" ></script>
   </head>
   
   <body>
      <input type = "button" onclick = "sayHello()" value = "Say Hello" />
   </body>
</html>
```

JavaScript:

```javascript
function sayHello() {
   alert("Hello World")
}
```

## Sources

```text
www.tutorialspoint.com
www.freecodecamp.org
www.altexsoft.com
bytebytego.com
```