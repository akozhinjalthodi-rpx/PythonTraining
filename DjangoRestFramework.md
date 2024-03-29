# Python Django REST Framework
## Installation

```
python -m pip install djangorestframework
```

#### Creating a sample project
```
django-admin startproject resttutorial
```

#### Run Migration
```
python manage.py migrate
```

#### Create SuperUser
```
python manage.py createsuperuser
```

#### Create a new APP called "Snippets"
```
python manage.py startapp snippets
```

#### Modify Settings.py 
```ini
ALLOWED_HOSTS = [
    "127.0.0.1",
    "localhost"]


INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'rest_framework',
    'snippets',
]

```

#### Create a new mode inside snippets/models.py

```py
from django.db import models
from pygments.lexers import get_all_lexers
from pygments.styles import get_all_styles

LEXERS = [item for item in get_all_lexers() if item[1]]
LANGUAGE_CHOICES = sorted([(item[1][0], item[0]) for item in LEXERS])
STYLE_CHOICES = sorted([(item, item) for item in get_all_styles()])


class Snippet(models.Model):
    created = models.DateTimeField(auto_now_add=True)
    title = models.CharField(max_length=100, blank=True, default='')
    code = models.TextField()
    linenos = models.BooleanField(default=False)
    language = models.CharField(choices=LANGUAGE_CHOICES, default='python', max_length=100)
    style = models.CharField(choices=STYLE_CHOICES, default='friendly', max_length=100)

    class Meta:
        ordering = ['created']

```

#### Creating a Serializer class
Serializers Specify how to turn the model into payload data for REST

##### Create a new file snippets/serializers.py
```python
from rest_framework import serializers
from snippets.models import Snippet, LANGUAGE_CHOICES, STYLE_CHOICES


class SnippetSerializer(serializers.Serializer):
    id = serializers.IntegerField(read_only=True)
    title = serializers.CharField(required=False, allow_blank=True, max_length=100)
    code = serializers.CharField(style={'base_template': 'textarea.html'})
    linenos = serializers.BooleanField(required=False)
    language = serializers.ChoiceField(choices=LANGUAGE_CHOICES, default='python')
    style = serializers.ChoiceField(choices=STYLE_CHOICES, default='friendly')

    def create(self, validated_data):
        """
        Create and return a new `Snippet` instance, given the validated data.
        """
        return Snippet.objects.create(**validated_data)

    def update(self, instance, validated_data):
        """
        Update and return an existing `Snippet` instance, given the validated data.
        """
        instance.title = validated_data.get('title', instance.title)
        instance.code = validated_data.get('code', instance.code)
        instance.linenos = validated_data.get('linenos', instance.linenos)
        instance.language = validated_data.get('language', instance.language)
        instance.style = validated_data.get('style', instance.style)
        instance.save()
        return instance
```
The first part of the serializer class defines the fields that get serialized/deserialized. The `create()` and `update()` methods define how fully fledged instances are created or modified when calling `serializer.save()`

A serializer class is very similar to a Django Form class, and includes similar validation flags on the various fields, such as required, max_length and default.

The field flags can also control how the serializer should be displayed in certain circumstances, such as when rendering to HTML. The `{'base_template': 'textarea.html'}` flag above is equivalent to using widget=widgets.Textarea on a Django Form class. This is particularly useful for controlling how the browsable API should be displayed, as we'll see later in the tutorial.

We can actually also save ourselves some time by using the `ModelSerializer` class, as we'll see later, but for now we'll keep our serializer definition explicit.

##### Working with Serializers

```py
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from rest_framework.renderers import JSONRenderer
from rest_framework.parsers import JSONParser

snippet = Snippet(code='foo = "bar"\n')
snippet.save()

snippet = Snippet(code='print("hello, world")\n')
snippet.save()
```
We've now got a few snippet instances to play with. Let's take a look at serializing one of those instances.

```py
serializer = SnippetSerializer(snippet)
serializer.data
# {'id': 2, 'title': '', 'code': 'print("hello, world")\n', 'linenos': False, 'language': 'python', 'style': 'friendly'}
```
At this point we've translated the model instance into Python native datatypes. To finalize the serialization process we render the data into json.
```py
content = JSONRenderer().render(serializer.data)
content
# b'{"id": 2, "title": "", "code": "print(\\"hello, world\\")\\n", "linenos": false, "language": "python", "style": "friendly"}'
```
Deserialization is similar. First we parse a stream into Python native datatypes...

```py
import io

stream = io.BytesIO(content)
data = JSONParser().parse(stream)
```
...then we restore those native datatypes into a fully populated object instance.

