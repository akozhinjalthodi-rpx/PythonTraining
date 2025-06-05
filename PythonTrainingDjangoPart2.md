Date: 10 Aug 2022

-----------------

## Creating first Django App 
Here we are going to create a basic poll application.

It will consist of two Parts.

* A public site that lets people view polls and vote in them.
* An admin site that lets you add, change, and delete polls.

### Creating a project
From the command line, cd into a directory where you’d like to store your code, then run the following command:

```
django-admin startproject mypollingwebapp
```

After running the above command, you will be seeing the below diretory in and files in current dir.

```
mypollingwebapp/
    manage.py
    mypollingwebapp/
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
```
These files are:


* The outer `mypollingwebapp/` root directory is a container for your project. Its name doesn’t matter to Django; you can rename it to anything you like.
* `manage.py`: A command-line utility that lets you interact with this Django project in various ways. 

Ref : https://docs.djangoproject.com/en/4.1/ref/django-admin/

* The inner `mypollingwebapp/` directory is the actual Python package for your project. Its name is the Python package name you’ll need to use to import anything inside it (e.g. mypollingwebapp.urls).
mypollingwebapp/`__init__.py`: An empty file that tells Python that this directory should be considered a Python package.

Ref: https://docs.python.org/3/tutorial/modules.html#tut-packages

* `mypollingwebapp/settings.py`: Settings/configuration for this Django project.
  
Ref: https://docs.djangoproject.com/en/4.1/topics/settings/

* `mypollingwebapp/urls.py`: The URL declarations for this Django project; a “table of contents” of your Django-powered site. 

Ref: https://docs.djangoproject.com/en/4.1/topics/http/urls/

* `mypollingwebapp/asgi.py`: An entry-point for ASGI-compatible web servers to serve your project. 


Ref : https://docs.djangoproject.com/en/4.1/howto/deployment/asgi/

* mypollingwebapp/wsgi.py: An entry-point for WSGI-compatible web servers to serve your project.

Ref : https://docs.djangoproject.com/en/4.1/howto/deployment/wsgi/

#### django-admin and manage.py

`django-admin` is Django’s command-line utility for administrative tasks

In addition, `manage.py` is automatically created in each Django project. It does the same thing as django-admin but also sets the `DJANGO_SETTINGS_MODULE` environment variable so that it points to your project’s `settings.py` file.

Generally, when working on a single Django project, it’s easier to use manage.py than django-admin. If you need to switch between multiple Django settings files, use django-admin with DJANGO_SETTINGS_MODULE or the --settings command line option.

The command-line examples throughout this document use django-admin to be consistent, but any example can use manage.py or python -m django just as well.

##### Usage 
```
$ django-admin <command> [options]
$ manage.py <command> [options]
$ python -m django <command> [options]
```
#### Getting runtime help
`django-admin help` Run `django-admin help` to display usage information and a list of the commands provided by each application.

Run `django-admin help --commands` to display a list of all available commands.

Run `django-admin help <command>` to display a description of the given command and a list of its available options.

#### Django settings
A Django settings file contains all the configuration of your Django installation.

##### The Basics
A settings file is just a Python module with module-level variables.
Here are a couple of example settings:
```ini
ALLOWED_HOSTS = ['www.example.com']
DEBUG = False
DEFAULT_FROM_EMAIL = 'webmaster@example.com'
```
Because a settings file is a Python module, the following apply:

* It doesn’t allow for Python syntax errors.
* It can assign settings dynamically using normal Python syntax. For example:
```ini
MY_SETTING = [str(i) for i in range(30)]
```
* It can import values from other settings files.

##### Designating the settings
`DJANGO_SETTINGS_MODULE`

When you use Django, you have to tell it which settings you’re using. Do this by using an environment variable, `DJANGO_SETTINGS_MODULE`.

The value of `DJANGO_SETTINGS_MODULE` should be in Python path syntax, e.g. `mypollingwebapp .settings`. Note that the settings module should be on the Python import search path.


### Creating the Polls app

Each application you write in Django consists of a Python package that follows a certain convention. Django comes with a utility that automatically generates the basic directory structure of an app, so you can focus on writing code rather than creating directories.

#### *_Projects vs. apps_*

What’s the difference between a project and an app? An app is a web application that does something – e.g., a blog system, a database of public records or a small poll app. A project is a collection of configuration and apps for a particular website. A project can contain multiple apps. An app can be in multiple projects.

Your apps can live anywhere on your Python path. In this tutorial, we’ll create our poll app in the same directory as your manage.py file so that it can be imported as its own top-level module, rather than a submodule of mypollingwebapp .

To create your app, make sure you’re in the same directory as manage.py and type this command:

```
python manage.py startapp polls
```
That’ll create a directory polls, which is laid out like this:

```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
#### Write your first view

A **view function**, or "view" for short, is a Python function that takes a web request and returns a web response. This response can be the HTML contents of a Web page, a redirect, a 404 error, an XML document, an image, or anything else. The view itself contains whatever arbitrary logic is necessary to return that response.

Let's write our first view. Open the file `polls/views.py` and put the following Python code in it:

##### polls/views.py 
```python
from django.http import HttpResponse

# This is the simplest view possible in Django.
# To call the view, we need to map it to a URL - and for this we need a URLconf.
def index(request):
    # The view returns an HttpResponse object containing the generated response.
    # Here, it's a simple string of HTML.
    return HttpResponse("<h1>Hello, world. You're at the polls index.</h1>")
```

To make this view callable via a URL, we need to create a URL configuration (URLconf).

1.  **Create an app-level `urls.py`:**
    Inside your `polls` directory, create a new file named `urls.py`. This file will contain URL patterns specific to the `polls` app.

    ##### polls/urls.py
    ```python
    from django.urls import path
    from . import views # Import views from the current app (polls)

    # app_name helps Django distinguish URL names between different apps
    app_name = 'polls'

    urlpatterns = [
        # When a user requests the root of this app's URL patterns (e.g., /polls/),
        # Django will call the views.index function.
        # The name='index' argument provides a way to refer to this URL pattern
        # from other parts of Django, especially templates.
        path('', views.index, name='index'),
    ]
    ```

2.  **Include the app's URLconf in the project-level `urls.py`:**
    The next step is to point the root URLconf (in `mypollingwebapp/urls.py`) at the `polls.urls` module we just created.

    Open `mypollingwebapp/urls.py` and modify it:
    ```python
    from django.contrib import admin
    from django.urls import include, path # Make sure 'include' is imported

    urlpatterns = [
        # When a URL starting with 'polls/' is requested,
        # Django will strip off 'polls/' and pass the remaining string
        # to the 'polls.urls' URLconf for further processing.
        path('polls/', include('polls.urls')),
        path('admin/', admin.site.urls),
    ]
    ```
    The `include()` function allows referencing other URLconfs. This promotes modularity, as each app can manage its own set of URLs. The `polls` app's URLs are now prefixed with `polls/`.

**How URL Dispatching Works:**
*   When a user requests a page (e.g., `/polls/`), Django loads the `ROOT_URLCONF` specified in `mypollingwebapp/settings.py` (which is `mypollingwebapp.urls` by default).
*   Django iterates through each `path()` in `urlpatterns`.
*   For `/polls/`, it matches `path('polls/', include('polls.urls'))`.
*   Django then chops off the matched part (`polls/`) and sends the remaining string (empty in this case) to the included `polls.urls` for further processing.
*   In `polls.urls`, the empty string matches `path('', views.index, name='index')`, so the `views.index` function is called.

**Run the Development Server:**
Make sure you are in the directory containing `manage.py` (the outer `mypollingwebapp/` directory) and run:
```bash
python manage.py runserver
```
(If port 8000 is in use, you can specify another: `python manage.py runserver 8001`)

Now, open your web browser and go to `http://127.0.0.1:8000/polls/`. You should see the text "Hello, world. You're at the polls index." rendered in an `<h1>` tag, which is what our `index` view returns.

**Understanding `path()` Arguments:**
The `path()` function can take up to four arguments:
*   `route` (required): A string containing a URL pattern. It does not match GET/POST parameters or the domain name. Example: `'<int:question_id>/'`
*   `view` (required): When Django finds a matching pattern, it calls this specified view function with an `HttpRequest` object as the first argument and any "captured" values from the route as keyword arguments.
*   `kwargs` (optional): A dictionary of arbitrary keyword arguments that can be passed to the target view.
*   `name` (optional): Naming your URL lets you refer to it unambiguously from other parts of Django, especially from within templates using the `{% url %}` tag. This is a very powerful feature that allows you to change URL patterns without having to update all references to them.

### Write views that actually do something
Each view is responsible for doing one of two things: returning an `HttpResponse` object containing the content for the requested page, or raising an exception such as `Http404`. The rest is up to you.

Your view can read records from a database, or not. It can use a template system such as Django’s – or a third-party Python template system – or not. It can generate a PDF file, output XML, create a ZIP file on the fly, anything you want, using whatever Python libraries you want.

All Django wants is that `HttpResponse`. Or an exception.

Let's expand our `polls` app views in `polls/views.py`. First, we'll create a few more placeholder views:

```python
# polls/views.py
from django.http import HttpResponse, Http404 # Add Http404
from django.shortcuts import render, get_object_or_404 # Add render and get_object_or_404
from django.template import loader # For loading templates
from .models import Question # Assuming your models are in polls.models

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    # output = ', '.join([q.question_text for q in latest_question_list])
    # return HttpResponse(output)

    # Using Django's template system
    template = loader.get_template('polls/index.html') # Loads the template
    context = { # A dictionary mapping template variable names to Python objects
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))

def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    # The get_object_or_404() is a shortcut. It tries Question.objects.get(pk=question_id).
    # If a Question with that primary key (pk) doesn't exist, it raises an Http404 exception.
    # try:
    #     question = Question.objects.get(pk=question_id)
    # except Question.DoesNotExist:
    #     raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', {'question': question})
    # The render() function is another shortcut. It takes the request, template path,
    # and context dictionary, and returns an HttpResponse of the rendered template.

def results(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/results.html', {'question': question})

def vote(request, question_id):
    # This view will handle the voting logic for a specific question.
    # We'll implement its full logic later when discussing forms.
    return HttpResponse(f"You're voting on question {question_id}.")
```

Now, update `polls/urls.py` to include these new views:
```python
# polls/urls.py
from django.urls import path
from . import views

app_name = 'polls' # Essential for namespacing URLs
urlpatterns = [
    path('', views.index, name='index'),
    # Example: /polls/5/
    path('<int:question_id>/', views.detail, name='detail'),
    # Example: /polls/5/results/
    path('<int:question_id>/results/', views.results, name='results'),
    # Example: /polls/5/vote/
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```
The `<int:question_id>` part in the routes captures an integer from the URL and passes it as a keyword argument `question_id` to the respective view function.

#### Using Django's Template System

Hardcoding HTML in views is not maintainable. Django's template system allows you to separate the presentation (HTML) from the Python code.

