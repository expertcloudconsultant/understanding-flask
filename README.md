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
