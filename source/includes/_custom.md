#Customisation

##Creating a theme

Adding a new theme requires you to:

* Create a new theme bundle
* Create a theme class that defines your theme
* Register your theme with the CMS
* Configure your Symfony app to use the theme

##Creating a theme bundle

```
AlphaTheme 
    |- AlphaThemeBundle.php
    |- Component
    |    |- CategoryNavigationController.php
    |- DependencyInjection
    |    |- AlphaThemeExtension.php
    |- Page
    |    |- UtilitiesContent
    |        |- ThemeDemoController.php
    |- Resources
    |    |- config
    |    |   |- routing.yml
    |    |   |- services.yml
    |    |   |- theme.yml
    |    |- public 
    |    |   |- dist
    |    |   |   |...
    |    |   |- images
    |    |   |   |...
    |    |   |- js
    |    |       |...
    |    |- templates
    |        |- layouts
    |        |   |...
    |        |- pages
    |        |   |...
    |        |- partials
    |        |   |...
    |        |- widgets
    |            |...
    |- Theme
        |- AlphaTheme.php
            
```

A bundle is in essence a folder of files laid out in a consistent way.

It **must** contain:

* A bundle definition file eg. `AlphaThemeBundle.php`
* A theme definition file eg. `Theme/AlphaTheme.php`
* A theme service definition in a config file eg. `Resources/config/services.yml`
* Dependency injection class to load the theme service definition eg. `DependencyInjection/AlphaThemeExtension.php`

For **Galaxies theme bundles**, the following addtions are also required:

* A demo route definition in a config file eg. `Resources/config/routing.yml`
* A theme config file eg. `Resources/config/theme.yml`
* A demo route controller eg. `Page/UtilitiesContent/ThemeDemoController.php`
* A preview image eg. `Resources/public/images/preview.png`

