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
