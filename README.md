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


To add a final route that performs a function and dynamically displays its result in an HTML file, you can create a route that generates random numbers and pass those numbers to an HTML template. Here's how you can do that:

1. Update your Flask application with a new route and a function that generates random numbers:

```python
from flask import Flask, render_template
import random

app = Flask(__name__)

# ... Routes for Home, About, and Contact ...

# Route 4: Generate Random Numbers
@app.route('/random_numbers')
def generate_random_numbers():
    # Generate three random numbers
    random_numbers = [random.randint(1, 100) for _ in range(3)]
    return render_template('random_numbers.html', numbers=random_numbers)

if __name__ == '__main__':
    app.run(debug=True)
```

In this code:

- We import the `random` module to generate random numbers.
- The `generate_random_numbers` function generates three random numbers between 1 and 100 and passes them as a list called `numbers` to the 'random_numbers.html' template.

2. Create a new HTML template named `random_numbers.html` in the "templates" folder:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Random Numbers</title>
</head>
<body>
    <h1>Random Numbers</h1>
    <p>Here are three random numbers:</p>
    <ul>
        {% for number in numbers %}
        <li>{{ number }}</li>
        {% endfor %}
    </ul>
</body>
</html>
```

In this template:

- We use template tags `{% ... %}` to loop through the `numbers` list and display each random number in an HTML list (`<ul>`).

3. Now, when you access the URL `http://localhost:5000/random_numbers`, Flask will execute the `generate_random_numbers` function, generate three random numbers, and pass them to the 'random_numbers.html' template. The template will display these numbers dynamically.

When you visit `http://localhost:5000/random_numbers` in your browser, you'll see a page with the title "Random Numbers" and three randomly generated numbers displayed in a list.

This example demonstrates how to create a route that performs a function and dynamically displays its result in an HTML file, allowing you to integrate dynamic data into your web application.


To make the random numbers update live without having to manually refresh the browser, you can use JavaScript and AJAX to periodically fetch updated numbers from the server and update the HTML content dynamically. Here's how you can modify your Flask application and HTML template to achieve this:

1. Update the Flask route to return JSON data instead of rendering an HTML template:

```python
from flask import Flask, render_template, jsonify
import random

app = Flask(__name__)

# ... Routes for Home, About, and Contact ...

# Route 4: Generate Random Numbers (JSON)
@app.route('/random_numbers')
def generate_random_numbers():
    # Generate three random numbers
    random_numbers = [random.randint(1, 100) for _ in range(3)]
    return jsonify(numbers=random_numbers)

if __name__ == '__main__':
    app.run(debug=True)
```

In this updated code, the `generate_random_numbers` function returns JSON data containing the randomly generated numbers.

2. Modify the 'random_numbers.html' template to display the numbers and include JavaScript to update them dynamically:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Random Numbers</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>
        function updateRandomNumbers() {
            $.get('/random_numbers', function(data) {
                var numbers = data.numbers;
                var numbersList = '<ul>';
                for (var i = 0; i < numbers.length; i++) {
                    numbersList += '<li>' + numbers[i] + '</li>';
                }
                numbersList += '</ul>';
                $('#randomNumbers').html(numbersList);
            });
        }

        // Update the random numbers every 3 seconds (3000 milliseconds)
        setInterval(updateRandomNumbers, 3000);
    </script>
</head>
<body>
    <h1>Random Numbers</h1>
    <p>Here are three random numbers:</p>
    <div id="randomNumbers"></div>
</body>
</html>
```

In this updated template:

- We include the jQuery library for making AJAX requests.
- The `updateRandomNumbers` JavaScript function makes an AJAX GET request to the `/random_numbers` route to fetch the updated random numbers and dynamically updates the content on the page.
- We use the `setInterval` function to call `updateRandomNumbers` every 3 seconds, ensuring that the numbers are updated periodically without needing a manual refresh.

Now, when you visit `http://localhost:5000/random_numbers` in your browser, you'll see the random numbers automatically updating every 3 seconds without the need for manual page refresh.