```py
serializer = SnippetSerializer(data=data)
serializer.is_valid()
# True
serializer.validated_data
# OrderedDict([('title', ''), ('code', 'print("hello, world")\n'), ('linenos', False), ('language', 'python'), ('style', 'friendly')])
serializer.save()
# <Snippet: Snippet object>
```
We can also serialize querysets instead of model instances. To do so we simply add a many=True flag to the serializer arguments.

```py
serializer = SnippetSerializer(Snippet.objects.all(), many=True)
serializer.data
# [OrderedDict([('id', 1), ('title', ''), ('code', 'foo = "bar"\n'), ('linenos', False), ('language', 'python'), ('style', 'friendly')]), OrderedDict([('id', 2), ('title', ''), ('code', 'print("hello, world")\n'), ('linenos', False), ('language', 'python'), ('style', 'friendly')]), OrderedDict([('id', 3), ('title', ''), ('code', 'print("hello, world")'), ('linenos', False), ('language', 'python'), ('style', 'friendly')])]
```
#### Using ModelSerializers
```py
class SnippetSerializer(serializers.ModelSerializer):
    class Meta:
        model = Snippet
        fields = ['id', 'title', 'code', 'linenos', 'language', 'style']
```
One nice property that serializers have is that you can inspect all the fields in a serializer instance, by printing its representation. Open the Django shell with python manage.py shell, then try the following:

```py
from snippets.serializers import SnippetSerializer
serializer = SnippetSerializer()
print(repr(serializer))
# SnippetSerializer():
#    id = IntegerField(label='ID', read_only=True)
#    title = CharField(allow_blank=True, max_length=100, required=False)
#    code = CharField(style={'base_template': 'textarea.html'})
#    linenos = BooleanField(required=False)
#    language = ChoiceField(choices=[('Clipper', 'FoxPro'), ('Cucumber', 'Gherkin'), ('RobotFramework', 'RobotFramework'), ('abap', 'ABAP'), ('ada', 'Ada')...
#    style = ChoiceField(choices=[('autumn', 'autumn'), ('borland', 'borland'), ('bw', 'bw'), ('colorful', 'colorful')...
```
It's important to remember that ModelSerializer classes don't do anything particularly magical, they are simply a shortcut for creating serializer classes:

* An automatically determined set of fields.
* Simple default implementations for the create() and update() methods.


#### Writing regular Django views using our Serializer (views.py)

```py
from django.http import HttpResponse, JsonResponse
from django.views.decorators.csrf import csrf_exempt
from rest_framework.parsers import JSONParser
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer

@csrf_exempt
def snippet_list(request):
    """
    List all code snippets, or create a new snippet.
    """
    if request.method == 'GET':
        snippets = Snippet.objects.all()
        serializer = SnippetSerializer(snippets, many=True)
        return JsonResponse(serializer.data, safe=False)

    elif request.method == 'POST':
        data = JSONParser().parse(request)
        serializer = SnippetSerializer(data=data)
        if serializer.is_valid():
            serializer.save()
            return JsonResponse(serializer.data, status=201)
        return JsonResponse(serializer.errors, status=400)
```
Note that because we want to be able to POST to this view from clients that won't have a CSRF token we need to mark the view as `csrf_exempt`. This isn't something that you'd normally want to do, and REST framework views actually use more sensible behavior than this, but it'll do for our purposes right now.


We'll also need a view which corresponds to an individual snippet, and can be used to retrieve, update or delete the snippet.

```py
@csrf_exempt
def snippet_detail(request, pk):
    """
    Retrieve, update or delete a code snippet.
    """
    try:
        snippet = Snippet.objects.get(pk=pk)
    except Snippet.DoesNotExist:
        return HttpResponse(status=404)

    if request.method == 'GET':
        serializer = SnippetSerializer(snippet)
        return JsonResponse(serializer.data)

    elif request.method == 'PUT':
        data = JSONParser().parse(request)
        serializer = SnippetSerializer(snippet, data=data)
        if serializer.is_valid():
            serializer.save()
            return JsonResponse(serializer.data)
        return JsonResponse(serializer.errors, status=400)

    elif request.method == 'DELETE':
        snippet.delete()
        return HttpResponse(status=204)
```

Finally we need to wire these views up. Create the `snippets/urls.py` file:

```py
from django.urls import path
from snippets import views

urlpatterns = [
    path('snippets/', views.snippet_list),
    path('snippets/<int:pk>/', views.snippet_detail),
]
```
We also need to wire up the root urlconf, in the tutorial/urls.py file, to include our snippet app's URLs.


