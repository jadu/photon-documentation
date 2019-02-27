---
title: Photon reference

toc_footers:
  - <a href="mailto:sarah@jadu.co.uk">Have a technical question?</a>
  - <a href="mailto:sarah@jadu.co.uk">Spotted an error?</a> 
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - themes
  - controllers
  - routes
  - models
  - default
  - differences
  - custom
  - troubleshooting

search: true
---

# Introduction

Photon is a PHP library built by Jadu to power templates for Jadu CMS.

New template sets are implemented as Symfony bundles and registered with the CMS by either amending the `bundles.xml` configuration file or running the register theme terminal command.

Templates are extensible and can be overridden easily. In common with many Symfony applications, routes are defined in the configuration file `routes.yml`, controller dependencies are set in the configuration file `services.yml`.

Photon is built upon the Symfony framework, so having a good knowledge of the framework and Twig template language is beneficial. The following guides from the Symfony documentation are a good starting point: 

* [Symfony Getting Started Guide](http://symfony.com/doc/2.8/setup.html)
* [Understanding the Service Container](http://symfony.com/doc/current/service_container.html)

Extensive documentation is also provided for Twig:

* [Twig documentation](https://twig.symfony.com/doc/1.x/)




