# iam-idbase
A base look-and-feel package for apps designed to run on Identity.UW with django.

## What it includes:
* template idbase/base.html and the common site-wide statics for dependent apps to include.
* Angular app in identity.js for common site-wide behaviors.
* middleware LoginUrlMiddleware and SessionTimeoutMiddleware for managing logins and sessions in a common way.
* RESTDispatch class for creating new api endpoints.

## Using it within a project
* Add 'idbase' to your settings.INSTALLED_APPS
* Add 'idbase.middleware.SessionTimeoutMiddleware' to settings.MIDDLEWARE_CLASSES after SessionMiddleware.
* Replace any authentication middleware in settings.MIDDLEWARE_CLASSES with 'idbase.middleware.LoginUrlMiddleware'.
* Add 'idbase.context_processors.app_context' to your settings.TEMPLATES list of context_processors.
* Declare a settings.APP_CONTEXT...
```
APP_CONTEXTS = {
    'default': {'base_url': '/account/', 'css_loads': ['account.css'], 'javascript_loads': ['account.js']}
}
```
* Add some urls to handle login and loginstatus...
```
urlpatterns = [
    url(r'^login$', login),
    url(r'^api/loginstatus$', LoginStatus().run),
    ...
]
```
* Extend idbase/base.html in your templates...
```
{% extends "idbase/base.html" %}

{% block content %}
<h1>Set up your account</h1>
...
{% endblock %}
```