```py
from django.urls import path, include

urlpatterns = [
    path('', include('snippets.urls')),
]
```
#### Testing our first attempt at a Web API
We can test our API using curl or httpie. Httpie is a user friendly http client that's written in Python. Let's install that.

You can install httpie using pip:
```sh
pip install httpie
```
```bash
http http://127.0.0.1:8000/snippets/

HTTP/1.1 200 OK
...
[
  {
    "id": 1,
    "title": "",
    "code": "foo = \"bar\"\n",
    "linenos": false,
    "language": "python",
    "style": "friendly"
  },
  {
    "id": 2,
    "title": "",
    "code": "print(\"hello, world\")\n",
    "linenos": false,
    "language": "python",
    "style": "friendly"
  }
]
```
Or we can get a particular snippet by referencing its id:

```py
http http://127.0.0.1:8000/snippets/2/

HTTP/1.1 200 OK
...
{
  "id": 2,
  "title": "",
  "code": "print(\"hello, world\")\n",
  "linenos": false,
  "language": "python",
  "style": "friendly"
}
```


### Wrapping API Views

1. We use `@api_view` decorator for working with function based views.
2. We use `APIView` class for working with class-based views.

#### Class Based Views
* Code is reusable by inheritance.
* Maintainable
#### Function Based Views 
* Easy to use
* Code is not reusable by inheritance
#### views.py 

```py
from rest_framework import status
from rest_framework.decorators import api_view
from rest_framework.response import Response
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer


@api_view(['GET', 'POST'])
def snippet_list(request):
    """
    List all code snippets, or create a new snippet.
    """
    if request.method == 'GET':
        snippets = Snippet.objects.all()
        serializer = SnippetSerializer(snippets, many=True)
        return Response(serializer.data)

    elif request.method == 'POST':
        serializer = SnippetSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
```
```py
@api_view(['GET', 'PUT', 'DELETE'])
def snippet_detail(request, pk):
    """
    Retrieve, update or delete a code snippet.
    """
    try:
        snippet = Snippet.objects.get(pk=pk)
    except Snippet.DoesNotExist:
        return Response(status=status.HTTP_404_NOT_FOUND)

    if request.method == 'GET':
        serializer = SnippetSerializer(snippet)
        return Response(serializer.data)

    elif request.method == 'PUT':
        serializer = SnippetSerializer(snippet, data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

    elif request.method == 'DELETE':
        snippet.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
```
Notice that we're no longer explicitly tying our requests or responses to a given content type. request.data can handle incoming json requests, but it can also handle other formats. Similarly we're returning response objects with data, but allowing REST framework to render the response into the correct content type for us.

#### Adding optional format suffixes to our URLs

```py
def snippet_list(request, format=None):
```
Now update the `snippets/urls.py` file slightly, to append a set of format_suffix_patterns in addition to the existing URLs.

```py
from django.urls import path
from rest_framework.urlpatterns import format_suffix_patterns
from snippets import views

urlpatterns = [
    path('snippets/', views.snippet_list),
    path('snippets/<int:pk>/', views.snippet_detail),
]

urlpatterns = format_suffix_patterns(urlpatterns)
```

Output:
```json
http http://127.0.0.1:8000/snippets/

HTTP/1.1 200 OK
...
[
  {
    "id": 1,
    "title": "",
    "code": "foo = \"bar\"\n",
    "linenos": false,
    "language": "python",
    "style": "friendly"
  },
  {
    "id": 2,
    "title": "",
    "code": "print(\"hello, world\")\n",
    "linenos": false,
    "language": "python",
    "style": "friendly"
  }
]
```
We can control the format of the response that we get back, either by using the Accept header:

```sh
http http://127.0.0.1:8000/snippets/ Accept:application/json  # Request JSON
http http://127.0.0.1:8000/snippets/ Accept:text/html         # Request HTML
```
Or by appending a format suffix:
```sh
http http://127.0.0.1:8000/snippets.json  # JSON suffix
http http://127.0.0.1:8000/snippets.api   # Browsable API suffix
```
Similarly, we can control the format of the request that we send, using the Content-Type header.

```json
# POST using form data
http --form POST http://127.0.0.1:8000/snippets/ code="print(123)"

{
  "id": 3,
  "title": "",
  "code": "print(123)",
  "linenos": false,
  "language": "python",
  "style": "friendly"
}

# POST using JSON
http --json POST http://127.0.0.1:8000/snippets/ code="print(456)"

{
    "id": 4,
    "title": "",
    "code": "print(456)",
    "linenos": false,
    "language": "python",
    "style": "friendly"
}
```

### Writing Class Based Views

#### Class Based Views 
* Code is reusable by inheritance.
* 
#### views.py 

