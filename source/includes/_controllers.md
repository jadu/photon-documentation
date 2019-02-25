# Controllers

## Page controllers

> Pages are registered within the theme `services.yml` configuration file. 

```yaml
photon_cms_project.page.document_category:
  class: DocumentCategoryController
  parent: photon.controller.page
  arguments:
      - '@photon.repository.category'
      - '@photon.repository.document'
      - '@photon.repository.homepage'
      - '@photon.repository.homepage_category_default'
      - '@photon.repository.supplement'
      - '@sdk.configuration.constant_repository'
      - '@router'
  tags:
      - { name: photon.page, 
      page_name: document_category }
```

> Page services must be tagged with `photon.page`.

Page controllers are responsible for fetching the content from a respository and rendering a template. A simple invokable controller  is defined per `Page` class. Page components are invoked by a route.

Each page controller extends the `Photon\Core\Controller\Page` class of the `PhotonCoreBundle` project. 

`Photon\Core\Controller\Page` itself extends the Symfon framework `Controller` class. Further details are available in the Symfony documentation - [Controller](https://symfony.com/doc/2.8/controller.html).

## Component controllers

> Components are registered within the theme `services.yml` configuration file.

```yaml
photon_cms_project.component.category_navigation:
  class: CategoryNavigationController
  parent: photon.controller.component
  arguments:
      - '@ohoton.repository.category'
      - '@router'
      - '@sdk.configuration.constant_repository'
  tags:
      - { name: photon.component, 
      component_name: category_navigation }
```

> Component services must be tagged with `photon.component`.

Component controllers, like page controllers, are responsible for fetching the content from a respository and rendering a template. 

A simple invokable controller class is defined per component. 

Page controllers have no knowledge of the action of the component controller, components are rendered within a page template as sub-requests.

As with Pages, Components can be extended and overridden by other themes.

Additional information on sub-requests is provided in the Symfony documentation - <a href="https://symfony.com/doc/2.8/components/http_kernel.html#sub-requests">Sub Requests</a>.

### Invoking components

```twig
{{ component('announcement') }}
{{ component('announcement', {name: 'Tom'}) }}
```

Components are not invoked by a route, but instead by using the `component()` Twig function

Parameters can be passed to components at render time, which are passed to the `__invoke()` method of the Component.

```php
<?php

public function __invoke($name)
{
    return $this->render('announcement.html.twig', [
        'name' => $name,
    ]);
}
```

## Widget controllers

> Widgets are registered within the theme `services.yml` configuration file.

```yaml
photon_cms_project.widget.website_statistics:
    class: WebsiteStatisticsWidget
    parent: photon.controller.widget
    arguments:
        - '@photon.repository.website_statistics'
    tags:
        - { name: photon.widget, widget_id: 31 }
```

> Widget services must be tagged with `photon.widget` and with the parameter `widget_id`. The id must match the corresponding database entry in `JaduHomepageWidgets`.

Widget controllers are specialised component controllers. They interact with the Homepage designer feature of Jadu CMS.

<aside class="notice">
When no matching widget service is found, the default widget service is used, with <code>widget_id = 1</code>. The default widget will pass code stored in the database through the function <code>eval()</code> to generate the response returned from the controller.
</aside>

### Invoking widgets

```twig
{{ widget(widgetRecord) }}
```
Widgets are not invoked by a route, but instad by using the `widget()` Twig function.

A widget record must be passed as a parameter to the `widget()` function.

## Interacting with the request

```php
<?php

if ($this->getRequestStack()->request->has('period')
    && $this->getRequestStack()->get('period') == 'today'
) {
```

The `Page` class within `PhotonCoreBundle` initialises the Symfony `Request` object in its constructor.

The Request stack object can be retrieved in classes that extend `Page` by calling `getRequestStack()` method.

Further details on how to interact with data held in the Request object are provided in the Symfony documentation - [Accessing Request Data](https://symfony.com/doc/2.8/components/http_foundation.html#accessing-request-data).

## Returning a response

```php

<?php

return $this->render('article.html.twig', [
    'page' => $page,
    'page_categoryId' => $categoryId,
    'page_contentType' => 1,
    'page_translationItem' => $document->getId(),
    'page_translationType'=> 'document',
    'page_structure' => $pageStructure
]);
```

All controller classes contain an `__invoke()` method that is called when a request terminates at that controller. The `__invoke()` method must return a `Response` object.

The `Photon\Core\Controller\Page` class of the `PhotonCoreBundle` project that all Photon Page controllers extend provides a method `render()` that returns a formatted `Response` object. 

`render()` generally takes two arguments:

- the path to the Twig template to be rendered
- an array of values to be supplied to the template

Further details on Response objects are provided by the Symfony documentation - [Response](https://symfony.com/doc/2.8/components/http_foundation.html#response).

## Core Page controller methods

The `Photon\Core\Controller\Page` class provides a number of useful functions to the controllers that extend it. 

Method | Description
---|---
`render()` | Render a twig template and return a Response
`getMetaElement()` | Create and return a Meta object
`getRequestStack()` | Get the Symfony Request object for this request
`getMetadata()` | Populate and return a Metadata object for this page
`isPreview()` | Check if this page is currently being accessed as a preview
`getTranslatedString()` | Get the translated string for a given key based on the site's locale value
`isPasswordProtected()` | Check if the site is currently behind password protection
`isAuthenticated()`  | Check if the user has a current session for viewing a site behind password protection