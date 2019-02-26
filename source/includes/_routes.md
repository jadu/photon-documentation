#Routes

> Routes are defined in the theme `routing.yml` config file.

```yaml
homepage:
    path: /homepage/{homepageId}/{homepageSlug}
    defaults:
        _controller: photon.page.homepage

atoz_list:
    path: /a_to_z/{startsWith}
    defaults:
        _controller: photon.page.atoz_list
        startsWith: ~

atoz_article:
    path: /a_to_z/service/{serviceId}/{serviceSlug}
    defaults:
        _controller: photon.page.atoz_article
    requirements:
        serviceId: \d+
```

Routes within Photon are based on the Symfony router. 

Where a `{placeholder}` is placed in the route path, that portion becomes a wildcard. The corresponding controller must now have an argument called `$placeholder`. 

<aside class="notice">
The wildcard and argument names must match exactly.
</aside>

Each route has an internal name. For example `homepage`, `atoz_list` and `atoz_article`. These must be unique and are used to generate URLs in controllers and templates.

Further information on routing is available in the Symfony documentation - [Routing](https://symfony.com/doc/2.8/routing.html).

##Generating URLs

```php
<?php

$link->setUrl($this->generateUrl(
    'news_article',
    [
        'articleId' => $newsArticle->getId(),
        'articleSlug' => $newsArticle->getSlug(),
    ]
));
```
To generate a URL, you must specify the name of the route, and any parameters used in the path for that route.

Instead of hardcoding URLs into templates, the `path` Twig function can be used to generate URLs based on the routing configuration. Changing the route will then update all template instances where that route is used.

```twig
<a href="{{ path('welcome') }}">Home</a>
```

Further information on generating URLs is provided in the Symfony documentation - [Generating URLs](https://symfony.com/doc/2.8/routing.html#generating-urls)


##Redirecting

```php
<?php

// redirect to the "homepage" route
return $this->redirectToRoute('homepage');

// do a permanent - 301 redirect
return $this->redirectToRoute('homepage', [], 301);

// redirect to a route with parameters
return $this->redirectToRoute(
    'blog_show',
    [
        'slug' => 'my-page',
    ]
);

// redirect externally
return $this->redirect('http://symfony.com/doc');
```

A number of redirect options are provided via Symfony.

Further information on redirecting is provided in the Symfony documentation - [Redirecting](https://symfony.com/doc/2.8/controller.html#redirecting).