```py

from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from django.http import Http404
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework import status

class SnippetList(APIView):
    """
    List all Snippets or Create new Snippet
    """

    def get(self, request, format=None):
        snippets =  Snippet.objects.all()
        serializer= SnippetSerializer(snippets, many=True)
        return Response(serializer.data)
    
    def post(self, request, format=None):
        serializer = SnippetSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=status.HTTP_201_CREATED)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)

class SnippetDetail(APIView):
    """
    Retrive, Update or Delete a Snippet instance
    """
    def get_object(self, pk):
        try:
            return Snippet.objects.get(pk=pk)
        except Snippet.DoesNotExist:
            raise Http404
    
    def get(self, request, pk, format=None):
        snippet = self.get_object(pk=pk)
        serializer=SnippetSerializer(snippet)
        return Response(serializer.data)
    
    def put(self, request, pk, format=None):
        snippet = self.get_object(pk)
        serializer = SnippetSerializer(snippet,data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data)
        return Response(serializer.errors, status=status.HTTP_400_BAD_REQUEST)
    
    def delete(self, request, pk, format=None):
        snippet = self.get_object(pk)
        snippet.delete()
        return Response(status=status.HTTP_204_NO_CONTENT)
    
```

#### urls.py

```py
from django.urls import path
from snippets import views
from rest_framework.urlpatterns import format_suffix_patterns

urlpatterns = [
    path("snippets/", views.SnippetList.as_view()),
    path("snippets/<int:pk>/", views.SnippetDetail.as_view()),
]
urlpatterns = format_suffix_patterns(urlpatterns)
```

### Using Mixins (views.py)

The create/retrieve/update/delete operations that we've been using so far are going to be pretty similar for any model-backed API views we create. Those bits of common behaviour are implemented in REST framework's mixin classes.

```py

from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from rest_framework import mixins
from rest_framework import generics

class SnippetList(mixins.ListModelMixin,mixins.CreateModelMixin,generics.GenericAPIView):
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer

    def get(self, request, *args, **kwargs):
        return self.list(request, *args, **kwargs)
    
    def post(self, request, *args, **kwargs):
        return self.create(request,*args, **kwargs)
```
We'll take a moment to examine exactly what's happening here. We're building our view using GenericAPIView, and adding in ListModelMixin and CreateModelMixin.

The base class provides the core functionality, and the mixin classes provide the .list() and .create() actions. We're then explicitly binding the get and post methods to the appropriate actions. Simple enough stuff so far.

```py

class SnippetDetail(mixins.RetrieveModelMixin,mixins.UpdateModelMixin,mixins.DestroyModelMixin,generics.GenericAPIView):
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer

    def get(self, request, *args, **kwargs):
        return self.retrieve(request, *args, *kwargs)
    
    def put(self, request, *args, **kwargs):
        return self.update(request, *args, **kwargs)
    
    def delete(self, request, *args, **kwargs):
        return self.destroy(request, *args, **kwargs)
    
```
Pretty similar. Again we're using the GenericAPIView class to provide the core functionality, and adding in mixins to provide the .retrieve(), .update() and .destroy() actions.


### Using generic class-based views
Using the mixin classes we've rewritten the views to use slightly less code than before, but we can go one step further. REST framework provides a set of already mixed-in generic views that we can use to trim down our views.py module even more.

```py
from snippets.models import Snippet
from snippets.serializers import SnippetSerializer
from rest_framework import generics


class SnippetList(generics.ListCreateAPIView):
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer


class SnippetDetail(generics.RetrieveUpdateDestroyAPIView):
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer
```

### Authentication and Permissions
Currently our API doesn't have any restrictions on who can edit or delete code snippets. We'd like to have some more advanced behavior in order to make sure that:

* Code snippets are always associated with a creator.
* Only authenticated users may create snippets.
* Only the creator of a snippet may update or delete it.
* Unauthenticated requests should have full read-only access.

#### Adding information to our model

Add two new fields to the model
```py 
owner = models.ForeignKey('auth.User', related_name='snippets', on_delete=models.CASCADE)
highlighted = models.TextField()
```

We'd also need to make sure that when the model is saved, that we populate the highlighted field, using the pygments code highlighting library.


```py 
#models.py, model:Snippet
from pygments.lexers import get_lexer_by_name
from pygments.formatters.html import HtmlFormatter
from pygments import highlight

def save(self, *args, **kwargs):
    """
    Use the `pygments` library to create a highlighted HTML
    representation of the code snippet.
    """
    lexer = get_lexer_by_name(self.language)
    linenos = 'table' if self.linenos else False
    options = {'title': self.title} if self.title else {}
    formatter = HtmlFormatter(style=self.style, linenos=linenos,
                              full=True, **options)
    self.highlighted = highlight(self.code, lexer, formatter)
    super().save(*args, **kwargs)
```

