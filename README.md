# django-mako [![CircleCI](https://circleci.com/gh/ahmedaljazzar/django-mako.svg?style=svg)](https://circleci.com/gh/ahmedaljazzar/django-mako)
The simple, elegant Django Mako library
Used base engine to create a template rendering class to be used like Django's TemplateView class. To understand how to use it, read [Custom backends on django](https://docs.djangoproject.com/en/1.8/topics/templates/#custom-backends).

The current implementation assumes all system templates are Mako Template. Thus, when you start a new template make sure that the template language is Mako not Django. Later, when you decide to use another template backend like Django Template Backend, just pass `using='Django'` in your FBV or add `self.template_engine = 'mako'` in your CBV `__init__` method. 
Enjoy! This shouldn't be tricky any more.


## Installation
To install the package as a requirement in your python environemnt just
do
```
pip install djangomako
```
or
```
easy_install djangomako
```


## Using the library
After installing the package in your python environment, navigate to 
your project's `settings.py` and add the following lines in the 
`TEMPLATES` variable

```python
TEMPLATES = [
    # ...
    {
        'BACKEND': 'djangomako.backends.MakoBackend',
        'NAME': 'mako',
        'DIRS': [
            os.path.join(BASE_DIR, 'templates'),
        ],
    },
    # ...
]
```

- The `BACKEND` value is from this library.
- The `NAME` is simply the template identifier.
- In `DIRS` you're gonna include all the directories that have mako 
templates.
- The order matters here, so if you want your project to 
support only mako, you just need to remove the Django entry from the 
templates, while if you need mako as a fallback only, then you need to
put it under the Django Template entry.


#### Template Variables

I passed some template variables to the context if the request objects 
exists:

1. `CSRF_TOKEN` and `CSRF_INPUT`
    ```mako
    ${ csrf_input }
    ${ csrf_token }
    ```
1. To access the request:
    ```mako
    ${ request }
    ```
1. To include a static file url:
    ```mako
    ${ static('image.png') }
    ```
1. To reverse a url in the template:
    - Mako Template
    ```mako
    ${ url('home') }
    ```

## Detailed Examples?
An example of how to use this library in Class-Based view and 
Function-Based Views is inside [niceapp](https://github.com/ahmedaljazzar/django-mako/tree/master/niceapp)
app.

## Detailed Explanation?
You can find a detailed explanation of how I implemented this library 
in my blog post named [Integrating third-party templates' libraries with Django](https://ahmedjazzar.com/single-post/Mako-Django).

## License
The MIT License (MIT)
Copyright (c) 2017 Ahmed Jazzar <me@ahmedjazzar.com>
