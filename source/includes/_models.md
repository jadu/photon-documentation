#Models

```php
<?php

namespace Photon\CmsEngine\Model\Element;

class Article
{
    /**
     * @var Link
     */
    private $link;
    
    /**
     * @param Link $link
     * 
     * @return Article
     */
    public function setLink($link)
    {
        $this->link = $link;

        return $this;
    }
    
    /** 
     * @return Link
     */
    public function getLink()
    {
        return $this->link;
    }
}
```

> You can use a dot (.) to access attributes of a model variable in twig

```twig
{{ article.title }}
{{ article.link.url }}
```

A number of model classes are provided to format data for pages and ensure a consistent interface when accessing data from different areas of the CMS.

The attributes of the model are accessed using getter and setter functions in PHP. Calls to setter methods can be chained for ease of use.

##Article

```php
<?php

use Photon\CmsEngine\Model\Element\Article;

$article = new Article();
$article->setTitle($item->getTitle());
$article->setSummary($item->getSummary());
$article->setBody($item->getDescription());
$article->setImage($item->getImage());

$article->addMeta(
    $this->getTranslatedString('date-label'),
    $this->getMetaElement(
        $this->getTranslatedString('date-label'),
        $item->getEventDate(),
        'string'
    )
);
```

This model defines a generic article page.

###Classname

`Photon\CmsEngine\Model\Element\Article`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$image | Image | Featured image of the article
$title | string | Title of the article
$subTitle | string | Subtitle of the article
$summary | string | A brief summary of the article
$body | string | Rich text content that makes up the body of the article
$meta | array | Array of metadata on this article
$supplements | array | Array of supplements associated with this article
$passwordProtected | boolean | Whether this content is password protected
$restricted | boolean | Whether access to this content is restricted
$navigation | array | Array of navigation links 
$pagination | array | Array of pagination links
$link | Link | Link to this article

##Form

```php
<?php

use Photon\CmsEngine\Model\Element\Form;
use Photon\CmsEngine\Model\Element\FormControl;

$form = new Form();
$form->setTitle($title);
$form->setMethod('post');

$control = new FormControl();
$control->setName('_token');
$control->setType('hidden');
$form->addControl($control);

$control = new FormControl();
$control->setLabel($emailLabel);
$control->setName('email');
$control->setType('email');
$control->setValue('');
$control->setMandatory(true);
$control->setAutocomplete(false);
$form->addControl($control);

$control = new FormControl();
$control->setLabel($passwordLabel);
$control->setName('password');
$control->setType('password');
$control->setValue('');
$control->setMandatory(true);
$control->setAutocomplete(false);
$form->addControl($control);

$control = new FormControl();
$control->setLabel($signinButtonLabel);
$control->setName('jaduSignInButton');
$control->setType('submit');
$form->setPrimaryAction($control);
```

This model defines a form, including a list of form controls to submit data to the page.

###Classname

`Photon\CmsEngine\Model\Element\Form`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$id | integer | The id of this form in the database, where the form is content managed
$title | string | The title of the form
$controls | array | An array of form controls that make up this form page
$errors | array | An array of errors found in the form following validation
$action | string | The content of the action attribute of the form HTML element
$method | string | The content of the method attribute of the form HTML element
$formHeading | string | The title of this form page
$instructions | string | Rich text content that makes up the instructions of the form page
$primaryAction | FormControl | The form control that forms the primary action of the form, often a submit button
$secondaryAction | FormControl | The form control that forms the secondary action of the form, often a cancel or back button

##FormControl

```php
<?php

use Photon\CmsEngine\Model\Element\FormControl;

$control = new FormControl();
$control->setLabel($passwordLabel);
$control->setName('password');
$control->setType('password');
$control->setValue('');
$control->setMandatory(true);
$control->setAutocomplete(false);
```

A single form control and its associated values, such as label and help text.

###Classname

`Photon\CmsEngine\Model\Element\FormControl`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$id | integer | The id of this form control in the database, where the form is content managed
$label | string | The label of the form control
$options | array | An array of form control options, for example in a select or radio button group
$name | string | The content of the name attribute of the form control's HTML element
$value | string | The content of the value attribute of the form control's HTML element
$type | string | The type of form control HTML element to use in the template
$error | boolean | Whether validation found an error in this control
$autocomplete | boolean | Whether the autocomplete attribute should be disabled for this control
$disabled | boolean | Whether this control is disabled in the user interface
$help | string | The help text to display with this form control
$maxlength | integer | The content of the maxlength attribute of the form control's HTML element
$mandatory | boolean | Whether this control must be completed prior to successful submission
$className | string | Additional CSS class name data associated with this control
$placeholder | string | The content of the placeholder attribute of the form control's HTML element