When the above is done, we need to update our database tables

```py
rm -f db.sqlite3
rm -r snippets/migrations
python manage.py makemigrations snippets
python manage.py migrate
```

Create Superuser
```
python manage.py createsuperuser

```
#### Adding endpoints for our User models
Now that we've got some users to work with, we'd better add representations of those users to our API. Creating a new serializer is easy. In serializers.py add:
```py
from django.contrib.auth.models import User

class UserSerializer(serializers.ModelSerializer):
    snippets = serializers.PrimaryKeyRelatedField(many=True, queryset=Snippet.objects.all())

    class Meta:
        model = User
        fields = ['id', 'username', 'snippets']
```
Because `'snippets'` is a reverse relationship on the `User` model, it will not be included by default when using the `ModelSerializer` class, so we needed to add an explicit field for it.

We'll also add a couple of views to `views.py`. We'd like to just use read-only views for the user representations, so we'll use the `ListAPIView` and `RetrieveAPIView` generic class-based views.

```py
from snippets.serializers import UserSerializer
from django.contrib.auth.models import User


class UserList(generics.ListAPIView):
    queryset = User.objects.all()
    serializer_class = UserSerializer


class UserDetail(generics.RetrieveAPIView):
    queryset = User.objects.all()
    serializer_class = UserSerializer
```
Finally we need to add those views into the API, by referencing them from the URL conf. Add the following to the patterns in `snippets/urls.py`.

```py
path('users/', views.UserList.as_view()),
path('users/<int:pk>/', views.UserDetail.as_view()),
```

### Associating Snippets with Users
Right now, if we created a code snippet, there'd be no way of associating the user that created the snippet, with the snippet instance. The user isn't sent as part of the serialized representation, but is instead a property of the incoming request.


The way we deal with that is by overriding a `.perform_create()` method on our snippet views, that allows us to modify how the instance save is managed, and handle any information that is implicit in the incoming request or requested URL.

On the `SnippetList` view class, add the following method:

```py
def perform_create(self, serializer):
    serializer.save(owner=self.request.user)
```

The `create()` method of our serializer will now be passed an additional `'owner'` field, along with the validated data from the request.

#### Updating our serializer

Now that snippets are associated with the user that created them, let's update our `SnippetSerializer` to reflect that. Add the following field to the serializer definition in `serializers.py`:
```py
owner = serializers.ReadOnlyField(source='owner.username')
```

*Note:* Make sure you also add 'owner', to the list of fields in the inner Meta class.

This field is doing something quite interesting. The source argument controls which attribute is used to populate a field, and can point at any attribute on the serialized instance. It can also take the dotted notation shown above, in which case it will traverse the given attributes, in a similar way as it is used with Django's template language.

The field we've added is the untyped ReadOnlyField class, in contrast to the other typed fields, such as CharField, BooleanField etc... The untyped ReadOnlyField is always read-only, and will be used for serialized representations, but will not be used for updating model instances when they are deserialized. We could have also used CharField(read_only=True) here.


### Adding required permissions to views

Now that code snippets are associated with users, we want to make sure that only authenticated users are able to create, update and delete code snippets.

REST framework includes a number of permission classes that we can use to restrict who can access a given view. In this case the one we're looking for is IsAuthenticatedOrReadOnly, which will ensure that authenticated requests get read-write access, and unauthenticated requests get read-only access.


First add the following import in the views module
```py
from rest_framework import permissions
```

Then, add the following property to both the `SnippetList` and `SnippetDetail` view classes.

```py
permission_classes = [permissions.IsAuthenticatedOrReadOnly]
```
### Adding login to the Browsable API
If you open a browser and navigate to the browsable API at the moment, you'll find that you're no longer able to create new code snippets. In order to do so we'd need to be able to login as a user.

We can add a login view for use with the browsable API, by editing the URLconf in our project-level urls.py file.

Add the following import at the top of the file:
```py
from django.urls import path, include

```
And, at the end of the file, add a pattern to include the login and logout views for the browsable API.

```py
urlpatterns += [
    path('api-auth/', include('rest_framework.urls')),
]
```
The `'api-auth/'` part of pattern can actually be whatever URL you want to use.

Now if you open up the browser again and refresh the page you'll see a `'Login'` link in the top right of the page. If you log in as one of the users you created earlier, you'll be able to create code snippets again.

Once you've created a few code snippets, navigate to the `'/users/'` endpoint, and notice that the representation includes a list of the snippet ids that are associated with each user, in each user's 'snippets' field.