1.  **Create a `templates` directory:**
    Inside your `polls` app directory, create a `templates` directory. Inside `polls/templates/`, create another directory named `polls` (this is for namespacing, so Django can distinguish this app's templates from others).
    Your template files will go into `polls/templates/polls/`.

    Structure:
    ```
    polls/
        templates/
            polls/
                index.html
                detail.html
                results.html
    ```

2.  **Template Namespacing:**
    Placing app-specific templates inside a subdirectory named after the app (e.g., `polls/templates/polls/`) is a crucial best practice. Django's template loaders (especially `APP_DIRS=True` in `settings.py`) will look for templates in these locations. This namespacing prevents conflicts if another app in your project has a template with the same name (e.g., `index.html`). You'll refer to these templates in your views as `polls/index.html`.

3.  **Create `polls/templates/polls/index.html`:**
    ```html+django
    {% if latest_question_list %}
        <ul>
        {% for question in latest_question_list %}
            {# Use the {% url %} template tag for robust URL reversing #}
            {# 'polls:detail' refers to the URL pattern named 'detail' within the 'polls' app namespace #}
            <li><a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a></li>
        {% endfor %}
        </ul>
    {% else %}
        <p>No polls are available.</p>
    {% endif %}
    ```

4.  **Create `polls/templates/polls/detail.html`:**
    ```html+django
    <h1>{{ question.question_text }}</h1>

    {% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}

    <form action="{% url 'polls:vote' question.id %}" method="post">
    {% csrf_token %} {# Essential for security against Cross-Site Request Forgeries #}
    {% for choice in question.choice_set.all %}
        <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}">
        <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br>
    {% endfor %}
    <input type="submit" value="Vote">
    </form>
    ```

5.  **Create `polls/templates/polls/results.html`:**
    ```html+django
    <h1>{{ question.question_text }}</h1>

    <ul>
    {% for choice in question.choice_set.all %}
        <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
    {% endfor %}
    </ul>

    <a href="{% url 'polls:detail' question.id %}">Vote again?</a>
    ```

**Explanation of Template Tags and Variables:**
*   `{{ variable }}`: Outputs the value of `variable`. Django performs lookups (dictionary, attribute, list-index).
*   `{% tag %}`: Executes a template tag.
    *   `{% if condition %}` ... `{% else %}` ... `{% endif %}`: Conditional rendering.
    *   `{% for item in list %}` ... `{% endfor %}`: Loops through items in a list.
    *   `{% url 'namespace:name' arg1 arg2 ... %}`: **URL Reversing**. This is a powerful tag that generates a URL based on the `name` given to a `path()` in your `urls.py`. It's preferred over hardcoding URLs because if you change the URL pattern in `urls.py`, your templates don't need to change as long as the name remains the same. The `polls:detail` part means "look for a URL pattern named `detail` inside the app namespace `polls`".
    *   `{% csrf_token %}`: Protects against Cross-Site Request Forgeries for POST forms.
*   Filters: `{{ choice.votes|pluralize }}` uses the `pluralize` filter to correctly add an "s" to "vote" if there's more than one vote.

#### The `render()` shortcut
Loading a template, filling a context, and returning an `HttpResponse` is a common pattern. Django provides the `render()` shortcut in `django.shortcuts`:
```python
# polls/views.py (index view using render)
from django.shortcuts import render
from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    # render() takes the request, template path, and context dictionary.
    return render(request, 'polls/index.html', context)
```
This makes views more concise.

#### The `get_object_or_404()` shortcut
Trying to get an object and raising `Http404` if it doesn't exist is also common. Django provides `get_object_or_404()`:
```python
# polls/views.py (detail view using get_object_or_404)
from django.shortcuts import get_object_or_404, render
from .models import Question

def detail(request, question_id):
    # The first argument is the Model class, followed by lookup parameters.
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```
This simplifies error handling for non-existent objects.

After making these changes and creating the template files, run the development server (`python manage.py runserver`) and navigate to `/polls/` in your browser. You should see the list of questions, and be able to click on them to go to their detail pages.

### Form handling and `reverse()`

The `vote` view needs to handle incoming POST data from the form in `polls/detail.html`.

```python
# polls/views.py
from django.http import HttpResponse, HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse # Used for URL reversing in Python code
from .models import Choice, Question

# ... (index, detail, results views as before) ...

def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        # request.POST is a dictionary-like object containing submitted POST data.
        # 'choice' is the name of our radio input in detail.html.
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form if a choice wasn't selected
        # or if the choice ID is invalid.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        # reverse() is used to generate the URL for the results page.
        # 'polls:results' refers to the URL pattern named 'results' in the 'polls' app namespace.
        # args=(question.id,) passes the necessary arguments to construct the URL.
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```
**Key points in the `vote` view:**
*   `request.POST['choice']`: Accesses the ID of the selected radio button. Raises `KeyError` if 'choice' isn't in the POST data.
*   `HttpResponseRedirect`: After successfully processing POST data, it's a best practice to redirect the user. This prevents issues if the user refreshes the page or clicks the back button (which could resubmit the form).
*   `reverse('polls:results', args=(question.id,))`: This function is the Python equivalent of the `{% url %}` template tag. It looks up the URL pattern named `results` in the `polls` app namespace and constructs the correct URL (e.g., `/polls/1/results/`). Using `reverse()` is more robust than hardcoding URLs.

### Database setup
Now, open up `mypollingwebapp /settings.py`. It’s a normal Python module with module-level variables representing Django settings.

By default, the configuration uses *SQLite*. If you’re new to databases, or you’re just interested in trying Django, this is the easiest choice. *SQLite is included in Python, so you won’t need to install anything else to support your database*. When starting your first real project, however, you may want to use a more scalable database like PostgreSQL, to avoid database-switching headaches down the road.

If you wish to use another database, install the appropriate database bindings and change the following keys in the DATABASES 'default' item to match your database connection settings:
* ENGINE – Either 'django.db.backends.sqlite3', 'django.db.backends.postgresql', 'django.db.backends.mysql', or 'django.db.backends.oracle'. Other backends are also available.
* NAME – The name of your database. If you’re using SQLite, the database will be a file on your computer; in that case, NAME should be the full absolute path, including filename, of that file. The default value, BASE_DIR / 'db.sqlite3', will store the file in your project directory.

If you are not using SQLite as your database, additional settings such as USER, PASSWORD, and HOST must be added. For more details, see the reference documentation for DATABASES.


Ref: https://docs.djangoproject.com/en/4.1/topics/install/#database-installation

Ref: https://docs.djangoproject.com/en/4.1/ref/settings/#std-setting-DATABASES

#### For databases other than SQLite

>If you’re using a database besides SQLite, make sure you’ve created a database by this point. Do that with “CREATE DATABASE database_name;” within your database’s interactive prompt.

> Also make sure that the database user provided in mypollingwebapp /settings.py has “create database” privileges. This allows automatic creation of a test database which will be needed in a later tutorial.

>If you’re using SQLite, you don’t need to create anything beforehand - the database file will be created automatically when it is needed.


While you’re editing mypollingwebapp /settings.py, set TIME_ZONE to your time zone.

Also, note the *INSTALLED_APPS* setting at the top of the file. That holds the names of all Django applications that are activated in this Django instance. Apps can be used in multiple projects, and you can package and distribute them for use by others in their projects.

By default, INSTALLED_APPS contains the following apps, all of which come with Django:

* django.contrib.admin – The admin site. You’ll use it shortly.
* django.contrib.auth – An authentication system.
* django.contrib.contenttypes – A framework for content types.
* django.contrib.sessions – A session framework.
* django.contrib.messages – A messaging framework.
* django.contrib.staticfiles – A framework for managing static files.

The migrate command looks at the INSTALLED_APPS setting and creates any necessary database tables according to the database settings in your mypollingwebapp /settings.py file and the database migrations shipped with the app (we’ll cover those later). You’ll see a message for each migration it applies. If you’re interested, run the command-line client for your database and type \dt (PostgreSQL), SHOW TABLES; (MariaDB, MySQL), .tables (SQLite), or SELECT TABLE_NAME FROM USER_TABLES; (Oracle) to display the tables Django created.

```
For the minimalists

Like we said above, the default applications are included for the common case, but not everybody needs them. If you don’t need any or all of them, feel free to comment-out or delete the appropriate line(s) from INSTALLED_APPS before running migrate. The migrate command will only run migrations for apps in INSTALLED_APPS.
```

#### Creating models
Now we’ll define your models – essentially, your database layout, with additional metadata.
```
Philosophy

A model is the single, definitive source of information about your data. It contains the essential fields and behaviors of the data you’re storing. Django follows the DRY Principle. The goal is to define your data model in one place and automatically derive things from it.

This includes the migrations - unlike in Ruby On Rails, for example, migrations are entirely derived from your models file, and are essentially a history that Django can roll through to update your database schema to match your current models.

```

In our poll app, we’ll create two models: Question and Choice. A Question has a question and a publication date. A Choice has two fields: the text of the choice and a vote tally. Each Choice is associated with a Question.

These concepts are represented by Python classes. Edit the polls/models.py file so it looks like this:

```python
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```
Here, each model is represented by a class that subclasses django.db.models.Model. Each model has a number of class variables, each of which represents a database field in the model.

Each field is represented by an instance of a Field class – e.g., CharField for character fields and DateTimeField for datetimes. This tells Django what type of data each field holds.

The name of each Field instance (e.g. question_text or pub_date) is the field’s name, in machine-friendly format. You’ll use this value in your Python code, and your database will use it as the column name.

You can use an optional first positional argument to a Field to designate a human-readable name. That’s used in a couple of introspective parts of Django, and it doubles as documentation. If this field isn’t provided, Django will use the machine-readable name. In this example, we’ve only defined a human-readable name for Question.pub_date. For all other fields in this model, the field’s machine-readable name will suffice as its human-readable name.

Some `Field` classes have required arguments. `CharField`, for example, requires that you give it a `max_length`. That’s used not only in the database schema, but in validation, as we’ll soon see.

A Field can also have various optional arguments; in this case, we’ve set the default value of votes to 0.

Finally, note a relationship is defined, using ForeignKey. That tells Django each Choice is related to a single Question. Django supports all the common database relationships: many-to-one, many-to-many, and one-to-one.

#### Activating models
That small bit of model code gives Django a lot of information. With it, Django is able to:

* Create a database schema (CREATE TABLE statements) for this app.
* Create a Python database-access API for accessing Question and Choice objects.

But first we need to tell our project that the polls app is installed.

```
Philosophy

Django apps are “pluggable”: You can use an app in multiple projects, and you can distribute apps, because they don’t have to be tied to a given Django installation.
```
To include the app in our project, we need to add a reference to its configuration class in the INSTALLED_APPS setting. The PollsConfig class is in the polls/apps.py file, so its dotted path is 'polls.apps.PollsConfig'. Edit the mypollingwebapp /settings.py file and add that dotted path to the INSTALLED_APPS setting. It’ll look like this:

```python
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

Now Django knows to include the polls app. Let’s run another command:

```
python manage.py makemigrations polls2
```
You should see something similar to the following:
```
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
```
By running makemigrations, you’re telling Django that you’ve made some changes to your models (in this case, you’ve made new ones) and that you’d like the changes to be stored as a migration.

Migrations are how Django stores changes to your models (and thus your database schema) - they’re files on disk. You can read the migration for your new model if you like; it’s the file polls/migrations/0001_initial.py. Don’t worry, you’re not expected to read them every time Django makes one, but they’re designed to be human-editable in case you want to manually tweak how Django changes things.

There’s a command that will run the migrations for you and manage your database schema automatically - that’s called migrate, and we’ll come to it in a moment - but first, let’s see what SQL that migration would run. The sqlmigrate command takes migration names and returns their SQL:

```
manage.py sqlmigrate polls2 0001
```
You should see something similar to the following (we’ve reformatted it for readability):

```sql
BEGIN;
--
-- Create model Question
--
CREATE TABLE "polls_question" (
    "id" serial NOT NULL PRIMARY KEY,
    "question_text" varchar(200) NOT NULL,
    "pub_date" timestamp with time zone NOT NULL
);
--
-- Create model Choice
--
CREATE TABLE "polls_choice" (
    "id" serial NOT NULL PRIMARY KEY,
    "choice_text" varchar(200) NOT NULL,
    "votes" integer NOT NULL,
    "question_id" integer NOT NULL -- This will store the ID of the related Question
);
ALTER TABLE "polls_choice"
  ADD CONSTRAINT "polls_choice_question_id_c5b4b260_fk_polls_question_id"
    FOREIGN KEY ("question_id") -- Establishes the foreign key relationship
    REFERENCES "polls_question" ("id") -- Points to the 'id' field of the 'polls_question' table
    DEFERRABLE INITIALLY DEFERRED; -- Database-specific instruction for transaction handling
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id"); -- Creates an index for faster lookups on question_id

COMMIT;      
```
**Key points about the generated SQL and Django's model-to-database mapping:**

*   **Database Agnostic (Mostly):** Django abstracts many database-specific details. The SQL shown is for PostgreSQL, but Django would generate equivalent SQL for MySQL, SQLite, Oracle, etc.
*   **Table Names:** Automatically generated as `appname_modelname` (e.g., `polls_question`). This can be overridden in the model's `Meta` class.
*   **Primary Keys (`id`):** An `id` field is automatically added as an auto-incrementing primary key for each model, unless you explicitly define a different primary key.
*   **Foreign Keys:** Django appends `_id` to the field name to create the database column for a `ForeignKey` (e.g., `question` field in `Choice` model becomes `question_id` column). This is also overridable.
*   **Constraints:** `FOREIGN KEY` constraints are created to maintain relational integrity at the database level.
*   **Indexes:** Django automatically creates indexes on foreign keys and fields specified with `db_index=True` for performance.
*   **`sqlmigrate` Utility:** The `sqlmigrate` command is excellent for understanding what Django is doing under the hood or for providing SQL scripts to database administrators. It **does not** run the migration; it only displays the SQL.

If you’re interested, you can also run `python manage.py check`; this checks for any problems in your project without making migrations or touching the database.

Now, run `migrate` again to create those model tables in your database:

```
$python manage.py migrate

Operations to perform:                                                                                                    Apply all migrations: admin, auth, contenttypes, polls2, sessions                                                     Running migrations:                                                                                                       Applying polls2.0001_initial... OK   
```

The migrate command takes all the migrations that haven’t been applied (Django tracks which ones are applied using a special table in your database called django_migrations) and runs them against your database - essentially, synchronizing the changes you made to your models with the schema in the database.

Migrations are very powerful and let you change your models over time, as you develop your project, without the need to delete your database or tables and make new ones - it specializes in upgrading your database live, without losing data. We’ll cover them in more depth in a later part of the tutorial, but for now, remember the three-step guide to making model changes:

* Change your models (in models.py).
* Run python manage.py makemigrations to create migrations for those changes
* Run python manage.py migrate to apply those changes to the database.

The reason that there are separate commands to make and apply migrations is because you’ll commit migrations to your version control system and ship them with your app; they not only make your development easier, they’re also usable by other developers and in production.


#### Playing with the API
Now, let’s hop into the interactive Python shell and play around with the free API Django gives you. To invoke the Python shell, use this command:
```
python manage.py shell
```
We’re using this instead of simply typing “python”, because manage.py sets the DJANGO_SETTINGS_MODULE environment variable, which gives Django the Python import path to your mypollingwebapp /settings.py file.

Once you’re in the shell, explore the database API:

```python
>>> from polls2.models import Choice, Question  # Import the model classes we just wrote.

# No questions are in the system yet.
>>> Question.objects.all()
<QuerySet []>

# Create a new Question.
# Support for time zones is enabled in the default settings file, so
# Django expects a datetime with tzinfo for pub_date. Use timezone.now()
# instead of datetime.datetime.now() and it will do the right thing.
>>> from django.utils import timezone
>>> q = Question(question_text="What's new?", pub_date=timezone.now())

# Save the object into the database. You have to call save() explicitly.
>>> q.save()

# Now it has an ID.
>>> q.id
1

# Access model field values via Python attributes.
>>> q.question_text
"What's new?"
>>> q.pub_date
datetime.datetime(2012, 2, 26, 13, 0, 0, 775217, tzinfo=<UTC>)

# Change values by changing the attributes, then calling save().
>>> q.question_text = "What's up?"
>>> q.save()

# objects.all() displays all the questions in the database.
>>> Question.objects.all()
<QuerySet [<Question: Question object (1)>]>
```
`<Question: Question object (1)>` isn’t a helpful representation of this object. Let’s fix that by editing the Question model (in the polls/models.py file) and adding a `__str__()` method to both Question and Choice:

```python
from django.db import models

class Question(models.Model):
    # ...
    def __str__(self):
        return self.question_text

class Choice(models.Model):
    # ...
    def __str__(self):
        return self.choice_text
```
It’s important to add `__str__()` methods to your models, not only for your own convenience when dealing with the interactive prompt, but also because objects’ representations are used throughout Django’s automatically-generated admin.

Let’s also add a custom method to this model:

```python
import datetime

from django.db import models
from django.utils import timezone


class Question(models.Model):
    # ...
    def was_published_recently(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```
Note the addition of import datetime and from django.utils import timezone, to reference Python’s standard datetime module and Django’s time-zone-related utilities in django.utils.timezone, respectively

Save these changes and start a new Python interactive shell by running python manage.py shell again:


```python
>>> from polls.models import Choice, Question

# Make sure our __str__() addition worked.
>>> Question.objects.all()
<QuerySet [<Question: What's up?>]>

# Django provides a rich database lookup API that's entirely driven by
# keyword arguments.
>>> Question.objects.filter(id=1)
<QuerySet [<Question: What's up?>]>
>>> Question.objects.filter(question_text__startswith='What')
<QuerySet [<Question: What's up?>]>

# Get the question that was published this year.
>>> from django.utils import timezone
>>> current_year = timezone.now().year
>>> Question.objects.get(pub_date__year=current_year)
<Question: What's up?>

# Request an ID that doesn't exist, this will raise an exception.
>>> Question.objects.get(id=2)
Traceback (most recent call last):
    ...
DoesNotExist: Question matching query does not exist.

# Lookup by a primary key is the most common case, so Django provides a
# shortcut for primary-key exact lookups.
# The following is identical to Question.objects.get(id=1).
>>> Question.objects.get(pk=1)
<Question: What's up?>

# Make sure our custom method worked.
>>> q = Question.objects.get(pk=1)
>>> q.was_published_recently()
True

# Give the Question a couple of Choices. The create call constructs a new
# Choice object, does the INSERT statement, adds the choice to the set
# of available choices and returns the new Choice object. Django creates
# a set to hold the "other side" of a ForeignKey relation
# (e.g. a question's choice) which can be accessed via the API.
>>> q = Question.objects.get(pk=1)

# Display any choices from the related object set -- none so far.
>>> q.choice_set.all()
<QuerySet []>

# Create three choices.
>>> q.choice_set.create(choice_text='Not much', votes=0)
<Choice: Not much>
>>> q.choice_set.create(choice_text='The sky', votes=0)
<Choice: The sky>
>>> c = q.choice_set.create(choice_text='Just hacking again', votes=0)

# Choice objects have API access to their related Question objects.
>>> c.question
<Question: What's up?>

# And vice versa: Question objects get access to Choice objects.
>>> q.choice_set.all()
<QuerySet [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]>
>>> q.choice_set.count()
3

# The API automatically follows relationships as far as you need.
# Use double underscores to separate relationships.
# This works as many levels deep as you want; there's no limit.
# Find all Choices for any question whose pub_date is in this year
# (reusing the 'current_year' variable we created above).
>>> Choice.objects.filter(question__pub_date__year=current_year)
<QuerySet [<Choice: Not much>, <Choice: The sky>, <Choice: Just hacking again>]>

# Let's delete one of the choices. Use delete() for that.
>>> c = q.choice_set.filter(choice_text__startswith='Just hacking')
>>> c.delete()
```

#### Introducing the Django Admin

```
Philosophy

Generating admin sites for your staff or clients to add, change, and delete content is tedious work that doesn’t require much creativity. For that reason, Django entirely automates creation of admin interfaces for models.

Django was written in a newsroom environment, with a very clear separation between “content publishers” and the “public” site. Site managers use the system to add news stories, events, sports scores, etc., and that content is displayed on the public site. Django solves the problem of creating a unified interface for site administrators to edit content.

The admin isn’t intended to be used by site visitors. It’s for site managers.
```
#### Creating an admin user
First we’ll need to create a user who can login to the admin site. Run the following command:

```
python manage.py createsuperuser
```
Enter your desired username and press enter.

```
Username: admin
```
You will then be prompted for your desired email address:
```
Email address: admin@example.com
```
The final step is to enter your password. You will be asked to enter your password twice, the second time as a confirmation of the first.

```
Password: **********
Password (again): *********
Superuser created successfully.
```
#### Start the development server
The Django admin site is activated by default. Let’s start the development server and explore it.

```
python manage.py runserver 8080
```

Explore admin UI by navigating into http://127.0.0.1:8080/admin/

#### Make the poll app modifiable in the admin
We need to tell the admin that Question objects have an admin interface. To do this, open the polls/admin.py file, and edit it to look like this:

```python
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```

Date : 11 Aug 2022

-----------

### Overview

A view is a “type” of web page in your Django application that generally serves a specific function and has a specific template. For example, in a blog application, you might have the following views:

* Blog homepage – displays the latest few entries.
* Entry “detail” page – permalink page for a single entry.
* Year-based archive page – displays all months with entries in the given year.
* Month-based archive page – displays all days with entries in the given month.
* Day-based archive page – displays all entries in the given day.
* Comment action – handles posting comments to a given entry.

In our poll application, we’ll have the following four views:

* Question “index” page – displays the latest few questions.
* Question “detail” page – displays a question text, with no results but with a form to vote.
* Question “results” page – displays results for a particular question.
* Vote action – handles voting for a particular choice in a particular question.

In Django, web pages and other content are delivered by views. Each view is represented by a Python function (or method, in the case of class-based views). Django will choose a view by examining the URL that’s requested (to be precise, the part of the URL after the domain name).

A URL pattern is the general form of a URL - for example: `/newsarchive/<year>/<month>/.`

To get from a URL to a view, Django uses what are known as ‘URLconfs’. A URLconf maps URL patterns to views.

```python
def detail(request, question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the results of question %s."
    return HttpResponse(response % question_id)

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)
```

Take a look in your browser, at “/polls/34/”. It’ll run the detail() method and display whatever ID you provide in the URL. Try “/polls/34/results/” and “/polls/34/vote/” too – these will display the placeholder results and voting pages.

When somebody requests a page from your website – say, “/polls/34/”, Django will load the mypollingwebapp .urls Python module because it’s pointed to by the *ROOT_URLCONF* setting. It finds the variable named urlpatterns and traverses the patterns in order. After finding the match at 'polls/', it strips off the matching text ("polls/") and sends the remaining text – "34/" – to the ‘polls.urls’ URLconf for further processing. There it matches '<int:question_id>/', resulting in a call to the detail() view like so:

```
detail(request=<HttpRequest object>, question_id=34)
```
The question_id=34 part comes from <int:question_id>. Using angle brackets “captures” part of the URL and sends it as a keyword argument to the view function. The question_id part of the string defines the name that will be used to identify the matched pattern, and the int part is a converter that determines what patterns should match this part of the URL path. The colon (:) separates the converter and pattern name.

### Write views that actually do something
Each view is responsible for doing one of two things: returning an HttpResponse object containing the content for the requested page, or raising an exception such as Http404. The rest is up to you.

Your view can read records from a database, or not. It can use a template system such as Django’s – or a third-party Python template system – or not. It can generate a PDF file, output XML, create a ZIP file on the fly, anything you want, using whatever Python libraries you want.

All Django wants is that HttpResponse. Or an exception.

Because it’s convenient, let’s use Django’s own database API, which we covered previously. Here’s one stab at a new index() view, which displays the latest 5 poll questions in the system, separated by commas, according to publication date:

```python
from urllib import response
from django.http import HttpResponse
from .models import Question

def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    output = ', '.join(q.question_text for q in latest_question_list)
    return HttpResponse(output)

def detail(request,question_id):
    return HttpResponse("You're looking at question %s." % question_id)

def results(request, question_id):
    response = "You're looking at the result of question %s."
    return HttpResponse(response % question_id) 

def vote(request, question_id):
    return HttpResponse("You're voting on question %s." % question_id)

# Leave the rest of the views (detail, results, vote) unchanged
```
There’s a problem here, though: the page’s design is hard-coded in the view. If you want to change the way the page looks, you’ll have to edit this Python code. So let’s use Django’s template system to separate the design from Python by creating a template that the view can use.

First, create a directory called templates in your polls directory. Django will look for templates in there.

Your project’s TEMPLATES setting describes how Django will load and render templates. The default settings file configures a DjangoTemplates backend whose APP_DIRS option is set to True. By convention DjangoTemplates looks for a “templates” subdirectory in each of the INSTALLED_APPS.

Within the templates directory you have just created, create another directory called polls, and within that create a file called index.html. In other words, your template should be at polls/templates/polls/index.html. Because of how the app_directories template loader works as described above, you can refer to this template within Django as polls/index.html.

```
Template namespacing

Now we might be able to get away with putting our templates directly in polls/templates (rather than creating another polls subdirectory), but it would actually be a bad idea. Django will choose the first template it finds whose name matches, and if you had a template with the same name in a different application, Django would be unable to distinguish between them. We need to be able to point Django at the right one, and the best way to ensure this is by namespacing them. That is, by putting those templates inside another directory named for the application itself.
```


Put the following code in that template:


```html
{% if latest_question_list %}
    <ul>
    {% for question in latest_question_list %}
        <li><a href="/polls/{{ question.id }}/">{{ question.question_text }}</a></li>
    {% endfor %}
    </ul>
{% else %}
    <p>No polls are available.</p>
{% endif %}
```
Note: To make the tutorial shorter, all template examples use incomplete HTML. In your own projects you should use complete HTML documents.

Now let’s update our index view in polls/views.py to use the template:

```python
from django.http import HttpResponse
from django.template import loader

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    template = loader.get_template('polls/index.html')
    context = {
        'latest_question_list': latest_question_list,
    }
    return HttpResponse(template.render(context, request))
```
That code loads the template called polls/index.html and passes it a context. The context is a dictionary mapping template variable names to Python objects.

Load the page by pointing your browser at “/polls/”, and you should see a bulleted-list containing the “What’s up” question from that we previously added. The link points to the question’s detail page.

#### A shortcut: render()
It’s a very common idiom to load a template, fill a context and return an HttpResponse object with the result of the rendered template. Django provides a shortcut. Here’s the full index() view, rewritten:

```python
from django.shortcuts import render

from .models import Question


def index(request):
    latest_question_list = Question.objects.order_by('-pub_date')[:5]
    context = {'latest_question_list': latest_question_list}
    return render(request, 'polls/index.html', context)
```
Note that once we’ve done this in all these views, we no longer need to import loader and HttpResponse (you’ll want to keep HttpResponse if you still have the stub methods for detail, results, and vote).


The render() function takes the request object as its first argument, a template name as its second argument and a dictionary as its optional third argument. It returns an HttpResponse object of the given template rendered with the given context.

### Raising a 404 error

Now, let’s tackle the question detail view – the page that displays the question text for a given poll. Here’s the view:

```python
from django.http import Http404
from django.shortcuts import render

from .models import Question
# ...
def detail(request, question_id):
    try:
        question = Question.objects.get(pk=question_id)
    except Question.DoesNotExist:
        raise Http404("Question does not exist")
    return render(request, 'polls/detail.html', {'question': question})
```
The new concept here: The view raises the Http404 exception if a question with the requested ID doesn’t exist.

We’ll discuss what you could put in that polls/detail.html template a bit later, but if you’d like to quickly get the above example working, a file containing just:

```html
{{ question }}
```
#### A shortcut: get_object_or_404()
It’s a very common idiom to use get() and raise Http404 if the object doesn’t exist. Django provides a shortcut. Here’s the detail() view, rewritten:

```python
from django.shortcuts import get_object_or_404, render

from .models import Question
# ...
def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/detail.html', {'question': question})
```

The get_object_or_404() function takes a Django model as its first argument and an arbitrary number of keyword arguments, which it passes to the get() function of the model’s manager. It raises Http404 if the object doesn’t exist.


```
Philosophy

Why do we use a helper function get_object_or_404() instead of automatically catching the ObjectDoesNotExist exceptions at a higher level, or having the model API raise Http404 instead of ObjectDoesNotExist?

Because that would couple the model layer to the view layer. One of the foremost design goals of Django is to maintain loose coupling. Some controlled coupling is introduced in the django.shortcuts module.
```

There’s also a get_list_or_404() function, which works just as get_object_or_404() – except using filter() instead of get(). It raises Http404 if the list is empty.

### Use the template system
Back to the detail() view for our poll application. Given the context variable question, here’s what the polls/detail.html template might look like:
```html
<h1>{{ question.question_text }}</h1>
<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }}</li>
{% endfor %}
</ul>
```
The template system uses dot-lookup syntax to access variable attributes. In the example of {{ question.question_text }}, first Django does a dictionary lookup on the object question. Failing that, it tries an attribute lookup – which works, in this case. If attribute lookup had failed, it would’ve tried a list-index lookup.

Method-calling happens in the {% for %} loop: question.choice_set.all is interpreted as the Python code question.choice_set.all(), which returns an iterable of Choice objects and is suitable for use in the {% for %} tag.

### Removing hardcoded URLs in templates
The problem with this hardcoded, tightly-coupled approach is that it becomes challenging to change URLs on projects with a lot of templates. However, since you defined the name argument in the path() functions in the polls.urls module, you can remove a reliance on specific URL paths defined in your url configurations by using the {% url %} template tag:

```html
<li><a href="{% url 'detail' question.id %}">{{ question.question_text }}</a></li>
```

The way this works is by looking up the URL definition as specified in the polls.urls module. You can see exactly where the URL name of ‘detail’ is defined below:

```python
path('<int:question_id>/', views.detail, name='detail'),
```

If you want to change the URL of the polls detail view to something else, perhaps to something like polls/specifics/12/ instead of doing it in the template (or templates) you would change it in polls/urls.py:

```python
# added the word 'specifics'
path('specifics/<int:question_id>/', views.detail, name='detail'),
```
### Namespacing URL names
The tutorial project has just one app, polls. In real Django projects, there might be five, ten, twenty apps or more. How does Django differentiate the URL names between them? For example, the polls app has a detail view, and so might an app on the same project that is for a blog. How does one make it so that Django knows which app view to create for a url when using the {% url %} template tag?

The answer is to add namespaces to your URLconf. In the polls/urls.py file, go ahead and add an app_name to set the application namespace:

```python
from django.urls import path

from . import views

app_name = 'polls'
urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail'),
    path('<int:question_id>/results/', views.results, name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```

Now change your polls/index.html template to:

```html
<li><a href="{% url 'polls:detail' question.id %}">{{ question.question_text }}</a></li>
```

### Write a minimal form
Let’s update our poll detail template (“polls/detail.html”) from the last tutorial, so that the template contains an HTML <form> element:
```html
<form action="{% url 'polls:vote' question.id %}" method="post">
{% csrf_token %}
<fieldset>
    <legend><h1>{{ question.question_text }}</h1></legend>
    {% if error_message %}<p><strong>{{ error_message }}</strong></p>{% endif %}
    {% for choice in question.choice_set.all %}
        <input type="radio" name="choice" id="choice{{ forloop.counter }}" value="{{ choice.id }}">
        <label for="choice{{ forloop.counter }}">{{ choice.choice_text }}</label><br>
    {% endfor %}
</fieldset>
<input type="submit" value="Vote">
</form>
```
A quick rundown:

* The above template displays a radio button for each question choice. The value of each radio button is the associated question choice’s ID. The name of each radio button is "choice". That means, when somebody selects one of the radio buttons and submits the form, it’ll send the POST data choice=# where # is the ID of the selected choice. This is the basic concept of HTML forms.
* We set the form’s action to {% url 'polls:vote' question.id %}, and we set method="post". Using method="post" (as opposed to method="get") is very important, because the act of submitting this form will alter data server-side. Whenever you create a form that alters data server-side, use method="post". This tip isn’t specific to Django; it’s good web development practice in general.
* forloop.counter indicates how many times the for tag has gone through its loop
* Since we’re creating a POST form (which can have the effect of modifying data), we need to worry about Cross Site Request Forgeries. Thankfully, you don’t have to worry too hard, because Django comes with a helpful system for protecting against it. In short, all POST forms that are targeted at internal URLs should use the {% csrf_token %} template tag.

Date: 21 Aug 2022

-----------------

Now, let’s create a Django view that handles the submitted data and does something with it. Remember, Previously, we created a URLconf for the polls application that includes this line:

```python
path('<int:question_id>/vote/', views.vote, name='vote'),
```

We also created a dummy implementation of the vote() function. Let’s create a real version. Add the following to polls/views.py:

```python
from django.http import HttpResponse, HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse

from .models import Choice, Question
# ...
def vote(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    try:
        selected_choice = question.choice_set.get(pk=request.POST['choice'])
    except (KeyError, Choice.DoesNotExist):
        # Redisplay the question voting form.
        return render(request, 'polls/detail.html', {
            'question': question,
            'error_message': "You didn't select a choice.",
        })
    else:
        selected_choice.votes += 1
        selected_choice.save()
        # Always return an HttpResponseRedirect after successfully dealing
        # with POST data. This prevents data from being posted twice if a
        # user hits the Back button.
        return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```
This code includes a few things we haven’t covered yet in this tutorial:



* request.POST is a dictionary-like object that lets you access submitted data by key name. In this case, request.POST['choice'] returns the ID of the selected choice, as a string. request.POST values are always strings. *Note that Django also provides request.GET for accessing GET data in the same way – but we’re explicitly using request.POST in our code, to ensure that data is only altered via a POST call.*
  
* request.POST['choice'] will raise KeyError if choice wasn’t provided in POST data. The above code checks for KeyError and redisplays the question form with an error message if choice isn’t given.

* After incrementing the choice count, the code returns an HttpResponseRedirect rather than a normal HttpResponse. HttpResponseRedirect takes a single argument: the URL to which the user will be redirected (see the following point for how we construct the URL in this case). As the Python comment above points out, you should always return an HttpResponseRedirect after successfully dealing with POST data. This tip isn’t specific to Django; it’s good web development practice in general.

* We are using the reverse() function in the HttpResponseRedirect constructor in this example. This function helps avoid having to hardcode a URL in the view function. It is given the name of the view that we want to pass control to and the variable portion of the URL pattern that points to that view. In this case, using the URLconf we set up in Tutorial 3, this reverse() call will return a string like
  
  ```html
  '/polls/3/results/'
  ```
where the 3 is the value of question.id. This redirected URL will then call the 'results' view to display the final page.

Ref HttpRequest : https://docs.djangoproject.com/en/4.1/ref/request-response/

After somebody votes in a question, the vote() view redirects to the results page for the question. Let’s write that view:

```python
from django.shortcuts import get_object_or_404, render


def results(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    return render(request, 'polls/results.html', {'question': question})
```

This is almost exactly the same as the detail() view from Previous Tutorial. The only difference is the template name. We’ll fix this redundancy later.


Now, create a polls/results.html template:

```html
<h1>{{ question.question_text }}</h1>

<ul>
{% for choice in question.choice_set.all %}
    <li>{{ choice.choice_text }} -- {{ choice.votes }} vote{{ choice.votes|pluralize }}</li>
{% endfor %}
</ul>

<a href="{% url 'polls:detail' question.id %}">Vote again?</a>
```

Now, go to /polls/1/ in your browser and vote in the question. You should see a results page that gets updated each time you vote. If you submit the form without having chosen a choice, you should see the error message.


Note : 

*The code for our vote() view does have a small problem. It first gets the selected_choice object from the database, then computes the new value of votes, and then saves it back to the database. If two users of your website try to vote at exactly the same time, this might go wrong: The same value, let’s say 42, will be retrieved for votes. Then, for both users the new value of 43 is computed and saved, but 44 would be the expected value.

This is called a race condition. If you are interested, you can read Avoiding race conditions using F() to learn how you can solve this issue : https://docs.djangoproject.com/en/4.1/ref/models/expressions/#avoiding-race-conditions-using-f . *

### Use generic views: Less code is better
The detail() (from Previous Tutorial) and results() views are very short – and, as mentioned above, redundant. The index() view, which displays a list of polls, is similar.

These views represent a common case of basic web development: getting data from the database according to a parameter passed in the URL, loading a template and returning the rendered template. Because this is so common, Django provides a shortcut, called the “generic views” system.

Generic views abstract common patterns to the point where you don’t even need to write Python code to write an app.

Let’s convert our poll app to use the generic views system, so we can delete a bunch of our own code. We’ll have to take a few steps to make the conversion. We will:

* Convert the URLconf.
* Delete some of the old, unneeded views.
* Introduce new views based on Django’s generic views.

```
Why the code-shuffle?

Generally, when writing a Django app, you’ll evaluate whether generic views are a good fit for your problem, and you’ll use them from the beginning, rather than refactoring your code halfway through. But this tutorial intentionally has focused on writing the views “the hard way” until now, to focus on core concepts.

You should know basic math before you start using a calculator.
```

#### Amend URLconf
First, open the polls/urls.py URLconf and change it like so:

```python
from django.urls import path

from . import views

app_name = 'polls'
urlpatterns = [
    path('', views.IndexView.as_view(), name='index'),
    path('<int:pk>/', views.DetailView.as_view(), name='detail'),
    path('<int:pk>/results/', views.ResultsView.as_view(), name='results'),
    path('<int:question_id>/vote/', views.vote, name='vote'),
]
```
Note that the name of the matched pattern in the path strings of the second and third patterns has changed from <question_id> to <pk>.

#### Amend views
Next, we’re going to remove our old index, detail, and results views and use Django’s generic views instead. To do so, open the polls/views.py file and change it like so:

```python
from django.http import HttpResponseRedirect
from django.shortcuts import get_object_or_404, render
from django.urls import reverse
from django.views import generic

from .models import Choice, Question


class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'

    def get_queryset(self):
        """Return the last five published questions."""
        return Question.objects.order_by('-pub_date')[:5]


class DetailView(generic.DetailView):
    model = Question
    template_name = 'polls/detail.html'


class ResultsView(generic.DetailView):
    model = Question
    template_name = 'polls/results.html'


def vote(request, question_id):
    ... # same as above, no changes needed.
```

Just for ref, below is the old code

```python
# from audioop import reverse
# from re import template
# import re
# from urllib import response
# from django.http import HttpResponse, HttpResponseRedirect
# from .models import Question, Choice
# from django.template import loader
# from django.http import Http404
# from django.shortcuts import render, get_object_or_404
# from django.urls import reverse


# def index(request):
#     latest_question_list = Question.objects.order_by('-pub_date')[:5]
#     template = loader.get_template('polls/index.html')
#     context = {
#         'latest_question_list': latest_question_list}
#     return HttpResponse(template.render(context, request))


# def detail(request, question_id):
#     question = get_object_or_404(Question, pk=question_id)
#     return render(request, 'polls/detail.html', {'question': question})


# def results(request, question_id):
#     question=get_object_or_404(Question, pk = question_id)
#     return render(request, 'polls/results.html', {'question': question})


# def vote(request, question_id):
#     question = get_object_or_404(Question, pk=question_id)
#     try:
#         selected_choice = question.choice_set.get(pk=request.POST['choice'])
#     except (KeyError, Choice.DoesNotExist):
#         return render(request, 'polls/detail.html', {
#             "question": question,
#             "error_message": "You Didn't Select a choice"
#         })
#     else:
#         selected_choice.votes += 1
#         selected_choice.save()
#         # Always return an HttpResponseRedirect after successfully dealing
#         # with post data. This prevents data from being posted twice if a user hits a back button
#         return HttpResponseRedirect(reverse('polls:results', args=(question.id,)))
```

We’re using two generic views here: ListView and DetailView. Respectively, those two views abstract the concepts of “display a list of objects” and “display a detail page for a particular type of object.”

* Each generic view needs to know what model it will be acting upon. This is provided using the model attribute.
* The DetailView generic view expects the primary key value captured from the URL to be called "pk", so we’ve changed question_id to pk for the generic views.

By default, the *DetailView* generic view uses a template called `<app name>/<model name>_detail.html`. In our case, it would use the template "`polls/question_detail.html`". The `template_name` attribute is used to tell Django to use a specific template name instead of the autogenerated default template name. We also specify the `template_name` for the results list view – this ensures that the results view and the detail view have a different appearance when rendered, even though they’re both a DetailView behind the scenes.


Similarly, the *ListView* generic view uses a default template called `<app name>/<model name>_list.html;` we use template_name to tell *ListView* to use our existing "`polls/index.html`" template.


In previous parts of the tutorial, the templates have been provided with a context that contains the question and latest_question_list context variables. For DetailView the question variable is provided automatically – since we’re using a Django model (Question), Django is able to determine an appropriate name for the context variable. However, for ListView, the automatically generated context variable is question_list. To override this we provide the context_object_name attribute, specifying that we want to use latest_question_list instead. As an alternative approach, you could change your templates to match the new default context variables – but it’s a lot easier to tell Django to use the variable you want.

Run the server, and use your new polling app based on generic views.

Date: 22 Aug 2022

----------------
## Testing the code : Introducing automated testing

Tests are routines that check the operation of your code.

### Why you need to create tests
You may feel that you have quite enough on your plate just learning Python/Django, and having yet another thing to learn and do may seem overwhelming and perhaps unnecessary. After all, our polls application is working quite happily now; going through the trouble of creating automated tests is not going to make it work any better. If creating the polls application is the last bit of Django programming you will ever do, then true, you don’t need to know how to create automated tests. But, if that’s not the case, now is an excellent time to learn.

#### Tests will save you time
Up to a certain point, ‘checking that it seems to work’ will be a satisfactory test. In a more sophisticated application, you might have dozens of complex interactions between components.

A change in any of those components could have unexpected consequences on the application’s behavior. Checking that it still ‘seems to work’ could mean running through your code’s functionality with twenty different variations of your test data to make sure you haven’t broken something - not a good use of your time.

That’s especially true when automated tests could do this for you in seconds. If something’s gone wrong, tests will also assist in identifying the code that’s causing the unexpected behavior.

Sometimes it may seem a chore to tear yourself away from your productive, creative programming work to face the unglamorous and unexciting business of writing tests, particularly when you know your code is working properly.

However, the task of writing tests is a lot more fulfilling than spending hours testing your application manually or trying to identify the cause of a newly-introduced problem.

#### Tests don’t just identify problems, they prevent them
It’s a mistake to think of tests merely as a negative aspect of development.

Without tests, the purpose or intended behavior of an application might be rather opaque. Even when it’s your own code, you will sometimes find yourself poking around in it trying to find out what exactly it’s doing.

Tests change that; they light up your code from the inside, and when something goes wrong, they focus light on the part that has gone wrong - even if you hadn’t even realized it had gone wrong.

#### Tests make your code more attractive
You might have created a brilliant piece of software, but you will find that many other developers will refuse to look at it because it lacks tests; without tests, they won’t trust it. Jacob Kaplan-Moss, one of Django’s original developers, says *“Code without tests is broken by design.”*

#### Tests help teams work together
The previous points are written from the point of view of a single developer maintaining an application. Complex applications will be maintained by teams. Tests guarantee that colleagues don’t inadvertently break your code (and that you don’t break theirs without knowing). If you want to make a living as a Django programmer, you must be good at writing tests!

#### Basic testing strategies
Some programmers follow a discipline called “test-driven development”; they actually write their tests before they write their code. This might seem counter-intuitive, but in fact it’s similar to what most people will often do anyway: they describe a problem, then create some code to solve it. Test-driven development formalizes the problem in a Python test case.


More often, a newcomer to testing will create some code and later decide that it should have some tests. Perhaps it would have been better to write some tests earlier, but it’s never too late to get started.

Sometimes it’s difficult to figure out where to get started with writing tests. If you have written several thousand lines of Python, choosing something to test might not be easy. In such a case, it’s fruitful to write your first test the next time you make a change, either when you add a new feature or fix a bug.

### Writing our first test

#### We identify a bug

Fortunately, there’s a little bug in the polls application for us to fix right away: the Question.was_published_recently() method returns True if the Question was published within the last day (which is correct) but also if the Question’s pub_date field is in the future (which certainly isn’t).

Confirm the bug by using the shell to check the method on a question whose date lies in the future:

```bash
>>> import datetime
>>> from django.utils import timezone
>>> from polls.models import Question
>>> # create a Question instance with pub_date 30 days in the future
>>> future_question = Question(pub_date=timezone.now() + datetime.timedelta(days=30))
>>> # was it published recently?
>>> future_question.was_published_recently()
True
```
Since things in the future are not ‘recent’, this is clearly wrong.


#### Create a test to expose the bug

A conventional place for an application’s tests is in the application’s tests.py file; the *testing system will automatically find tests in any file whose name begins with test*.

Put the following in the tests.py file in the polls application:

```python
import datetime

from django.test import TestCase
from django.utils import timezone

from .models import Question


class QuestionModelTests(TestCase):

    def test_was_published_recently_with_future_question(self):
        """
        was_published_recently() returns False for questions whose pub_date
        is in the future.
        """
        time = timezone.now() + datetime.timedelta(days=30)
        future_question = Question(pub_date=time)
        self.assertIs(future_question.was_published_recently(), False)
```

Here we have created a django.test.TestCase subclass with a method that creates a Question instance with a pub_date in the future. We then check the output of was_published_recently() - which ought to be False.


#### Running tests

In the terminal, we can run our test:

```
py manage.py test polls
```
Output:
```
Found 1 test(s).
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
F
======================================================================
FAIL: test_was_published_recently_with_future_question (polls2.tests.QuestionModelTests)
was_published_recently() returns False for future Questions, Whose pub_date is in the future.
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/home/aneesh/git/gitr/PythonTraining/mypollingwebapp/polls2/tests.py", line 17, in test_was_published_recently_with_future_question
    self.assertIs(future_question.was_published_recently(),False)
AssertionError: True is not False

----------------------------------------------------------------------
Ran 1 test in 0.000s

FAILED (failures=1)
Destroying test database for alias 'default'..
```

```
Different error?

If instead you’re getting a NameError here, you may have missed a step in Part 2 where we added imports of datetime and timezone to polls/models.py. Copy the imports from that section, and try running your tests again.
```
What happened is this:

* manage.py test polls looked for tests in the polls application
* it found a subclass of the django.test.TestCase class
* it created a special database for the purpose of testing
* it looked for test methods - ones whose names begin with test
* in test_was_published_recently_with_future_question it created a Question instance whose pub_date field is 30 days in the future
* … and using the assertIs() method, it discovered that its was_published_recently() returns True, though we wanted it to return False

The test informs us which test failed and even the line on which the failure occurred.


#### Fixing the bug
We already know what the problem is: Question.was_published_recently() should return False if its pub_date is in the future. Amend the method in models.py, so that it will only return True if the date is also in the past:

```python
def was_published_recently(self):
    now = timezone.now()
    return now - datetime.timedelta(days=1) <= self.pub_date <= now
```
and run the test again:

```
Creating test database for alias 'default'...
System check identified no issues (0 silenced).
.
----------------------------------------------------------------------
Ran 1 test in 0.001s

OK
Destroying test database for alias 'default'...
```
After identifying a bug, we wrote a test that exposes it and corrected the bug in the code so our test passes.

Many other things might go wrong with our application in the future, but we can be sure that we won’t inadvertently reintroduce this bug, because running the test will warn us immediately. We can consider this little portion of the application pinned down safely forever.

### More comprehensive tests
While we’re here, we can further pin down the was_published_recently() method; in fact, it would be positively embarrassing if in fixing one bug we had introduced another.

Add two more test methods to the same class, to test the behavior of the method more comprehensively:

```python
def test_was_published_recently_with_old_question(self):
    """
    was_published_recently() returns False for questions whose pub_date
    is older than 1 day.
    """
    time = timezone.now() - datetime.timedelta(days=1, seconds=1)
    old_question = Question(pub_date=time)
    self.assertIs(old_question.was_published_recently(), False)

def test_was_published_recently_with_recent_question(self):
    """
    was_published_recently() returns True for questions whose pub_date
    is within the last day.
    """
    time = timezone.now() - datetime.timedelta(hours=23, minutes=59, seconds=59)
    recent_question = Question(pub_date=time)
    self.assertIs(recent_question.was_published_recently(), True)
```
And now we have three tests that confirm that Question.was_published_recently() returns sensible values for past, recent, and future questions.

Again, polls is a minimal application, but however complex it grows in the future and whatever other code it interacts with, we now have some guarantee that the method we have written tests for will behave in expected ways.



### Test a view
The polls application is fairly undiscriminating: it will publish any question, including ones whose pub_date field lies in the future. We should improve this. Setting a pub_date in the future should mean that the Question is published at that moment, but invisible until then.

#### A test for a view
When we fixed the bug above, we wrote the test first and then the code to fix it. In fact that was an example of test-driven development, but it doesn’t really matter in which order we do the work.

In our first test, we focused closely on the internal behavior of the code. For this test, we want to check its behavior as it would be experienced by a user through a web browser.


Date : 23 Aug 2022 

------------------
#### The Django test client
Django provides a test Client to simulate a user interacting with the code at the view level. We can use it in tests.py or even in the shell.

We will start again with the shell, where we need to do a couple of things that won’t be necessary in tests.py. The first is to set up the test environment in the shell:

```
$ python manage.py shell
```
```python
>>> from django.test.utils import setup_test_environment
>>> setup_test_environment()
```

setup_test_environment() installs a template renderer which will allow us to examine some additional attributes on responses such as response.context that otherwise wouldn’t be available. Note that this method does not set up a test database, so the following will be run against the existing database and the output may differ slightly depending on what questions you already created. You might get unexpected results if your TIME_ZONE in settings.py isn’t correct. If you don’t remember setting it earlier, check it before continuing.

Next we need to import the test client class (later in tests.py we will use the django.test.TestCase class, which comes with its own client, so this won’t be required):


```python
>>> from django.test import Client
>>> # create an instance of the client for our use
>>> client = Client()
```

With that ready, we can ask the client to do some work for us:



```python
>>> # get a response from '/'
>>> response = client.get('/')
Not Found: /
>>> # we should expect a 404 from that address; if you instead see an
>>> # "Invalid HTTP_HOST header" error and a 400 response, you probably
>>> # omitted the setup_test_environment() call described earlier.
>>> response.status_code
404
>>> # on the other hand we should expect to find something at '/polls/'
>>> # we'll use 'reverse()' rather than a hardcoded URL
>>> from django.urls import reverse
>>> response = client.get(reverse('polls:index'))
>>> response.status_code
200
>>> response.content
b'\n    <ul>\n    \n        <li><a href="/polls/1/">What&#x27;s up?</a></li>\n    \n    </ul>\n\n'
>>> response.context['latest_question_list']
<QuerySet [<Question: What's up?>]>
```

### Improving our view

The list of polls shows polls that aren’t published yet (i.e. those that have a pub_date in the future). Let’s fix that.

We need to amend the get_queryset() method and change it so that it also checks the date by comparing it with timezone.now(). First we need to add an import:

```python
#views.py
def get_queryset(self):
    """
    Return the last five published questions (not including those set to be
    published in the future).
    """
    return Question.objects.filter(
        pub_date__lte=timezone.now()
    ).order_by('-pub_date')[:5]
```

== Question.objects.filter(pub_date__lte=timezone.now()) == returns a queryset containing Questions whose pub_date is less than or equal to - that is, earlier than or equal to - timezone.now.

### Testing our new view
Now you can satisfy yourself that this behaves as expected by firing up runserver, loading the site in your browser, creating Questions with dates in the past and future, and checking that only those that have been published are listed. You don’t want to have to do that every single time you make any change that might affect this - so let’s also create a test, based on our shell session above.

Add the following to polls/tests.py:


```
from django.urls import reverse
```

and we’ll create a shortcut function to create questions as well as a new test class:

```python

def create_question(question_text, days):
    """
    Create a question with the given `question_text` and published the
    given number of `days` offset to now (negative for questions published
    in the past, positive for questions that have yet to be published).
    """
    time = timezone.now() + datetime.timedelta(days=days)
    return Question.objects.create(question_text=question_text, pub_date=time)


class QuestionIndexViewTests(TestCase):
    def test_no_questions(self):
        """
        If no questions exist, an appropriate message is displayed.
        """
        response = self.client.get(reverse('polls:index'))
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, "No polls are available.")
        self.assertQuerysetEqual(response.context['latest_question_list'], [])

    def test_past_question(self):
        """
        Questions with a pub_date in the past are displayed on the
        index page.
        """
        question = create_question(question_text="Past question.", days=-30)
        response = self.client.get(reverse('polls:index'))
        self.assertQuerysetEqual(
            response.context['latest_question_list'],
            [question],
        )

    def test_future_question(self):
        """
        Questions with a pub_date in the future aren't displayed on
        the index page.
        """
        create_question(question_text="Future question.", days=30)
        response = self.client.get(reverse('polls:index'))
        self.assertContains(response, "No polls are available.")
        self.assertQuerysetEqual(response.context['latest_question_list'], [])

    def test_future_question_and_past_question(self):
        """
        Even if both past and future questions exist, only past questions
        are displayed.
        """
        question = create_question(question_text="Past question.", days=-30)
        create_question(question_text="Future question.", days=30)
        response = self.client.get(reverse('polls:index'))
        self.assertQuerysetEqual(
            response.context['latest_question_list'],
            [question],
        )

    def test_two_past_questions(self):
        """
        The questions index page may display multiple questions.
        """
        question1 = create_question(question_text="Past question 1.", days=-30)
        question2 = create_question(question_text="Past question 2.", days=-5)
        response = self.client.get(reverse('polls:index'))
        self.assertQuerysetEqual(
            response.context['latest_question_list'],
            [question2, question1],
        )
```

Let’s look at some of these more closely.

First is a question shortcut function, **create_question**, to take some repetition out of the process of creating questions.

**test_no_questions** doesn’t create any questions, but checks the message: “No polls are available.” and verifies the **latest_question_list** is empty. Note that the **django.test.TestCase** class provides some additional assertion methods. In these examples, we use **assertContains()** and **assertQuerysetEqual()**.

In **test_past_question**, we create a question and verify that it appears in the list.

In **test_future_question**, we create a question with a **pub_date** in the future. The database is reset for each test method, so the first question is no longer there, and so again the index shouldn’t have any questions in it.

And so on. In effect, we are using the tests to tell a story of admin input and user experience on the site, and checking that at every state and for every new change in the state of the system, the expected results are published.

### Testing the DetailView
What we have works well; however, even though future questions don’t appear in the index, users can still reach them if they know or guess the right URL. So we need to add a similar constraint to DetailView:

```python
class DetailView(generic.DetailView):
    ...
    def get_queryset(self):
        """
        Excludes any questions that aren't published yet.
        """
        return Question.objects.filter(pub_date__lte=timezone.now())
```
We should then add some tests, to check that a **Question** whose **pub_date** is in the past can be displayed, and that one with a **pub_date** in the future is not:

```python
class QuestionDetailViewTests(TestCase):
    def test_future_question(self):
        """
        The detail view of a question with a pub_date in the future
        returns a 404 not found.
        """
        future_question = create_question(question_text='Future question.', days=5)
        url = reverse('polls:detail', args=(future_question.id,))
        response = self.client.get(url)
        self.assertEqual(response.status_code, 404)

    def test_past_question(self):
        """
        The detail view of a question with a pub_date in the past
        displays the question's text.
        """
        past_question = create_question(question_text='Past Question.', days=-5)
        url = reverse('polls:detail', args=(past_question.id,))
        response = self.client.get(url)
        self.assertContains(response, past_question.question_text)
```

### Ideas for more tests

We ought to add a similar **get_queryset** method to **ResultsView** and create a new test class for that view. It’ll be very similar to what we have just created; in fact there will be a lot of repetition.

We could also improve our application in other ways, adding tests along the way. For example, it’s silly that **Questions** can be published on the site that have no **Choices**. So, our views could check for this, and exclude such **Questions**. Our tests would create a **Question** without **Choices** and then test that it’s not published, as well as create a similar **Question** with **Choices**, and test that it is published.

Perhaps logged-in admin users should be allowed to see unpublished **Questions**, but not ordinary visitors. Again: whatever needs to be added to the software to accomplish this should be accompanied by a test, whether you write the test first and then make the code pass the test, or work out the logic in your code first and then write a test to prove it.

At a certain point you are bound to look at your tests and wonder whether your code is suffering from test bloat, which brings us to:


#### When testing, more is better
It might seem that our tests are growing out of control. At this rate there will soon be more code in our tests than in our application, and the repetition is unaesthetic, compared to the elegant conciseness of the rest of our code.

**It doesn’t matter**. Let them grow. For the most part, you can write a test once and then forget about it. It will continue performing its useful function as you continue to develop your program.

Sometimes tests will need to be updated. Suppose that we amend our views so that only **Questions** with **Choices** are published. In that case, many of our existing tests will fail - telling us exactly which tests need to be amended to bring them up to date, so to that extent tests help look after themselves.

At worst, as you continue developing, you might find that you have some tests that are now redundant. Even that’s not a problem; in testing redundancy is a good thing.

As long as your tests are sensibly arranged, they won’t become unmanageable. Good rules-of-thumb include having:

* a separate **TestClass** for each model or view
* a separate test method for each set of conditions you want to test
* test method names that describe their function

#### Further testing

This tutorial only introduces some of the basics of testing. There’s a great deal more you can do, and a number of very useful tools at your disposal to achieve some very clever things.

For example, while our tests here have covered some of the internal logic of a model and the way our views publish information, you can use an “in-browser” framework such as Selenium to test the way your HTML actually renders in a browser. These tools allow you to check not just the behavior of your Django code, but also, for example, of your JavaScript. It’s quite something to see the tests launch a browser, and start interacting with your site, as if a human being were driving it! Django includes LiveServerTestCase to facilitate integration with tools like Selenium.

If you have a complex application, you may want to run tests automatically with every commit for the purposes of [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration), so that quality control is itself - at least partially - automated.

A good way to spot untested parts of your application is to check code coverage. This also helps identify fragile or even dead code. If you can’t test a piece of code, it usually means that code should be refactored or removed. Coverage will help to identify dead code. See [Integration with coverage.py](https://docs.djangoproject.com/en/4.1/topics/testing/advanced/#topics-testing-code-coverage) for details.

[Testing in Django](https://docs.djangoproject.com/en/4.1/topics/testing/) has comprehensive information about testing.


## Handling Static Files
This tutorial begins where previous tutorial left off. We’ve built a tested web-poll application, and we’ll now add a stylesheet and an image.

Aside from the HTML generated by the server, web applications generally need to serve additional files — such as images, JavaScript, or CSS — necessary to render the complete web page. In Django, we refer to these files as **“static files”.**

For small projects, this isn’t a big deal, because you can keep the static files somewhere your web server can find it. However, in bigger projects – especially those comprised of multiple apps – dealing with the multiple sets of static files provided by each application starts to get tricky.

That’s what **django.contrib.staticfiles** is for: it collects static files from each of your applications (and any other places you specify) into a single location that can easily be served in production.

Ref : https://docs.djangoproject.com/en/4.1/faq/help/


### Customize your app’s look and feel

First, create a directory called **static** in your **polls** directory. Django will look for static files there, similarly to how Django finds templates inside **polls/templates/**.

Django’s **STATICFILES_FINDERS** setting contains a list of finders that know how to discover static files from various sources. One of the defaults is **AppDirectoriesFinder** which looks for a **“static”** subdirectory in each of the **INSTALLED_APPS**, like the one in polls we just created. The admin site uses the same directory structure for its static files.

Within the **static** directory you have just created, create another directory called **polls** and within that create a file called **style.css**. In other words, your stylesheet should be at **polls/static/polls/style.css**. Because of how the **AppDirectoriesFinder** staticfile finder works, you can refer to this static file in Django as **polls/style.css**, similar to how you reference the path for templates.

```
Static file namespacing

Just like templates, we might be able to get away with putting our static files directly in polls/static (rather than creating another polls subdirectory), but it would actually be a bad idea. Django will choose the first static file it finds whose name matches, and if you had a static file with the same name in a different application, Django would be unable to distinguish between them. We need to be able to point Django at the right one, and the best way to ensure this is by namespacing them. That is, by putting those static files inside another directory named for the application itself.

```


Put the following code in that stylesheet (polls/static/polls/style.css):

```css
li a {
    color: green;
}
```
Next, add the following at the top of polls/templates/polls/index.html:

```html
{% load static %}

<link rel="stylesheet" href="{% static 'polls/style.css' %}">
```
The `{% static %}` template tag generates the absolute URL of static files.

Reload http://localhost:8000/polls/ and you should see that the question links are green (Django style!) which means that your stylesheet was properly loaded.


### Adding a background-image
Next, we’ll create a subdirectory for images. Create an images subdirectory in the polls/static/polls/ directory. Inside this directory, add any image file that you’d like to use as a background. For the purposes of this tutorial, we’re using a file named background.png, which will have the full path polls/static/polls/images/background.png.

Then, add a reference to your image in your stylesheet (polls/static/polls/style.css):

```css
body {
    background: white url("images/background.png") no-repeat;
}
```
Reload http://localhost:8000/polls/ and you should see the background loaded in the top left of the screen.

```
Warning

The {% static %} template tag is not available for use in static files which aren’t generated by Django, like your stylesheet. You should always use relative paths to link your static files between each other, because then you can change STATIC_URL (used by the static template tag to generate its URLs) without having to modify a bunch of paths in your static files as well.
```

These are the basics. For more details on settings and other bits included with the framework see the [static files howto](https://docs.djangoproject.com/en/4.1/howto/static-files/) and the [staticfiles reference](https://docs.djangoproject.com/en/4.1/ref/contrib/staticfiles/). [Deploying static](https://docs.djangoproject.com/en/4.1/howto/static-files/deployment/) files discusses how to use static files on a real server.

Date : 24 Aug 2022

----------------
### Customize the admin form

By registering the Question model with admin.site.register(Question), Django was able to construct a default form representation. Often, you’ll want to customize how the admin form looks and works. You’ll do this by telling Django the options you want when you register the object.

Let’s see how this works by reordering the fields on the edit form. Replace the admin.site.register(Question) line with:

```python
from django.contrib import admin

from .models import Question


class QuestionAdmin(admin.ModelAdmin):
    fields = ['pub_date', 'question_text']

admin.site.register(Question, QuestionAdmin)
```
You’ll follow this pattern – create a model admin class, then pass it as the second argument to admin.site.register() – any time you need to change the admin options for a model.

This particular change above makes the “Publication date” come before the “Question” field:


This isn’t impressive with only two fields, but for admin forms with dozens of fields, choosing an intuitive order is an important usability detail.

And speaking of forms with dozens of fields, you might want to split the form up into fieldsets:

```python
from django.contrib import admin

from .models import Question


class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date']}),
    ]

admin.site.register(Question, QuestionAdmin)
```
OK, we have our Question admin page, but a Question has multiple Choices, and the admin page doesn’t display choices.

Yet.

There are two ways to solve this problem. The first is to register Choice with the admin just as we did with Question:

```python
from django.contrib import admin

from .models import Choice, Question
# ...
admin.site.register(Choice)
```
Now “Choices” is an available option in the Django admin. The “Add choice” form looks like this:

In that form, the “Question” field is a select box containing every question in the database. Django knows that a ForeignKey should be represented in the admin as a `<select>` box. In our case, only one question exists at this point.

Also note the “Add Another” link next to “Question.” Every object with a ForeignKey relationship to another gets this for free. When you click “Add Another”, you’ll get a popup window with the “Add question” form. If you add a question in that window and click “Save”, Django will save the question to the database and dynamically add it as the selected choice on the “Add choice” form you’re looking at.

But, really, this is an inefficient way of adding Choice objects to the system. It’d be better if you could add a bunch of Choices directly when you create the Question object. Let’s make that happen.


Remove the register() call for the Choice model. Then, edit the Question registration code to read:

```python
from django.contrib import admin

from .models import Choice, Question


class ChoiceInline(admin.StackedInline):
    model = Choice
    extra = 3


class QuestionAdmin(admin.ModelAdmin):
    fieldsets = [
        (None,               {'fields': ['question_text']}),
        ('Date information', {'fields': ['pub_date'], 'classes': ['collapse']}),
    ]
    inlines = [ChoiceInline]

admin.site.register(Question, QuestionAdmin)
```

This tells Django: “Choice objects are edited on the Question admin page. By default, provide enough fields for 3 choices.”


At the end of the three current slots you will find an “Add another Choice” link. If you click on it, a new slot will be added. If you want to remove the added slot, you can click on the X to the top right of the added slot. This image shows an added slot:

One small problem, though. It takes a lot of screen space to display all the fields for entering related Choice objects. For that reason, Django offers a tabular way of displaying inline related objects. To use it, change the ChoiceInline declaration to read:

```python
class ChoiceInline(admin.TabularInline):
    #...
```

### Customize the admin change list
Now that the Question admin page is looking good, let’s make some tweaks to the “change list” page – the one that displays all the questions in the system.

By default, Django displays the str() of each object. But sometimes it’d be more helpful if we could display individual fields. To do that, use the list_display admin option, which is a tuple of field names to display, as columns, on the change list page for the object:

```python
class QuestionAdmin(admin.ModelAdmin):
    # ...
    list_display = ('question_text', 'pub_date')
```
For good measure, let’s also include the was_published_recently() method

```python
class QuestionAdmin(admin.ModelAdmin):
    # ...
    list_display = ('question_text', 'pub_date', 'was_published_recently')
```
You can click on the column headers to sort by those values – except in the case of the was_published_recently header, because sorting by the output of an arbitrary method is not supported. Also note that the column header for was_published_recently is, by default, the name of the method (with underscores replaced with spaces), and that each line contains the string representation of the output.

You can improve that by using the display() decorator on that method (in polls/models.py), as follows:

```python
from django.contrib import admin

class Question(models.Model):
    # ...
    @admin.display(
        boolean=True,
        ordering='pub_date',
        description='Published recently?',
    )
    def was_published_recently(self):
        now = timezone.now()
        return now - datetime.timedelta(days=1) <= self.pub_date <= now
```
Ref : https://docs.djangoproject.com/en/4.1/ref/contrib/admin/#django.contrib.admin.ModelAdmin.list_display

Edit your polls/admin.py file again and add an improvement to the Question change list page: filters using the list_filter. Add the following line to QuestionAdmin:

list_filter = ['pub_date']

That adds a “Filter” sidebar that lets people filter the change list by the pub_date field:

The type of filter displayed depends on the type of field you’re filtering on. Because pub_date is a DateTimeField, Django knows to give appropriate filter options: “Any date”, “Today”, “Past 7 days”, “This month”, “This year”.


This is shaping up well. Let’s add some search capability:

```python
search_fields = ['question_text']
```
That adds a search box at the top of the change list. When somebody enters search terms, Django will search the question_text field. You can use as many fields as you’d like – although because it uses a LIKE query behind the scenes, limiting the number of search fields to a reasonable number will make it easier for your database to do the search.

Now’s also a good time to note that change lists give you free pagination. The default is to display 100 items per page. Change list pagination, search boxes, filters, date-hierarchies, and column-header-ordering all work together like you think they should.

### Customize the admin look and feel
Clearly, having “Django administration” at the top of each admin page is ridiculous. It’s just placeholder text.

You can change it, though, using Django’s template system. The Django admin is powered by Django itself, and its interfaces use Django’s own template system.


#### Customizing your project’s templates

Create a templates directory in your project directory (the one that contains manage.py). Templates can live anywhere on your filesystem that Django can access. (Django runs as whatever user your server runs.) However, keeping your templates within the project is a good convention to follow.

Open your settings file (mypollingwebapp /settings.py, remember) and add a DIRS option in the TEMPLATES setting:

```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```
DIRS is a list of filesystem directories to check when loading Django templates; it’s a search path.
```
Organizing templates

Just like the static files, we could have all our templates together, in one big templates directory, and it would work perfectly well. However, templates that belong to a particular application should be placed in that application’s template directory (e.g. polls/templates) rather than the project’s (templates). We’ll discuss in more detail in the reusable apps tutorial why we do this.
```

Now create a directory called admin inside templates, and copy the template admin/base_site.html from within the default Django admin template directory in the source code of Django itself (django/contrib/admin/templates) into that directory.


###### Where are the Django source files?

If you have difficulty finding where the Django source files are located on your system, run the following command:
```python
$ python -c "import django; print(django.__path__)"
```

Then, edit the file and replace \{\{ site_header\|default:_\('Django administration'\) \}\} \(including the curly braces\) with your own site’s name as you see fit. You should end up with a section of code like:
```html
{% block branding %}
<h1 id="site-name"><a href="{% url 'admin:index' %}">Polls Administration</a></h1>
{% endblock %}
```
We use this approach to teach you how to override templates. In an actual project, you would probably use the django.contrib.admin.AdminSite.site_header attribute to more easily make this particular customization.

This template file contains lots of text like {% block branding %} and {{ title }}. The {% and {{ tags are part of Django’s template language. When Django renders admin/base_site.html, this template language will be evaluated to produce the final HTML page, just like we saw in Tutorial 3.

Note that any of Django’s default admin templates can be overridden. To override a template, do the same thing you did with base_site.html – copy it from the default directory into your custom directory, and make changes.

### Customizing your application’s templates
Astute readers will ask: But if DIRS was empty by default, how was Django finding the default admin templates? The answer is that, since APP_DIRS is set to True, Django automatically looks for a templates/ subdirectory within each application package, for use as a fallback (don’t forget that django.contrib.admin is an application).

Our poll application is not very complex and doesn’t need custom admin templates. But if it grew more sophisticated and required modification of Django’s standard admin templates for some of its functionality, it would be more sensible to modify the application’s templates, rather than those in the project. That way, you could include the polls application in any new project and be assured that it would find the custom templates it needed.

See the [template loading documentation](https://docs.djangoproject.com/en/4.1/topics/templates/#template-loading) for more information about how Django finds its templates.

#### Customize the admin index page
On a similar note, you might want to customize the look and feel of the Django admin index page.

By default, it displays all the apps in INSTALLED_APPS that have been registered with the admin application, in alphabetical order. You may want to make significant changes to the layout. After all, the index is probably the most important page of the admin, and it should be easy to use.


The template to customize is admin/index.html. (Do the same as with admin/base_site.html in the previous section – copy it from the default directory to your custom template directory). Edit the file, and you’ll see it uses a template variable called app_list. That variable contains every installed Django app. Instead of using that, you can hard-code links to object-specific admin pages in whatever way you think is best.

Date : 25 Aug 2022

------------------
### Advanced Tutorial : How to write re usable apps

We’ll be turning our web-poll into a standalone Python package you can reuse in new projects and share with other people

#### Reusability matters

It’s a lot of work to design, build, test and maintain a web application. Many Python and Django projects share common problems. Wouldn’t it be great if we could save some of this repeated work?

Reusability is the way of life in Python. The [Python Package Index (PyPI)](https://pypi.org/) has a vast range of packages you can use in your own Python programs. Check out [Django Packages](https://djangopackages.org/) for existing reusable apps you could incorporate in your project. Django itself is also a normal Python package. This means that you can take existing Python packages or Django apps and compose them into your own web project. You only need to write the parts that make your project unique.

Let’s say you were starting a new project that needed a polls app like the one we’ve been working on. How do you make this app reusable? Luckily, you’re well on the way already. In Tutorial 1, we saw how we could decouple polls from the project-level URLconf using an include. In this tutorial, we’ll take further steps to make the app easy to use in new projects and ready to publish for others to install and use.

```
Package? App?
-----------

A Python package provides a way of grouping related Python code for easy reuse. A package contains one or more files of Python code (also known as “modules”).

A package can be imported with import foo.bar or from foo import bar. For a directory (like polls) to form a package, it must contain a special file __init__.py, even if this file is empty.

A Django application is a Python package that is specifically intended for use in a Django project. An application may use common Django conventions, such as having models, tests, urls, and views submodules.

Later on we use the term packaging to describe the process of making a Python package easy for others to install. It can be a little confusing, we know.
```

#### Your project and your reusable app

After the previous tutorials, our project should look like this:

```
mypollingwebapp /
    manage.py
    mypollingwebapp /
        __init__.py
        settings.py
        urls.py
        asgi.py
        wsgi.py
    polls/
        __init__.py
        admin.py
        apps.py
        migrations/
            __init__.py
            0001_initial.py
        models.py
        static/
            polls/
                images/
                    background.gif
                style.css
        templates/
            polls/
                detail.html
                index.html
                results.html
        tests.py
        urls.py
        views.py
    templates/
        admin/
            base_site.html
```

You created mypollingwebapp /templates and polls/templates in previous tutorials. Now perhaps it is clearer why we chose to have separate template directories for the project and application: everything that is part of the polls application is in polls. It makes the application self-contained and easier to drop into a new project.

The polls directory could now be copied into a new Django project and immediately reused. It’s not quite ready to be published though. For that, we need to package the app to make it easy for others to install.

#### Installing some prerequisites
The current state of Python packaging is a bit muddled with various tools. For this tutorial, we’re going to use [setuptools](https://pypi.org/project/setuptools/) to build our package. It’s the recommended packaging tool (merged with the **distribute** fork). We’ll also be using pip to install and uninstall it. You should install these two packages now. If you need help, you can refer to [how to install Django with pip](https://docs.djangoproject.com/en/4.1/topics/install/#installing-official-release). You can install setuptools the same way.

#### Packaging your app
Python packaging refers to preparing your app in a specific format that can be easily installed and used. Django itself is packaged very much like this. For a small app like polls, this process isn’t too difficult.

1. First, create a parent directory for polls, outside of your Django project. Call this directory django-polls.

```
Choosing a name for your app

When choosing a name for your package, check resources like PyPI to avoid naming conflicts with existing packages. It’s often useful to prepend django- to your module name when creating a package to distribute. This helps others looking for Django apps identify your app as Django specific.

Application labels (that is, the final part of the dotted path to application packages) must be unique in INSTALLED_APPS. Avoid using the same label as any of the Django contrib packages, for example auth, admin, or messages.
ref : https://docs.djangoproject.com/en/4.1/ref/contrib/ 
```
2. Move the polls directory into the django-polls directory.
3. Create a file django-polls/README.rst with the following contents:
```rst   
=====
Polls
=====

Polls is a Django app to conduct web-based polls. For each question,
visitors can choose between a fixed number of answers.

Detailed documentation is in the "docs" directory.

Quick start
-----------

1. Add "polls" to your INSTALLED_APPS setting like this::

    INSTALLED_APPS = [
        ...
        'polls',
    ]

2. Include the polls URLconf in your project urls.py like this::

    path('polls/', include('polls.urls')),

3. Run ``python manage.py migrate`` to create the polls models.

4. Start the development server and visit http://127.0.0.1:8000/admin/
   to create a poll (you'll need the Admin app enabled).

5. Visit http://127.0.0.1:8000/polls/ to participate in the poll.
```
4. Create a django-polls/LICENSE file. Choosing a license is beyond the scope of this tutorial, but suffice it to say that code released publicly without a license is useless. Django and many Django-compatible apps are distributed under the BSD license; however, you’re free to pick your own license. Just be aware that your licensing choice will affect who is able to use your code.
5. Next we’ll create **pyproject.toml**, **setup.cfg**, and **setup.py** files which detail how to build and install the app. A full explanation of these files is beyond the scope of this tutorial, but the [setuptools documentation](https://setuptools.pypa.io/en/latest/) has a good explanation. Create the django-polls/pyproject.toml, django-polls/setup.cfg, and django-polls/setup.py files with the following contents:

**django-polls/pyproject.toml**
```toml
[build-system]
requires = ['setuptools>=40.8.0', 'wheel']
build-backend = 'setuptools.build_meta:__legacy__'
```
**django-polls/setup.cfg**
```ini
[metadata]
name = django-polls
version = 0.1
description = A Django app to conduct web-based polls.
long_description = file: README.rst
url = https://www.example.com/
author = Your Name
author_email = yourname@example.com
license = BSD-3-Clause  # Example license
classifiers =
    Environment :: Web Environment
    Framework :: Django
    Framework :: Django :: X.Y  # Replace "X.Y" as appropriate
    Intended Audience :: Developers
    License :: OSI Approved :: BSD License
    Operating System :: OS Independent
    Programming Language :: Python
    Programming Language :: Python :: 3
    Programming Language :: Python :: 3 :: Only
    Programming Language :: Python :: 3.8
    Programming Language :: Python :: 3.9
    Topic :: Internet :: WWW/HTTP
    Topic :: Internet :: WWW/HTTP :: Dynamic Content

[options]
include_package_data = true
packages = find:
python_requires = >=3.8
install_requires =
    Django >= X.Y  # Replace "X.Y" as appropriate
```
**django-polls/setup.py**

```python
from setuptools import setup

setup()
```
6. Only Python modules and packages are included in the package by default. To include additional files, we’ll need to create a MANIFEST.in file. The setuptools docs referred to in the previous step discuss this file in more detail. To include the templates, the README.rst and our LICENSE file, create a file django-polls/MANIFEST.in with the following contents:

```in
include LICENSE
include README.rst
recursive-include polls/static *
recursive-include polls/templates *
```
7. It’s optional, but recommended, to include detailed documentation with your app. Create an empty directory django-polls/docs for future documentation. Add an additional line to django-polls/MANIFEST.in:

```
recursive-include docs *
```
Note that the docs directory won’t be included in your package unless you add some files to it. Many Django apps also provide their documentation online through sites like readthedocs.org.

8. Try building your package with **python setup.py sdist** (run from inside django-polls). This creates a directory called dist and builds your new package, django-polls-0.1.tar.gz.


#### Using your own package
Since we moved the polls directory out of the project, it’s no longer working. We’ll now fix this by installing our new django-polls package.

```
Installing as a user library

The following steps install django-polls as a user library. Per-user installs have a lot of advantages over installing the package system-wide, such as being usable on systems where you don’t have administrator access as well as preventing the package from affecting system services and other users of the machine.

Note that per-user installations can still affect the behavior of system tools that run as that user, so using a virtual environment is a more robust solution (see below).
```
1. To install the package, use pip
```
python -m pip install --user django-polls/dist/django-polls-0.1.tar.gz
```

2. With luck, your Django project should now work correctly again. Run the server again to confirm this.

