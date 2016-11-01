# Django Spages

Lightweight single page app for Django on top of [Page.js](https://github.com/visionmedia/page.js) (7.8 Ko) for
the client-side routing, and [Promise.js](https://github.com/stackp/promisejs) (2,3 Ko) for the async ajax calls. 

- *Fast*: load the page once and update the content using rest
- *Old school friendly*: straigthforward, no npm and friends build steps

## Install

  ```bash
pip install django-spages
  ```

Installed apps:

  ```python
"rest_framework",
"ckeditor",
"ckeditor_uploader",
"codemirror2",
"mptt_graph",
"jsoneditor",
"spages",
  ```

Migrate.

Urls:

  ```python
url(r'^ckeditor/', include('ckeditor_uploader.urls')),
url(r'^',include('spages.urls'))
  ```
  
## Options

To use the Codemirror editor instead of the default Ckeditor add this setting:

  ```python
SPAGES_CODE_MODE = True
  ```

## Usage

You just need a ``{% block content %}`` in your ``base.html`` template and a ``<div id="content">`` where you want
the page content to be rendered.

Other possibility: ``{% include "spages/client.js" %}`` somewhere.

Create pages in the admin. The page.js routes will be autogenerated in ``templates/spages/auto/routes.js``. A 
management command is also available to rebuild the routes: ``python manage.py build_routes``. 

Just link to your pages normaly in the navigation and the routes will be applied, retrieving json 
from the server to update content.

If you need to extend the basic js handlers on page create templates: ``spages/extra_handlers.js``: this js will be
executed before fetching the data. And ``spages/extra_async_handlers.js``: this will be executed within the async loop
after fetching content.

## Why?

The goal is to get faster render speed for pages, and to improve the user experience,
specialy the ones that use low bandwidth connections.