### Object level permissions

Really we'd like all code snippets to be visible to anyone, but also make sure that only the user that created a code snippet is able to update or delete it.

To do that we're going to need to create a custom permission.

In the snippets app, create a new file, `permissions.py`

```py 
from rest_framework import permissions


class IsOwnerOrReadOnly(permissions.BasePermission):
    """
    Custom permission to only allow owners of an object to edit it.
    """

    def has_object_permission(self, request, view, obj):
        # Read permissions are allowed to any request,
        # so we'll always allow GET, HEAD or OPTIONS requests.
        if request.method in permissions.SAFE_METHODS:
            return True

        # Write permissions are only allowed to the owner of the snippet.
        return obj.owner == request.user
```
Now we can add that custom permission to our snippet instance endpoint, by editing the permission_classes property on the `SnippetDetail` view class:

```py
from snippets.permissions import IsOwnerOrReadOnly

permission_classes = [permissions.IsAuthenticatedOrReadOnly,
                      IsOwnerOrReadOnly]

```
Now, if you open a browser again, you find that the 'DELETE' and 'PUT' actions only appear on a snippet instance endpoint if you're logged in as the same user that created the code snippet.

### Authenticating with the API
Because we now have a set of permissions on the API, we need to authenticate our requests to it if we want to edit any snippets. We haven't set up any authentication classes, so the defaults are currently applied, which are SessionAuthentication and BasicAuthentication.

When we interact with the API through the web browser, we can login, and the browser session will then provide the required authentication for the requests.

If we're interacting with the API programmatically we need to explicitly provide the authentication credentials on each request.

If we try to create a snippet without authenticating, we'll get an error:

```bash
http POST http://127.0.0.1:8080/snippets/ code="print(123)"

{
    "detail": "Authentication credentials were not provided."
}

```
We can make a successful request by including the username and password of one of the users we created earlier.

```
http -a admin:password123 POST http://127.0.0.1:8080/snippets/ code="print(789)"

{
    "id": 1,
    "owner": "admin",
    "title": "foo",
    "code": "print(789)",
    "linenos": false,
    "language": "python",
    "style": "friendly"
}
```
### Summary
We've now got a fairly fine-grained set of permissions on our Web API, and end points for users of the system and for the code snippets that they have created.

### Relationships and Hyperlinked API's

#### Creating an endpoint for the root of our API
Right now we have endpoints for 'snippets' and 'users', but we don't have a single entry point to our API. To create one, we'll use a regular function-based view and the @api_view decorator we introduced earlier. In your snippets/views.py add:

```py
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework.reverse import reverse


@api_view(['GET'])
def api_root(request, format=None):
    return Response({
        'users': reverse('user-list', request=request, format=format),
        'snippets': reverse('snippet-list', request=request, format=format)
    })
```

Two things should be noticed here. First, we're using REST framework's reverse function in order to return fully-qualified URLs; second, URL patterns are identified by convenience names that we will declare later on in our snippets/urls.py.

### Creating an endpoint for the highlighted snippets
The other obvious thing that's still missing from our pastebin API is the code highlighting endpoints.

Unlike all our other API endpoints, we don't want to use JSON, but instead just present an HTML representation. There are two styles of HTML renderer provided by REST framework, one for dealing with HTML rendered using templates, the other for dealing with pre-rendered HTML. The second renderer is the one we'd like to use for this endpoint.

The other thing we need to consider when creating the code highlight view is that there's no existing concrete generic view that we can use. We're not returning an object instance, but instead a property of an object instance.

Instead of using a concrete generic view, we'll use the base class for representing instances, and create our own .get() method. In your snippets/views.py add:

```py
from rest_framework import renderers

class SnippetHighlight(generics.GenericAPIView):
    queryset = Snippet.objects.all()
    renderer_classes = [renderers.StaticHTMLRenderer]

    def get(self, request, *args, **kwargs):
        snippet = self.get_object()
        return Response(snippet.highlighted)
```
As usual we need to add the new views that we've created in to our URLconf. We'll add a url pattern for our new API root in snippets/urls.py:

```py
path('', views.api_root),

```
And then add a url pattern for the snippet highlights:

```py
path('snippets/<int:pk>/highlight/', views.SnippetHighlight.as_view()),

```

#### Hyperlinking our API

Dealing with relationships between entities is one of the more challenging aspects of Web API design. There are a number of different ways that we might choose to represent a relationship:
* Using primary keys.
* Using hyperlinking between entities.
* Using a unique identifying slug field on the related entity.
* Using the default string representation of the related entity.
* Nesting the related entity inside the parent representation.
* Some other custom representation.

