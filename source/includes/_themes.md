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

When developing a theme for use within a Galaxies site, you may want to prevent changes made taking effect on any other sites (e.g. a custom theme route).

This can be achieved by adding an XML element `galaxy<GALAXY_DATABASE_NAME>` to your `bundles.xml` configuration. This will  tell Jadu to only load the bundle(s) listed for the site with the given database name.

**Please note:** This configuration section should not contain PhotonTheme bundles - these are loaded globally on **all** requests. Separate bundles should be created for any Galaxies Sites that require customisations, such as specific routing.

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