An example theme bundle is available on GitHub: [ExampleTheme](https://github.com/jadu/photon-example-theme/tree/master/src/ExampleTheme)

##Creating a theme definition

```php
<?php

namespace Spacecraft\DemoProject\Theme;

use Photon\Core\Theme\Theme;

class DemoTheme implements Theme
{
    public function getName()
    {
        return 'demo';
    }

    public function getParent()
    {
        return 'base';
    }

    public function getPath()
    {
        return __DIR__ . '/../Resources/templates';
    }
}
```

The example defines the `demo` theme, which extends `base`. By convention, the theme file sits within the `Theme` directory of the project. 

The machine name of the theme should be defined in the `getName()` method. If the theme is extending an existing theme, this should be defined in the `getParent()` method. `base` is the machine name of the CMS default theme.

The path to the twig templates provided by this theme should be defined within the `getPath()` method.

##Defining a theme service

```yaml
spacecraft_demo_project.theme:
    class: Spacecraft\DemoProject\Theme\DemoTheme
    tags:
        - { name: photon.theme }
```

To define a theme service service, create a service in `services.yml` that points to the theme definition file. The service should be tagged with `photon.theme`.

<aside class="notice">
Remember to include Dependency injection project extension if your theme includes its own services.yml.
</aside>

##Using a custom theme

```yaml
photon_core:
    theme: demo
```

To use a theme, the configuration of your Symfony application should be updated. The `photon_core` element should have a child, `theme`. The value of `theme` should be the machine name of the theme, eg. `demo`.

By default, the CMS stores the Symfony application for the main site in `/path/to/jadu/config/frontend.yml`.

##Twig namespaces

```twig
{% extends '@theme:base/components/announcement.html.twig' %}

{% block title_outer %}
    <h2>{{ block('title') }}</h2>
{% endblock %}
```

The selected theme will always be the main namespace for Twig, i.e. `pages/demo.html.twig` will be loaded from the selected theme's templates. 

If a theme has a parent theme, then the parent theme will also be within the main namespace. 

Twig templates of a particular theme can be referenced using the theme namespace.

<aside class="notice">
This is particularly useful when extending a base theme.
</aside>

##Customising pages

> Defining the controller:

```php
<?php

namespace Spacecraft\DemoProject\Page;

use Photon\Core\Controller\Page;
use Symfony\Component\HttpFoundation\Response;

class DemoController extends Page
{
    /**
     * @return Response
     */
    public function __invoke()
    {
        return $this->render('pages/demo.html.twig');
    }
}
```

> Defining the service:

```yaml
spacecraft_demo_project.page.demo:
    class: Spacecraft\DemoProject\Page\DemoController
    parent: photon.controller.page
```

> When adding a new page, simply define the route and specify the new controller service

```yaml
demo:
    path: /demo
    defaults:
        _controller: spacecraft_demo_project.page.demo
```

Pages can be added in Photon by creating a controller class, defining a service and route.

The controller class is a standard Symfony controller that takes a `Request` and returns a `Response`. Generally, each page will have it's own controller and be an invokable class.

In this example the Twig template being rendered needs to be available in the current theme. 

<aside class="notice">
When creating the service, the parent service <code>photon.controller.page</code> can be used to simplify the definition. This will set all of the dependencies that are required by the <code>Page</code> base class.
</aside>

##Customising components

> Defining the controller:

```php
<?php

namespace Spacecraft\DemoProject\Component;

use Photon\Core\Controller\Component;
use Symfony\Component\HttpFoundation\Response;

class AnnouncementController extends Component
{
    /**
     * @return Response
     */
    public function __invoke()
    {
        return $this->render('components/announcement.html.twig');
    }
}
```

> Defining the service:

```yaml
spacecraft_demo_project.page.demo:
    class: Spacecraft\DemoProject\Component\AnnouncementController
    parent: photon.controller.component
    tags:
        - { name: photon.component, component_name: announcement }
```

> Invoking the component:

```twig
{{ component('announcement') }}
```

Components can be added in Photon by creating a controller class and defining a service tagged as `photon.component`.

The controller class for a component is a standard Symfony controller that takes a `Request` and returns a `Response`. The controller must be an invokable class to be compatible with the component system.

The service must be given a name. This name will be used when referencing the component within a Twig template.

Once the component service is defined it can be rendered within any Photon template using the `component()` Twig function.

<aside class="notice">
When creating the service, the parent service <code>photon.controller.component</code> can be used to simplify the definition. This will set all of the dependencies that are required by the <code>Component</code> base class. 
</aside>

##Customising widgets

> Defining the controller:

```php
<?php

namespace Photon\CmsProject\Widget;


use Photon\CmsEngine\Model\PublishingContent\Homepage\HomepageWidget;
use Photon\Core\Controller\Widget;
use Symfony\Component\HttpFoundation\Response;

class ContentWidget extends Widget
{
    /**
     * @param HomepageWidget $widget
     * @param bool $isPreview
     *
     * @return Response
     */
    public function __invoke(HomepageWidget $widget, $isPreview = false)
    {
        if ($isPreview && empty($widget->getSettingValue('title')) && empty($widget->getSettingValue('content'))) {
            return new Response('Please apply some settings to this widget.');
        }
        return $this->render('widgets/content.html.twig', [
            'title' => $widget->getSettingValue('title'),
            'content' => $widget->getSettingValue('content'),
        ]);
    }
}
```

> Defining the service:

```yaml
photon_cms_project.widget.website_statistics:
    class: Photon\CmsProject\Widget\WebsiteStatisticsWidget
    parent: photon.controller.widget
    arguments:
        - '@photon_cms_engine.repository.website_statistics'
    tags:
        - { name: photon.widget, widget_id: 31 }
```

Widgets can be added in Photon by creating a controller class, registering the widget in the `JaduHomepageWidgets` database table and defining a service tagged as `photon.widget` and the id of the widget in the CMS database.

The controller class for a widget is a standard Symfony controller that takes a request and returns a response. The controller must be an invokable class to be compatible with the widget system.

The widget service must be tagged with `photon.widget` and given an id. The id is used when the CMS identifies the controller to invoke, where a matching controller can not be found, the default widget controller is reverted to.

<aside class="notice">
When creating the service, the parent <code>photon.controller.widget</code> can be used to simplify the definition. This will set all of the dependencies that are required by the <code>Widget</code> base class. 
</aside>

##Customising supplements

```xml
<?xml version="1.0" encoding="utf-8"?>
<system xmlns:config="http://www.jadu.co.uk/schema/config">
    <supplements config:type="array">
        <item key="spacecraft-popular-pages">PopularPagesPageSupplementManager</item>
    </supplements>
</system>
```

Supplements can be added in Photon by creating a manager class, administration interface file and associated class.

The new supplement class must be registered with the CMS in the database table `JaduPageSupplements`. The supplement manager class must be registered in `page_supplements.xml`.