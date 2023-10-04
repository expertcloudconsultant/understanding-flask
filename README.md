# understanding-flask
Helpful guide to understanding flask


Here's a minimal Flask application with three routes that a technology student can use to understand the basics of routing in Flask. In this example, we'll create routes for a technology-themed website with pages for "Home," "About," and "Contact."

```python
from flask import Flask

app = Flask(__name__)

# Route 1: Home Page
@app.route('/')
def home():
    return "Welcome to the Technology Student's Home Page!"

# Route 2: About Page
@app.route('/about')
def about():
    return "Learn about our technology courses and programs."

# Route 3: Contact Page
@app.route('/contact')
def contact():
    return "Contact us for more information and assistance."

if __name__ == '__main__':
    app.run(debug=True)
```

In this Flask application:

- The root URL `'/'` (e.g., `http://localhost:5000/`) is associated with the `home` function, which displays a welcome message for the technology student on the home page.

- The URL `'/about'` (e.g., `http://localhost:5000/about`) is associated with the `about` function, which provides information about technology courses and programs.

- The URL `'/contact'` (e.g., `http://localhost:5000/contact`) is associated with the `contact` function, which offers contact information for further inquiries.

You can run this Flask application, and when you visit the specified URLs in your web browser or use an API client like Postman, you'll see the corresponding messages displayed in your browser or received as responses.

This minimal example should help a technology student understand the concept of routing in Flask and how different routes can lead to different views or pages in a web application.



**To have different routes in your Flask application render different HTML pages, you'll need to use the `render_template` function provided by Flask. This function allows you to render HTML templates and pass data to those templates. Here's an expanded version of the Flask application with three routes, each rendering a different HTML page:**

1. First, make sure you have a folder named "templates" in your project directory. This is where Flask expects to find your HTML templates.

2. Create three HTML templates: `home.html`, `about.html`, and `contact.html` in the "templates" folder. These templates will be rendered for the respective routes.

Here's the updated Flask application:

```python
from flask import Flask, render_template

app = Flask(__name__)

# Route 1: Home Page
@app.route('/')
def home():
    return render_template('home.html')

# Route 2: About Page
@app.route('/about')
def about():
    return render_template('about.html')

# Route 3: Contact Page
@app.route('/contact')
def contact():
    return render_template('contact.html')

if __name__ == '__main__':
    app.run(debug=True)
```

Now, you need to create the HTML templates (`home.html`, `about.html`, and `contact.html`) in the "templates" folder with the content you want to display on each page. For example:

`home.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Home Page</title>
</head>
<body>
    <h1>Welcome to the Technology Student's Home Page!</h1>
</body>
</html>
```

`about.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>About Us</title>
</head>
<body>
    <h1>About Us</h1>
    <p>Learn about our technology courses and programs.</p>
</body>
</html>
```

`contact.html`:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Contact Us</title>
</head>
<body>
    <h1>Contact Us</h1>
    <p>Contact us for more information and assistance.</p>
</body>
</html>
```

With this setup, when you access the following URLs in your browser:

- `http://localhost:5000/` (Root URL), you'll see the "Home Page" HTML template.
- `http://localhost:5000/about`, you'll see the "About Us" HTML template.
- `http://localhost:5000/contact`, you'll see the "Contact Us" HTML template.

This expanded example demonstrates how to use Flask to route to different HTML pages based on the requested URL, providing a more complete web application structure.
