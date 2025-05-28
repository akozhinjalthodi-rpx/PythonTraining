Date : 09 Aug 2022

------------------

## What is django? 
Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. Built by experienced developers, it takes care of much of the hassle of web development, so you can focus on writing your app without needing to reinvent the wheel. It’s free and open source.
* Django was designed to help developers take applications from concept to completion as quickly as possible.
* Django takes security seriously and helps developers avoid many common security mistakes.
* Some of the busiest sites on the web leverage Django’s ability to quickly and flexibly scale.

## Why Django?
* It’s very easy to switch database in Django framework.
* It has built-in admin interface which makes easy to work with it.
* Django is fully functional framework that requires nothing else.
* It has thousands of additional packages available.
* It is very scalable.

## Installation of Django

Setting up Django involves installing Python, pip (Python's package installer), creating a virtual environment, and then installing Django itself.

**Prerequisites:**
*   **Python:** Ensure you have Python 3.6 or newer installed. You can download it from [python.org](https://www.python.org/downloads/). During installation, make sure to check the box that says "Add Python to PATH" (or similar).
*   **pip:** pip is usually included with Python installations (version 3.4+). You can verify its installation and update it to the latest version using:
    ```bash
    python -m pip install --upgrade pip
    ```

**Steps to Install Django:**

1.  **Create a Project Directory:**
    First, create a folder for your Django project and navigate into it.
    ```bash
    mkdir my_django_project
    cd my_django_project
    ```

2.  **Create and Activate a Virtual Environment:**
    It's a strong best practice to use a virtual environment for each Django project. This isolates your project's dependencies from your global Python installation and other projects. Python's built-in `venv` module is recommended.

    *   **Create the virtual environment (e.g., named `venv`):**
        ```bash
        python -m venv venv
        ```
        This command creates a `venv` folder in your project directory.

    *   **Activate the virtual environment:**
        *   **On Windows (Command Prompt/PowerShell):**
            ```batch
            venv\Scripts\activate
            ```
            (If using PowerShell and you encounter issues, you might need to run `Set-ExecutionPolicy Unrestricted -Scope Process` first, then `venv\Scripts\Activate.ps1`)
        *   **On macOS and Linux (bash/zsh):**
            ```bash
            source venv/bin/activate
            ```
        After activation, your command prompt/terminal prompt will usually change to show the active environment's name (e.g., `(venv) C:\path\to\my_django_project>`).

3.  **Install Django:**
    With the virtual environment active, install Django using pip:
    ```bash
    (venv) pip install django
    ```
    This will install the latest stable version of Django into your active virtual environment. You can also install a specific version: `pip install django==3.2`.

4.  **Create a Django Project:**
    Now, you can create your Django project. The `django-admin startproject` command sets up the basic directory structure and core files for your project.
    *   To create a project named `my_project_name` *inside* your current `my_django_project` directory (recommended to avoid an extra level of nesting if you're already in your main project folder):
        ```bash
        (venv) django-admin startproject my_project_name .
        ```
        (Note the `.` at the end – it tells Django to create the project in the current directory.)
    *   Alternatively, if you want Django to create a new subdirectory for the project:
        ```bash
        # (venv) django-admin startproject my_project_name 
        # This would create my_django_project/my_project_name/my_project_name/manage.py
        ```
    Let's assume you used `django-admin startproject config .` to name your main configuration directory `config`. Your structure would look like:
    ```
    my_django_project/
    ├── venv/
    ├── config/         <-- Your project's configuration directory
    │   ├── __init__.py
    │   ├── asgi.py
    │   ├── settings.py
    │   ├── urls.py
    │   └── wsgi.py
    └── manage.py       <-- Django's command-line utility
    ```

5.  **Run the Development Server:**
    Navigate into your project directory (if you created a subdirectory, e.g., `cd my_project_name`). If you used `.` for `startproject`, you should already be in the directory containing `manage.py`.
    ```bash
    (venv) python manage.py runserver
    ```
    This starts Django's lightweight development server.

6.  **Verify Installation:**
    Open a web browser and go to `http://127.0.0.1:8000/`. You should see the Django welcome page, indicating that your installation was successful.

    To stop the development server, press `Ctrl+C` in your terminal.
    To deactivate the virtual environment when you're done:
    ```bash
    (venv) deactivate
    ```

### Benefits of Django Architecture –
* Rapid Development
* Loosely Coupled
* Ease of Modification

### Drawbacks of MVC Architecture –
* Too much load on Model Component
* Development Complexity is high
* Two components are controlling View
(Note: This section on "Drawbacks of MVC Architecture" might be misleading in a Django context as Django uses MVT, which addresses some of these. Consider re-evaluating if this section is necessary or how it relates specifically to Django's MVT.)


## Django Project MVT Structure
Django is based on MVT (*Model-View-Template*) architecture. MVT is a software design pattern, similar to the more commonly known MVC (Model-View-Controller), for developing web applications. It provides a clear separation of concerns, making projects more organized and maintainable.

**The MVT Structure has the following three parts:**

*   **Model:** The Model acts as the interface for your data. It is responsible for maintaining data, representing the logical data structure behind the entire application. In Django, models are Python classes that map to database tables (generally in relational databases like PostgreSQL, MySQL, SQLite). They handle data storage, retrieval, updating, and validation.

*   **View (Django's View Function/Class):** In Django, the "View" component is responsible for handling a web request and returning a web response. It contains the business logic. When a user navigates to a URL, a Django view function (or class-based view) is executed. This view interacts with models to fetch or save data and then selects an appropriate template to render the data for the user. **Note:** Django's "View" is more akin to the "Controller" in a traditional MVC pattern.

*   **Template:** The Template is responsible for the presentation layer – what the user sees in their browser. It's typically an HTML file mixed with Django Template Language (DTL) syntax. DTL allows you to embed dynamic content (from views) into static HTML.
    *   **Django Template Language (DTL) Syntax:**
        *   `{{ variable }}`: Used to output the value of a variable passed from the view.
        *   `{% tag %}`: Used for control flow (like `{% if %}`, `{% for %}`), loading external template tags, or other template-specific logic.
        *   `{# comment #}`: Used for comments within the template (not rendered in HTML).
        *   Filters: `{{ variable|filter_name }}` can be used to modify variable display (e.g., `{{ name|lower }}`).

The MVT pattern promotes loose coupling, meaning each component can be developed and modified independently with minimal impact on the others.

![MVT Diagram](https://media.geeksforgeeks.org/wp-content/uploads/20210606092225/image.png)
*(Image Source: GeeksforGeeks)*

## Project Structure

When you create a Django project (e.g., using `django-admin startproject myproject .`), it sets up a specific directory structure with several key files. Understanding these files is essential for navigating and developing your Django application.

Assuming your project is named `myproject` and the configuration directory is also `myproject` (created with `django-admin startproject myproject .`):

```
my_django_project/
├── venv/                     # Virtual environment directory (if used)
├── myproject/                # Python package for your project (configuration root)
│   ├── __init__.py           # Makes this directory a Python package
│   ├── asgi.py               # Entry-point for ASGI-compatible web servers (for async features)
│   ├── settings.py           # Project settings and configuration
│   ├── urls.py               # Project-level URL declarations (main URL router)
│   └── wsgi.py               # Entry-point for WSGI-compatible web servers (for sync features)
└── manage.py                 # Django's command-line utility
```

### Key Files and Their Purpose:

*   **Outer `my_django_project/` directory:** This is just a container for your project. You can rename it to anything; it doesn’t affect Django.
*   **`manage.py`:**
    *   A command-line utility that lets you interact with your Django project in various ways.
    *   Common commands include:
        *   `python manage.py runserver`: Starts the development server.
        *   `python manage.py startapp <app_name>`: Creates a new Django application within your project.
        *   `python manage.py makemigrations`: Creates new migration files based on changes to your models.
        *   `python manage.py migrate`: Applies database migrations.
        *   `python manage.py createsuperuser`: Creates an admin user.
        *   `python manage.py collectstatic`: Collects static files for deployment.
    *   To see all available commands: `python manage.py help`

*   **Inner `myproject/` directory (Project Configuration Root):**
    *   This directory is the actual Python package for your project. Its name is the Python package name you’ll use to import anything inside it (e.g., `from myproject.settings import DEBUG`).
    *   **`__init__.py`:** An empty file that tells Python that this directory should be considered a Python package. It can also be used to execute package initialization code or define package-level names.
    *   **`settings.py`:**
        *   Contains all the configuration for your Django project.
        *   Common settings include:
            *   `SECRET_KEY`: A cryptographic key for security purposes (keep it secret!).
            *   `DEBUG`: A boolean that turns on/off debug mode (should be `False` in production).
            *   `ALLOWED_HOSTS`: A list of strings representing the host/domain names that this Django site can serve.
            *   `INSTALLED_APPS`: A list of all Django applications that are activated in this Django instance (includes built-in apps and your own).
            *   `MIDDLEWARE`: A list of middleware classes for processing requests and responses.
            *   `ROOT_URLCONF`: The Python path to your project's main URL configuration module (usually `'myproject.urls'`).
            *   `TEMPLATES`: Configuration for template engines, directories, etc.
            *   `DATABASES`: Dictionary containing database connection settings (e.g., engine, name, user, password).
            *   `AUTH_PASSWORD_VALIDATORS`: Configuration for password strength validation.
            *   `LANGUAGE_CODE`, `TIME_ZONE`: Internationalization settings.
            *   `STATIC_URL`: URL prefix for static files (CSS, JavaScript, Images).
            *   `STATICFILES_DIRS`: List of directories where Django will look for static files in addition to app 'static' subdirectories.
            *   `STATIC_ROOT`: The absolute path to the directory where `collectstatic` will gather all static files for deployment.
            *   `MEDIA_URL`: URL prefix for user-uploaded media files.
            *   `MEDIA_ROOT`: Absolute path to the directory that will hold user-uploaded files.
    *   **`urls.py` (Project-level):**
        *   This is the main URL dispatcher for your project. It's the "table of contents" for your Django-powered site.
        *   It contains a list of `path()` and/or `re_path()` instances (`urlpatterns`) that route URLs to views or to other URL configuration modules (typically from your individual apps).
    *   **`wsgi.py` (Web Server Gateway Interface):**
        *   An entry-point for WSGI-compatible web servers to serve your project (primarily for synchronous Python web applications).
        *   It's used during deployment to integrate Django with a WSGI server like Gunicorn or uWSGI.
    *   **`asgi.py` (Asynchronous Server Gateway Interface):**
        *   An entry-point for ASGI-compatible web servers to serve your project.
        *   This is used if you plan to use Django's asynchronous features (e.g., Django Channels for WebSockets or other long-polling connections).

### Django Apps
A Django project is typically composed of one or more "apps". An app is a web application that does something – e.g., a blog system, a public records database, or a simple poll app. It's good practice to make apps reusable across different projects. Apps are usually created within the project using `python manage.py startapp <app_name>`. Each app will have its own models, views, templates (optional), and URLs.

## MVC Architecture vs. MVT Structure

While Django is often referred to as an MVT (Model-View-Template) framework, it's helpful to understand its relationship with the more traditional MVC (Model-View-Controller) pattern.

*   **MVC (Model-View-Controller):**
    *   **Model:** Manages the data and business logic.
    *   **View:** Handles the presentation of data to the user (the UI).
    *   **Controller:** Receives user input, interacts with the Model, and selects a View to render.

*   **MVT (Model-View-Template) in Django:**
    *   **Model:** Same as in MVC. Django Models handle data interaction, typically with a database.
    *   **Template:** This is what MVC calls the "View." It's the presentation layer (HTML, CSS, JS) that defines how data is displayed, using Django Template Language for dynamic content.
    *   **View (Django View):** This is Django's request handler. It acts like the "Controller" in MVC. It receives an HTTP request, processes it (e.g., interacts with the Model), and then returns an HTTP response, often by rendering a Template with context data.

**Analogy:**

| MVC Component  | Django MVT Component | Role                                                              |
|----------------|----------------------|-------------------------------------------------------------------|
| Model          | Model                | Manages application data and business rules.                      |
| View           | Template             | Handles data presentation and user interface (UI).                |
| Controller     | View (function/class)| Receives requests, processes them, interacts with models, and selects a template for the response. |

So, MVT is essentially Django's specific implementation of an MVC-like pattern. The names are slightly different, but the core idea of separating concerns (data logic, presentation logic, and request handling logic) remains the same.


## How to Create a Basic Project using MVT in Django ?

This article focuses on creating a basic project to render a template using MVT architecture. We will use MVT (Models, Views, Templates) to render data to a local server.

### Create a basic Project: 

* To initiate a project of Django on Your PC, open Terminal and Enter the following command 

```python 
django-admin startproject projectName
```

* A New Folder with the name `projectName` will be created. To enter in the project using the terminal enter command 

```
cd projectName
```
* Create a new file views.py inside the project folder where settings.py, urls.py and other files are stored and save the following code in it- 

```python
# HttpResponse is used to
# pass the information
# back to view
from django.http import HttpResponse

# Defining a function which
# will receive request and
# perform task depending
# upon function definition
def hello_geek (request) :

	# This will return Hello Geeks
	# string as HttpResponse
	return HttpResponse("Hello Geeks")

```

* Open `urls.py` inside project folder (projectName) and add your entry- 
  * Import hello_geek function from views.py file.  
```
from projectName.views import hello_geeks
```

* Add an entry in url field inside url patterns- 

```
path('geek/', hello_geek), 
```
* Now to run the server follow these steps- 
  * Start the server- Start the server by typing following command in cmd- 
``` 
$ python manage.py runserver 127.0.0.1:8080
```
* Checking – Open the browser and type this url-  http://127.0.0.1:8080/geek/

## Django Forms
Django's form handling capabilities simplify many aspects of working with HTML forms. Forms are crucial for collecting user input, and Django provides a robust framework to generate form widgets, validate submitted data, and process it.

### Creating a Simple Form (`django.forms.Form`)
You define a form in Django by creating a class that inherits from `django.forms.Form`. Inside this class, you specify the form fields, each represented as an instance of a Field class (e.g., `CharField`, `EmailField`).

First, you'll typically create a `forms.py` file within your Django app directory (e.g., `myapp/forms.py`).

**Example: `myapp/forms.py`**
```python
from django import forms
import datetime # Import datetime for DateField example

class ContactForm(forms.Form):
    name = forms.CharField(
        max_length=100, 
        label="Your Name",
        required=True,
        help_text="Please enter your full name."
    )
    email = forms.EmailField(
        label="Your Email",
        required=True,
        widget=forms.EmailInput(attrs={'placeholder': 'you@example.com'})
    )
    message = forms.CharField(
        widget=forms.Textarea(attrs={'rows': 4, 'placeholder': 'Your message here...'}), 
        label="Message",
        required=True
    )
    age = forms.IntegerField(
        required=False, 
        label="Your Age (Optional)",
        min_value=0,
        help_text="Enter a valid age if you'd like."
    )
    subscribe_newsletter = forms.BooleanField(
        required=False, 
        initial=True, 
        label="Subscribe to our newsletter?"
    )
    GENDER_CHOICES = [
        ('', 'Prefer not to say'),
        ('M', 'Male'),
        ('F', 'Female'),
        ('O', 'Other'),
    ]
    gender = forms.ChoiceField(
        choices=GENDER_CHOICES, 
        required=False, 
        label="Gender"
    )
    birth_date = forms.DateField(
        required=False, 
        label="Birth Date (Optional)",
        widget=forms.DateInput(attrs={'type': 'date'}), # Uses HTML5 date picker
        initial=datetime.date.today # Example initial value
    )
    website = forms.URLField(
        required=False, 
        label="Your Website (Optional)",
        widget=forms.URLInput(attrs={'placeholder': 'https://example.com'})
    )
```
In this expanded example:
*   `required=True` (which is the default for most fields) makes the field mandatory. Setting `required=False` makes it optional.
*   `help_text` provides additional guidance displayed with the form field.
*   `widget=forms.EmailInput(attrs={'placeholder': 'you@example.com'})` shows how to customize the HTML widget and add attributes like `placeholder`.
*   `IntegerField` is used for numerical integer input, with `min_value` as an example validator.
*   `BooleanField` creates a checkbox; `initial=True` makes it checked by default.
*   `ChoiceField` creates a select dropdown, taking a list of tuples (`choices`). The first element in each tuple is the value stored, and the second is the human-readable display.
*   `DateField` is for date input. Using `forms.DateInput(attrs={'type': 'date'})` can leverage the browser's native date picker. `initial` can be set to a `datetime.date` object.
*   `URLField` validates input as a URL.

### Rendering Forms in Templates
Once you have defined your form in `forms.py` and instantiated it in your view (we'll cover views in more detail later), you need to display it in an HTML template. Django provides several ways to render a form object into HTML.

First, your view function would pass the form instance to the template through the context dictionary. For example:
```python
# In your views.py
from django.shortcuts import render
from .forms import ContactForm # Assuming your form is in forms.py

def contact_view(request):
    form = ContactForm() # Create an instance of your form
    return render(request, 'myapp/contact_template.html', {'form': form})
```

Then, in your template (`myapp/contact_template.html` in this case), you can render the form using different built-in methods:

*   **`{{ form.as_p }}`:** Renders each form field and its label wrapped in `<p>` (paragraph) tags. This is a common quick way to display a form.
    ```html+django
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <button type="submit">Submit</button>
    </form>
    ```

*   **`{{ form.as_ul }}`:** Renders each form field and its label wrapped in `<li>` (list item) tags. You would typically wrap this in `<ul>`.
    ```html+django
    <form method="post">
        {% csrf_token %}
        <ul>
            {{ form.as_ul }}
        </ul>
        <button type="submit">Submit</button>
    </form>
    ```

*   **`{{ form.as_table }}`:** Renders each form field and its label wrapped in `<tr>` (table row), `<th>` (table header for label), and `<td>` (table data for field) tags. You would wrap this in `<table>`.
    ```html+django
    <form method="post">
        {% csrf_token %}
        <table>
            {{ form.as_table }}
        </table>
        <button type="submit">Submit</button>
    </form>
    ```

*   **Manual Field Rendering:** For maximum control over the form's appearance, you can render each field individually. This allows you to add custom HTML structure, classes, and attributes.
    ```html+django
    <form method="post" class="my-custom-form">
        {% csrf_token %}
        
        <div class="form-field">
            {{ form.name.label_tag }} 
            {{ form.name }} 
            {% if form.name.help_text %}
                <small class="form-help-text">{{ form.name.help_text }}</small>
            {% endif %}
            {% for error in form.name.errors %}
                <p class="error-message">{{ error }}</p>
            {% endfor %}
        </div>

        <div class="form-field">
            {{ form.email.label_tag }}
            {{ form.email }}
            {% if form.email.help_text %}
                <small class="form-help-text">{{ form.email.help_text }}</small>
            {% endif %}
            {% for error in form.email.errors %}
                <p class="error-message">{{ error }}</p>
            {% endfor %}
        </div>

        <!-- Repeat for other fields as needed -->
        
        <div class="form-field">
            {{ form.subscribe_newsletter.label_tag }} {{ form.subscribe_newsletter }}
            {% for error in form.subscribe_newsletter.errors %}
                <p class="error-message">{{ error }}</p>
            {% endfor %}
        </div>

        <button type="submit" class="submit-button">Send Message</button>
    </form>
    ```
    In manual rendering:
    *   `{{ form.field_name.label_tag }}` renders the `<label>` for the field.
    *   `{{ form.field_name }}` renders the field's widget (e.g., `<input>`, `<select>`, `<textarea>`).
    *   `{{ form.field_name.help_text }}` displays any help text associated with the field.
    *   `{{ form.field_name.errors }}` displays a list of validation errors for that field. You can loop through them if there can be multiple errors.
    *   `{{ form.non_field_errors }}` can be used to display errors that are not specific to a particular field (e.g., global form validation errors).

Choosing the rendering method depends on how much customization you need. For quick prototypes, `as_p` is often sufficient. For production UIs, manual rendering provides the most flexibility. Remember to always include `{% csrf_token %}` inside your `<form>` tag for security against Cross-Site Request Forgeries, especially if your form uses the `POST` method.

### Handling Form Data in Views
Once your form is rendered in a template, you need a view function to handle the data when the user submits it. This typically involves:

1.  **Checking the request method:** Forms are usually submitted using the `POST` method.
2.  **Binding data to the form:** If it's a `POST` request, create a form instance populated with the submitted data (`request.POST`).
3.  **Validating the form:** Call the `is_valid()` method on the form instance. Django will run all validation routines for each field (e.g., checking if required fields are present, if email fields are valid emails, etc.) and any custom validation you've defined.
4.  **Accessing cleaned data:** If `is_valid()` returns `True`, the validated data is available in the `form.cleaned_data` dictionary.
5.  **Processing the data:** Perform your desired action (e.g., save to database, send an email, etc.).
6.  **Redirecting (Post/Redirect/Get - PRG):** After successfully processing `POST` data, it's a best practice to return an `HttpResponseRedirect` to a new URL. This prevents data from being posted twice if the user refreshes the page after submission.
7.  **Handling invalid forms:** If `is_valid()` returns `False`, re-render the template with the form instance. This instance will now contain error messages that can be displayed to the user.

**Example View (`myapp/views.py`):**

Let's expand our `contact_view` to process the `ContactForm`.
```python
# In your views.py
from django.shortcuts import render, redirect
from django.urls import reverse # To generate URLs by name
from .forms import ContactForm # Assuming your form is in forms.py
# from django.core.mail import send_mail # Example: if you were sending an email

def contact_view(request):
    if request.method == 'POST':
        # Create a form instance and populate it with data from the request (binding):
        form = ContactForm(request.POST)
        # Check if the form is valid:
        if form.is_valid():
            # Process the data in form.cleaned_data
            name = form.cleaned_data['name']
            email = form.cleaned_data['email']
            message = form.cleaned_data['message']
            subscribe = form.cleaned_data['subscribe_newsletter']
            # ... and so on for other fields like age, gender, etc.

            # Example: Print to console (in a real app, you'd do something more useful)
            print(f"Contact Form Submission:")
            print(f"  Name: {name}")
            print(f"  Email: {email}")
            print(f"  Message: {message}")
            print(f"  Subscribe: {subscribe}")

            # Example: send_mail(
            # 'Contact Form Submission from ' + name,
            # message,
            # email, # from_email
            # ['your_admin_email@example.com'], # to_list
            # )
            
            # Redirect to a new URL to prevent re-submission on refresh (PRG pattern)
            # Make sure you have a URL pattern named 'thank_you' in your app's urls.py
            return redirect(reverse('myapp:thank_you')) # Assuming your app_name is 'myapp'
    else:
        # If it's a GET (or any other method), create a blank form
        form = ContactForm()

    return render(request, 'myapp/contact_template.html', {'form': form})

def thank_you_view(request):
    # A simple view to show after successful form submission
    return render(request, 'myapp/thank_you_template.html')
```

**Explanation of the View:**

*   **`if request.method == 'POST':`**: This block handles submitted form data.
*   **`form = ContactForm(request.POST)`**: Creates a "bound" form instance with the user's input.
*   **`if form.is_valid():`**: Triggers Django's validation. If all data is valid:
    *   `form.cleaned_data` dictionary contains the validated data, converted to appropriate Python types.
    *   After processing, `return redirect(reverse('myapp:thank_you'))` sends the user to a different page. `reverse()` is used to look up the URL by its name, which is more robust than hardcoding URLs. You would need to define a URL pattern named `thank_you` that maps to `thank_you_view`.
*   **`else: form = ContactForm()`**: If the request is `GET` (e.g., the user is visiting the page for the first time), an "unbound" (empty) form is created to be displayed.
*   If the form is submitted (`POST`) but is *not* valid, the `if form.is_valid():` block is skipped. The view then proceeds to `render(request, 'myapp/contact_template.html', {'form': form})`. This `form` instance now contains the submitted data *and* any error messages, which will be displayed by the template rendering tags (like `{{ form.as_p }}` or manual error display).

You would also need to create a simple template for the thank you page, for example `myapp/templates/myapp/thank_you_template.html`:
```html+django
{% extends "base_layout.html" %} {# Assuming you have a base_layout.html #}

{% block title %}Thank You - {{ block.super }}{% endblock %}

{% block content %}
  <h2>Thank You!</h2>
  <p>Your message has been submitted successfully.</p>
  <p><a href="{% url 'myapp:contact' %}">Submit another message?</a></p> {# Link back to the contact form #}
{% endblock %}
```
And ensure you have URL patterns defined in `myapp/urls.py` for `contact_view` and `thank_you_view`.

## Template Inheritance
Template inheritance is a powerful feature in Django that allows you to build a base "skeleton" template containing all the common elements of your site and define **blocks** that child templates can override. This helps you adhere to the DRY (Don't Repeat Yourself) principle, reducing redundancy and making your templates easier to maintain.

**The Core Idea:**

1.  **Base Template:** You create a base template (e.g., `base_layout.html`) that includes the main HTML structure (like `<html>`, `<head>`, `<body>`, common navigation, footer). This base template defines named blocks using the `{% block %}` tag.
2.  **Child Templates:** Other templates in your application can then "extend" this base template. They use the `{% extends "path/to/base_template.html" %}` tag (usually as the first line) and can then override the content of the blocks defined in the parent template.

**Key Tags:**

*   **`{% block block_name %}` ... `{% endblock block_name %}`:**
    Defines a block in the base template that child templates can fill in. It's good practice to name your `endblock` tag (e.g., `{% endblock content %}`).
*   **`{% extends "base_template.html" %}`:**
    Used in a child template to specify the parent template it inherits from. This must be the first template tag in the file.
*   **`{{ block.super }}` (Optional):**
    If used within a `{% block %}` in a child template, it will render the content of the parent template's block at that position. This is useful for adding to a parent's block content rather than completely replacing it.

**Example: `base_layout.html`**

This file would typically be placed in a project-level `templates` directory or a shared app's `templates` directory (e.g., `myproject/templates/base_layout.html` or `common_app/templates/common_app/base_layout.html`).

```html+django
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Awesome Django Site{% endblock title %}</title>
    {# Link to global CSS, JS, etc. - Assuming you have static files set up #}
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/global_styles.css' %}">
    {# Block for additional head content like page-specific CSS or meta tags #}
    {% block extra_head %}{% endblock extra_head %}
</head>
<body>
    <header class="site-header">
        <div class="container">
            <h1>{% block page_header %}Welcome to My Site!{% endblock page_header %}</h1>
            <nav class="main-navigation">
                <ul>
                    <li><a href="{% url 'home_page' %}">Home</a></li> {# Replace 'home_page' with your actual home URL name #}
                    <li><a href="{% url 'about_page' %}">About Us</a></li> {# Replace 'about_page' with your actual about URL name #}
                    {% block nav_items %}{# For additional navigation items from child templates #}{% endblock nav_items %}
                </ul>
            </nav>
        </div>
    </header>

    <main class="container page-content">
        {% block content %}
            <p>This is default content. Child templates should override this block.</p>
        {% endblock content %}
    </main>

    <footer class="site-footer">
        <div class="container">
            <p>&copy; {% now "Y" %} MyApp. All rights reserved.
            {% block footer_extra %}{# For extra content in the footer #}{% endblock footer_extra %}</p>
        </div>
    </footer>

    {# Optional: Common JavaScript files #}
    {% block extra_scripts %}{% endblock extra_scripts %}
</body>
</html>
```
This base template defines several blocks (`title`, `extra_head`, `page_header`, `nav_items`, `content`, `footer_extra`, `extra_scripts`) that child templates can customize.