##FormControlOption

```php
<?php

use Photon\CmsEngine\Model\Element\FormControlOption;

$option = new FormControlOption();
$option->setValue('')
    ->setText('All Categories');
$options[] = $option;

foreach ($topLevelCategories as $topLevelCategory) {
    $option = new FormControlOption();
    $option->setValue($topLevelCategory->getId())
        ->setText($topLevelCategory->getTitle());
    $options[] = $option;
}
```

A single option for a form control, such as a select or radio button group.

###Classname

`Photon\CmsEngine\Model\Element\FormControlOption`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$value | string | The content of the value attribute of the form control's HTML element
$text | string | The label for this option

##Link

```php
<?php

use Photon\CmsEngine\Model\Element\Link;

$azLink = new Link();
$azLink->setTitle($char);
$azLink->setUrl(
    $this->urlGenerator->generate(
        'atoz_list',
        [
            'startsWith' => $char,
        ]
    )
);
$azLink->setDisabled($count > 0);
```

A link element, including the link destination and label text. 

###Classname

`Photon\CmsEngine\Model\Element\Link`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$url | string | The content of the href attribute of the link's HTML element
$title | string | The text the link will be applied to
$subtitle | string | Additional text that the link will be applied to, commonly used to split the title to allow additional HTML elements to be applied and styled differently
$active | boolean | The link has been selected 
$disabled | boolean | The link should be displayed as disabled in the user interface


##Listing

```php
<?php

use Photon\CmsEngine\Model\Element\Listing;

$listing = new Listing();
$listing->setTitle($azPageTitle);

$listItems = $this->getRecordList($items, $aliasitems);
if ($listItems) {
    $listing->addList($listItems);
}

$listing->setAZLinkList(
    $this->buildAZLinkListBar()
);
```

A generic list page.

###Classname

`Photon\CmsEngine\Model\Element\Listing`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$filterBar | Form | A form for filtering the content of this list
$pagination | array | Array of pagination links
$feature | Article | Featured article from the list on this page
$title | string | The title of the page
$azLinkList | array | Array of A to Z navigation links for filtering the content of this list
$lists | array | Array of lists to display on this page


##ListItem

```php
<?php

use Photon\CmsEngine\Model\Element\ListItem;

$list = new ListItem();
$list->setType('record');
$list->setItems($records);
```

An array of records or articles. 

###Classname

`Photon\CmsEngine\Model\Element\ListItem`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$title | string | The title of the list
$items | array | Array of article or link objects that make up this list
$type | string | The type of list, for example "record" or "article"

##Meta

```php
<?php

use Photon\CmsEngine\Model\Element\Meta;

$meta = new Meta();
$meta->setTitle($title);
$meta->setValue($value);
$meta->setType($type);
```

A snippet of content related to an article, for example the published date.

###Classname

`Photon\CmsEngine\Model\Element\Meta`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$value | string | The value of the metadata defined
$title | string | The label for the metadata defined
$type | string | The type of the value, for example "string" or "date"

##Modular

```php
<?php

use Photon\CmsEngine\Model\Element\Modular;

$modular = new Modular();
$modular->setHomepage($homepage);
$modular->setTitle($homepage->getTitle());
$modular->setSupplements($this->getSupplements($homepage));
```

Generic modular page for use with Jadu CMS Homepage content type.

###Classname

`Photon\CmsEngine\Model\Element\Modular`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$title | string | The title of the page
$homepage | Homepage | The modular content block of the page
$supplements | array | Array of supplements associated with this article
$navigation | array | Array of navigation links 
$documents | array | Array of document records associated with this page

##Page

```php
<?php

use Photon\CmsEngine\Model\Element\Page;

$page = new Page();
$page->setContent($article);
$page->setBreadcrumb($this->getBreadcrumb());
$page->setMetadata($this->getMetadata());
$page->setBodyClass('councillor-article');
```

A generic page, including elements such as metadata and breadcrumb.

###Classname

`Photon\CmsEngine\Model\Element\Page`

###Attributes

Attribute | Type | Description
-----------|--------|---------------------------
$breadcrumb | array | Array of breadcrumb links
$navigation | array | Array of navigation links
$content | Modular/Listing/Article/Form | The main content block of the page
$metadata | array | HTML metadata values
$attributes | array | Array of key value pairs associated with the page
$bodyClass | string | Additional CSS class name to be printed on the body HTML element