REST framework supports all of these styles, and can apply them across forward or reverse relationships, or apply them across custom managers such as generic foreign keys.

In this case we'd like to use a `hyperlinked` style between entities. In order to do so, we'll modify our serializers to extend `HyperlinkedModelSerializer` instead of the existing `ModelSerializer`.

The `HyperlinkedModelSerializer` has the following differences from `ModelSerializer`:

* It does not include the id field by default.
* It includes a url field, using HyperlinkedIdentityField.
* Relationships use HyperlinkedRelatedField, instead of PrimaryKeyRelatedField.

We can easily re-write our existing serializers to use hyperlinking. In your snippets/serializers.py add:

```py
class SnippetSerializer(serializers.HyperlinkedModelSerializer):
    owner = serializers.ReadOnlyField(source='owner.username')
    highlight = serializers.HyperlinkedIdentityField(view_name='snippet-highlight', format='html')

    class Meta:
        model = Snippet
        fields = ['url', 'id', 'highlight', 'owner',
                  'title', 'code', 'linenos', 'language', 'style']


class UserSerializer(serializers.HyperlinkedModelSerializer):
    snippets = serializers.HyperlinkedRelatedField(many=True, view_name='snippet-detail', read_only=True)

    class Meta:
        model = User
        fields = ['url', 'id', 'username', 'snippets']
```

Notice that we've also added a new 'highlight' field. This field is of the same type as the url field, except that it points to the 'snippet-highlight' url pattern, instead of the 'snippet-detail' url pattern.

Because we've included format suffixed URLs such as '.json', we also need to indicate on the highlight field that any format suffixed hyperlinks it returns should use the '.html' suffix.

#### Making sure our URL patterns are named
If we're going to have a hyperlinked API, we need to make sure we name our URL patterns. Let's take a look at which URL patterns we need to name.

* The root of our API refers to 'user-list' and 'snippet-list'.
* Our snippet serializer includes a field that refers to 'snippet-highlight'.
* Our user serializer includes a field that refers to 'snippet-detail'.
* Our snippet and user serializers include 'url' fields that by default will refer to `{model_name}-detail'`, which in this case will be 'snippet-detail' and 'user-detail'.


After adding all those names into our URLconf, our final snippets/urls.py file should look like this:

```py
from django.urls import path
from rest_framework.urlpatterns import format_suffix_patterns
from snippets import views

# API endpoints
urlpatterns = format_suffix_patterns([
    path('', views.api_root),
    path('snippets/',
        views.SnippetList.as_view(),
        name='snippet-list'),
    path('snippets/<int:pk>/',
        views.SnippetDetail.as_view(),
        name='snippet-detail'),
    path('snippets/<int:pk>/highlight/',
        views.SnippetHighlight.as_view(),
        name='snippet-highlight'),
    path('users/',
        views.UserList.as_view(),
        name='user-list'),
    path('users/<int:pk>/',
        views.UserDetail.as_view(),
        name='user-detail')
])
```

### Adding pagination

The list views for users and code snippets could end up returning quite a lot of instances, so really we'd like to make sure we paginate the results, and allow the API client to step through each of the individual pages.

We can change the default list style to use pagination, by modifying our tutorial/settings.py file slightly. Add the following setting:
```py
REST_FRAMEWORK = {
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 10
}
```

Note that settings in REST framework are all namespaced into a single dictionary setting, named REST_FRAMEWORK, which helps keep them well separated from your other project settings.

We could also customize the pagination style if we needed to, but in this case we'll just stick with the default.

#### Browsing the API
If we open a browser and navigate to the browsable API, you'll find that you can now work your way around the API simply by following links.

You'll also be able to see the 'highlight' links on the snippet instances, that will take you to the highlighted code HTML representations.


### ViewSets & Routers
REST framework includes an abstraction for dealing with ViewSets, that allows the developer to concentrate on modeling the state and interactions of the API, and leave the URL construction to be handled automatically, based on common conventions.

ViewSet classes are almost the same thing as View classes, except that they provide operations such as retrieve, or update, and not method handlers such as get or put.

A ViewSet class is only bound to a set of method handlers at the last moment, when it is instantiated into a set of views, typically by using a Router class which handles the complexities of defining the URL conf for you.

#### Refactoring to use ViewSets

Let's take our current set of views, and refactor them into view sets.

First of all let's refactor our `UserList` and `UserDetail` views into a single `UserViewSet`. We can remove the two views, and replace them with a single class:

```py
from rest_framework import viewsets

class UserViewSet(viewsets.ReadOnlyModelViewSet):
    """
    This viewset automatically provides `list` and `retrieve` actions.
    """
    queryset = User.objects.all()
    serializer_class = UserSerializer
```
Here we've used the `ReadOnlyModelViewSet` class to automatically provide the default 'read-only' operations. We're still setting the queryset and serializer_class attributes exactly as we did when we were using regular views, but we no longer need to provide the same information to two separate classes.

Next we're going to replace the `SnippetList`, `SnippetDetail` and `SnippetHighlight` view classes. We can remove the three views, and again replace them with a single class.

```py
from rest_framework.decorators import action
from rest_framework.response import Response
from rest_framework import permissions

class SnippetViewSet(viewsets.ModelViewSet):
    """
    This viewset automatically provides `list`, `create`, `retrieve`,
    `update` and `destroy` actions.

    Additionally we also provide an extra `highlight` action.
    """
    queryset = Snippet.objects.all()
    serializer_class = SnippetSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly,
                          IsOwnerOrReadOnly]

    @action(detail=True, renderer_classes=[renderers.StaticHTMLRenderer])
    def highlight(self, request, *args, **kwargs):
        snippet = self.get_object()
        return Response(snippet.highlighted)

    def perform_create(self, serializer):
        serializer.save(owner=self.request.user)

```
This time we've used the `ModelViewSet` class in order to get the complete set of default read and write operations.

Notice that we've also used the @action decorator to create a custom action, named `highlight`. This decorator can be used to add any custom endpoints that don't fit into the standard `create`/`update`/`delete` style.

Custom actions which use the `@action` decorator will respond to `GET` requests by default. We can use the methods argument if we wanted an action that responded to `POST` requests.

The `URLs` for custom actions by default depend on the method name itself. If you want to change the way url should be constructed, you can include `url_path` as a decorator keyword argument.

#### Binding ViewSets to URLs explicitly

The handler methods only get bound to the actions when we define the `URLConf`. To see what's going on under the hood let's first explicitly create a set of views from our ViewSets.

In the `snippets/urls.py` file we bind our `ViewSet` classes into a set of concrete views.
```py
rom snippets.views import SnippetViewSet, UserViewSet, api_root
from rest_framework import renderers

snippet_list = SnippetViewSet.as_view({
    'get': 'list',
    'post': 'create'
})
snippet_detail = SnippetViewSet.as_view({
    'get': 'retrieve',
    'put': 'update',
    'patch': 'partial_update',
    'delete': 'destroy'
})
snippet_highlight = SnippetViewSet.as_view({
    'get': 'highlight'
}, renderer_classes=[renderers.StaticHTMLRenderer])
user_list = UserViewSet.as_view({
    'get': 'list'
})
user_detail = UserViewSet.as_view({
    'get': 'retrieve'
})
```

Notice how we're creating multiple views from each `ViewSet` class, by binding the http methods to the required action for each view.

Now that we've bound our resources into concrete views, we can register the views with the URL conf as usual.

```py
urlpatterns = format_suffix_patterns([
    path('', api_root),
    path('snippets/', snippet_list, name='snippet-list'),
    path('snippets/<int:pk>/', snippet_detail, name='snippet-detail'),
    path('snippets/<int:pk>/highlight/', snippet_highlight, name='snippet-highlight'),
    path('users/', user_list, name='user-list'),
    path('users/<int:pk>/', user_detail, name='user-detail')
])
```
### Using Routers

Because we're using ViewSet classes rather than View classes, we actually don't need to design the URL conf ourselves. The conventions for wiring up resources into views and urls can be handled automatically, using a `Router` class. All we need to do is register the appropriate view sets with a router, and let it do the rest.

Here's our re-wired `snippets/urls.py` file.

```py
from django.urls import path, include
from rest_framework.routers import DefaultRouter
from snippets import views

# Create a router and register our viewsets with it.
router = DefaultRouter()
router.register(r'snippets', views.SnippetViewSet,basename="snippet")
router.register(r'users', views.UserViewSet,basename="user")

# The API URLs are now determined automatically by the router.
urlpatterns = [
    path('', include(router.urls)),
]

```
Registering the viewsets with the router is similar to providing a urlpattern. We include two arguments - the URL prefix for the views, and the viewset itself.

The DefaultRouter class we're using also automatically creates the `API root` view for us, so we can now delete the `api_root` method from our views module.

#### Trade-offs between views vs viewsets
Using viewsets can be a really useful abstraction. It helps ensure that URL conventions will be consistent across your API, minimizes the amount of code you need to write, and allows you to concentrate on the interactions and representations your API provides rather than the specifics of the URL conf.

That doesn't mean it's always the right approach to take. There's a similar set of trade-offs to consider as when using class-based views instead of function based views. Using viewsets is less explicit than building your views individually.