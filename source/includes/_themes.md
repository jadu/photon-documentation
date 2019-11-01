#Themes

Each theme within Photon is defined as a Symfony bundle.

## Whats in a theme bundle?

Each theme bundle contains a single theme. 

Themes extend one another, so a theme bundle need not be exhaustive.

Typically a theme will contain:

* **Pages**: controllers responsible for fetching the content from a *Repository* and redering a *Template*
* **Components**: controllers responsible for rendering a fragment to be embedded within a *Template*
* **Theme**: A simple PHP class that registers the theme and specifies paths to *Resources*
* **Resources**: a colletion of Twig templates, configuration files and static assets
* **Widgets**: controllers responsible for rendering a widget

Further information on the Bundle system is available in the Symfony documentation - [The Bundle System](https://symfony.com/doc/2.8/bundles.html).

##Registering a theme

> A command is provide to easily register Galaxies site themes with the CMS.

```shell
php cli.php cms:theme-register /absolute/path/to/theme
```

Themes must be registered with the CMS so that they are loaded by the Symfony kernel when it is booted. This can be done via running the `cms:theme-register` command.

## Limiting themes for Galaxies sites

When developing a theme for use within a Galaxies site, you may want to limit the loaded theme bundles to prevent unwanted resources being available for that Galaxies site (e.g. a custom theme route).

This is possible by adding an XML element `galaxy<GALAXY_DATABASE_NAME>` to your `bundles.xml` configuration, which will limit the theme bundles loaded by the Symfony kernel for that Galaxies site.


> For example, to ensure galaxy with database 'ms_jadudb_1' only loads 'MyGalaxyThemeBundle'.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<bundles xmlns:config="http://www.jadu.co.uk/schema/config">
  <!-- ... -->
  
  <galaxyms_jadudb_1 config:type="array">
      <item key="my-galaxy-theme">MyGalaxyTheme\MyGalaxyThemeBundle</item>
  </galaxyms_jadudb_1>
</bundles>
