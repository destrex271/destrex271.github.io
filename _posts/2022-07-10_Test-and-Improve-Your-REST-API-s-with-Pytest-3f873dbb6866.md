Test and Improve Your REST API’s with Pytest

Test and Improve Your REST API’s with Pytest
============================================

“Tests are stories we tell the next generation of programmers on a project.”

---

### Test and Improve Your REST API’s with Pytest

![](https://cdn-images-1.medium.com/max/800/1*6DiKaTQOssbhimr6fJZbWw.jpeg)
> **“Tests are stories we tell the next generation of programmers on a project.”**

Unit Testing is an integral part of Software Development. If your code isn’t tested properly, it might fail in production at the most critical times. All these problems that might arise in the future can be averted by following the Test driven approach to Software Development.

Today we are going to see how to use Pytest to write unit tests for your Django API’s built using the Django Rest Framework.

### Setting Up Your Django Project

First of all install the following packages with pip

```
pip install django djangorestframework pytest pytest-django factory_boy pytest_factoryboy
```

This installs all the required modules to create our django application and setup the unit tests. You can clone [this repository](https://github.com/destrex271/Drf_API) to setup this basic django project if you are following this article just to learn about this process else just look at the code in this repository to get an idea on how to integrate these unit tests.

### What is Pytest?

The pytest framework makes it easy to write small, readable tests, and can scale to support complex functional testing for applications and libraries. It is one of the most used frameworks out there in python to write unit tests and it is also really easy to use.

#### Setting Up Pytest Configuration

First of all create the *pytest.ini* file in the root directory of you django project.

![](https://cdn-images-1.medium.com/max/800/1*GPaX23i-p_BQBT8yMC1vtA.png)

And add the following contents to the file:

```
[pytest]
```

```
DJANGO_SETTINGS_MODULE = "yourprojectname".settings
```

```
python_files = test.py test_*.py *_tests.py tests.py
```

Here the *python\_files* attribute gives the possible files with the following filenames that might contain the unit test functions.

### Setup Your Tests

In this demo application we are using a single model named *Song.*

```
from django.db import models  
  
# Create your models here.  
  
class Song(models.Model):  
  
    title = models.TextField(blank=False)  
    artist = models.TextField(blank=False, default="unknown")  
    lyrics = models.TextField(blank=False, default="Unavailable")  
    file_location = models.SlugField(blank=False,default="none")  
  
    def __str__(self) -> str:  
        return ("Title : " + str(self.title) + " Artist: " + str(self.artist))
```

First of all we will setup a Factory Module for this model so that we can test our API’s with automatically generated dummy data without manually providing it.

To proceed we first need to organize our tests and all the configuration files associated with them in a tests folder inside our app but before that do delete the tests.py file provided by default.

Arrange your directory structure as follows:

![](https://cdn-images-1.medium.com/max/800/1*E8_4LZCQ3jMGBNlcBt0CvA.png)

Directory Structure For Tests

Lets setup our Model Factories.

#### Setting Up the Model Factory for our Songs Model

To conduct unit tests we cannot use the production database, so instead we create a mock database to run our tests against. The general way for that would be to create a function that would manually add some mock data to our database. That is really easy if your codebase is really small but for large codebases we need to keep everything organised and isolated as much as possible([*Loosely Coupled*](https://docs.djangoproject.com/en/4.0/misc/design-philosophies/)) to prevent any unnecessary problems in our tests.

Therefore we utilize [*Model Factories*](https://factoryboy.readthedocs.io/en/stable/orms.html)to create mock data for our test database. We use [*factory\_boy*](https://factoryboy.readthedocs.io/en/stable/introduction.html) and [*pytest\_factoryboy*](https://readthedocs.org/projects/pytest-factoryboy/) libraries for this.

Add the following content to your *factories.py*:

```
import factory  
from api.models import Song  
  
class SongFactory(factory.django.DjangoModelFactory):  
    class Meta:  
        model = Song  
      
    title = factory.Faker("sentence")  
    artist = factory.Faker("name")  
    lyrics = factory.Faker("text")  
    file_location = factory.Faker("slug")
```

This factory class allows us to define the behaviour of our Model Factory and we can later use it to create our mock data. We use the conftest.py file for that. The objects of this class can utilize the *create()* function to generate a single mock instance or the *create\_batch(n)* function (where n is a positive integer) to generate “n” mock instances. In that case we will by default receive an instance of our Model Factory in the format of “model\_factory” and we can use it as “model\_factory.create\_batch(10)”. To register our model factory we add the following to our *conftest.py*:

```
from pytest_factoryboy import register  
from .factories import SongFactory  
  
# Register Approach  
  
register(SongFactory)
```

Although this feature was made to remove fixtures but I like to use both of them as a combination and therefore add the following to your conftest.py instead:

```
from .factories import StudentFactory  
import pytest
```

```
@pytest.fixture  
def students():  
    return StudentFactory.create_batch(10)
```

Now lets Finally write our tests!

### Writing Our Unit Tests

Now we are going to utilize the true power of pytest.

First of all since we need to call our API’s we need to have some sort of a way to access there url routes. For that we use the APIClient class provided by the Django Rest Framework.

Lets import it and instantiate it in our file:

```
from rest_framework.test import APIClient
```

```
import pytest
```

```
client = APIClient()
```

Now lets create our unit test function as follows, here we will simulate a simple get request and check if the API returns a response with the status code 200.

```
@pytest.mark.django_db  
def test_get_song(songs):  
    response = client.get('/songs')  
    assert response.status_code == 200
```

Here the decorator *‘pytest.mark.django\_db’* is used to allow our test function to interact with the database. We use the ‘get’ function of client object to send a request to the API. Notice that we passed a parameter ‘songs’ to our function. This is the same fixture function defined in the conftest.py which will populate the test database with 10 instances of songs generated by our SongFactory object.

You can design more intricate tests that even check the validity of the data received, or by sending some wrong parameters along with your request just to validate the behavior of your API.

Just remember that your unit tests are to study and then define the behavior of your API under various conditions, so most of the edge cases must be targeted.

Now run the command:

```
pytest -s
```

In your terminal from the root library and it will execute all the tests that you have designed, in our case only a single test will be executed.

The -s parameter is just to allow your print statements to write to the console, if you want that, else you can just run pytest.

You can write more tests, even for post requests. A demo for that would go as follows:

```
@pytest.mark.django_db  
def test_post_song():  
    payload = {  
       "name": "Faded",  
       "artist": "Alan Walker",  
       "file_location": "https://www.youtube.com/watch?v=60ItHLz5WEA"  
    }  
    response = client.post('/songs/create', payload, format='json')  
    assert response.status_code == 201
```

This adds a song to our test database and we can check the validity by checking the status code. You can also check if the data returned in the response is same as that in the payload, this will allow you to check whether your API is storing the data sent to it properly. The format attribute specifies that the data being sent is in json format.

The same procedure can be followed for PUT and DELETE requests.

Well with this we end a basic introduction to unit testing in Django with pytest.

Thanks for reading!

By [Akshat Jaimini](https://medium.com/@destrex271) on [July 10, 2022](https://medium.com/p/3f873dbb6866).

[Canonical link](https://medium.com/@destrex271/test-and-improve-your-rest-apis-with-pytest-3f873dbb6866)

Exported from [Medium](https://medium.com) on March 25, 2025.