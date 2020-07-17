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

## Limiting changes to specific Galaxies sites

When building your Galaxies site, you may want to prevent some functionality from taking effect on any other sites. All Galaxies Theme bundles are loaded in globally, regardless of which site is being requested.

The `bundles.xml` configuration file allows you to define additional bundles to be loaded for specific Galaxies sites based on the site's database name. It is recommended that any customisations to the functionality of a single site (for example custom routing) are created in a bundle separate to the site's theme and then registered in `bundles.xml`.

To register an additional bundle for a specific site, add an XML element `galaxy<GALAXY_DATABASE_NAME>` to your `bundles.xml` configuration.

> For example, to ensure galaxy with database 'ms_jadudb_1' only loads 'MyGalaxyBundle'.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<bundles xmlns:config="http://www.jadu.co.uk/schema/config">
  <!-- ... -->
  
  <galaxyms_jadudb_1 config:type="array">
      <item key="my-galaxy">MyGalaxyTheme\MyGalaxyBundle</item>
  </galaxyms_jadudb_1>
</bundles>
```
