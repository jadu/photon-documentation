# Default theme

The default theme implements all functionality provided with Jadu CMS, and provides a base from which to extend when creating a custom theme.

The default theme is maintained, and any updates available will be added either:

* when you next use Composer to update your dependencies
* when your site is patched with an updated Jadu CMS release

## Page classes

The default theme uses [Block Element Modifier](http://getbem.com/) (BEM)naming conventions for its class names. 

Uniquely classes are set on each page of the default theme. For reference, these are:

Page | Class name
-----|-----------
A to Z article | atoz-article
A to Z list | atoz-list
Councillor article | councillor-article
Councillor list | councillor-list
Meeting article | meeting-article
Meeting list | meeting-list
Account | user-home-list
Sign in | signin-form
API key application | api-form 
Change details | change-details-form
Change password | password-reset-form
Forgot password | forgot-password-form
Reset password | password-reset-form
Register | registration-form
Unsubscribe | unsubscribe-form
Directory landing page | directory-article
Directory A to Z list | directory-record-list
Directory record | directory-record-article
Directory search results | directory-result-list
Directory category list | directory-record-list
Directory submission | directory-submit-form
Document | document-article
Download landing page | download-article
Event article | event-article
Event list | event-list 
Event submission | event-submit-form
Category landing page | category-modular
Standalone homepage | homepage-modular
Index | index-modular 
News article | news-article 
News list | news-list
Accessibility settings | accessibility-form
Search results | search-list
Offline page | offline-article

##Partials

The partials in the default theme are organised according to atomic design principles. 

Further information on atomic design is available in the [Atomic design blog post](http://bradfrost.com/blog/post/atomic-web-design/).

##Non-HTML response routes

For the following routes, output comes directly from the controller and is not rendered in a template:

* meeting_download
* content_rss
* file_download
* logout

##Hard coded text

```twig
{{ 
    getTranslatedString(
        'password-reset-email-ip-statement', 
        [app.request.getClientIp()]
    ) 
}}
```

> Within page and component controllers, translated text can be retrieved using the function `getTranslatedString()` of `Photon\Core\Controller\Page`. 

```php
<?php

$crumb->setTitle($this->getTranslatedString('az-page-link'));
```

Hard coded text in templates is managed using the Language Pack module in Jadu CMS.

A non-technical user interface is provided to add, update and remove text in the language pack.

Photon provides functions to retrieve the appropriate text based on the locale associated with the site.

The function to retrieve text takes two arguments:

* the reference for the string to retrieve.
* an array of parameters to replace placeholders in the text (optional).


### Site locale

The locale of a site is set within the JaduLanguagePacksToSites database table. Where no matching record is found, requests for text fallback to the language pack installed with the CMS.

New language packs can be defined within the CMS and are associated with a locale. Available locales are defined within the JaduLanguageLocales database table.

## Layouts

The default template set makes use of template inheritance in Twig to reduce repetition and ease maintenance. 

The primary template is `base.html.twig`. The base template defines the HTML skeleton of the page and a number of block tags that a child template may override or extend. 

Further information on extending templates can be found in [Twig documentation](https://twig.symfony.com/doc/1.x/tags/extends.html).

### Article

A page on a single topic with a title and body of content.

* A to Z article
* Councillor article
* Meeting article
* News article
* Event article
* Download article
* Document article
* Directory article
* Directory record article
* Offline page

### List

A list of records or articles, that may be paginated or filterable.

* A to Z list
* Councillor list
* Meeting list
* User home
* News list
* Default category homepage
* Event list
* Directory search results
* Directory record list
* Search result list

### Modular

A page of content made up of blocks of widgets.

* Index
* Standalone homepage
* Category homepage

### Form

A HTML form.

* API apply
* Change details
* Forgot password
* Password reset
* Registration
* Sign in
* Unsubscribe
* Event submission
* Directory submission
* Accessibility settings