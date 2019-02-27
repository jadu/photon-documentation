#Default theme

The default theme implements all functionality provided with Jadu CMS, and provides a base from which to extend when creating a custom theme.

The default theme is maintained, and any updates available will be added either:

* when you next use Composer to update your dependencies
* when your site is patched with an updated Jadu CMS release

##CSS classes

The default theme uses [Block Element Modifier](http://getbem.com/) (BEM)naming conventions for its class names. 

Uniquely classes are set on each page of the default theme.

##Partials

The partials in the default theme are organised according to atomic design principles. 

Further information on atomic design is available in the [Atomic design blog post](http://bradfrost.com/blog/post/atomic-web-design/).


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

##Default routes & pages

The default theme consists of the following routes and associated page controllers that output their response in a template. Page controllers are found in the theme `Page` directory.

##A to Z article

A single A to Z of services entry and any associated contact details.

###Route name

`atoz_article`

###URL pattern

`/a-to-z/service/{serviceId}/{serviceSlug}`

###Layout

`Article`

###Module

`EGov`

###Page class

`atoz-article`

###Acceptance criteria

* Page errors if an invalid service ID is passed - 404 response
* Page errors if the service is offline - 404 response
* Page redirects to appropriate URL if service has redirect set
* Breadcrumb includes A-Z list
* A to Z record metadata is included in the page
* Title, content, eligibility, accessibility and availability content is rendered on the page
* Multimedia items are rendered in service document editor content
* Eligibility section is only shown if it has been completed
* Accessibility section is only shown if it has been completed
* Availability section is only shown if it has been completed
* Contacts section is only shown if it has been completed
* Each contact assigned to service is printed
* Contact name is only printed if it has been completed
* Contact department is only printed if it has been completed
* Contact email is only printed if it has been completed
* Contact telephone is only printed if it has been completed
* Contact mobile is only printed if it has been completed
* Contact fax is only printed if it has been completed
* Contact URL is only printed if it has been completed
* Contact address is only printed if it has been completed
* Contact email is rendered as a mailto: link
* Contact telephone is rendered as a tel: link
* Contact mobile is rendered as a tel: link
* Contact URL is rendered as a link
* Approved version is shown 
* HTML content is rendered unencoded

##A to Z list

Filtered list of A to Z entries and aliases.

###Route name

`atoz_list`

###URL pattern

`/a-to-z/{startsWith}`

###Layout

`List`

###Module

`EGov`

###Page class

`atoz-list`

###Acceptance criteria 

* I can view a list of A to Z records starting with the selected letter
* Each list item links to the correct A to Z article path
* A to Z record aliases are included in the list of records
* List of records appears in alphabetical order
* All records starting with a letter are shown on one page (no pagination)
* List of records can be filtered by a different letter by clicking a letter in A-Z bar
* Letters with no records are shown as disabled
* Letters with records link to the correct A to Z list path
* Message shown if no services in system

##Accessibility settings

Form to customise the appearance of the site in line with a user's accessibility needs.

###Route name

`accessibility_settings`

###URL pattern

`/accessibility/settings`

###Layout

`Form`

###Module

`Utilities`

###Page class

`accessibility-form`

###Accessibility criteria 

* Colour scheme setting is saved to session when form is submitted
* Font size setting is saved to session when form is submitted
* Font setting is saved to session when form is submitted
* Using the reset button clears saved session values
* Form can be navigated by keyboard only


##API apply

Form to apply for an API key linked with a user's account. 

###Route name

`user_account_api_apply`

###URL pattern

`/account/api/apply`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`api-form`

###Acceptance criteria 

* Must have valid user session to view
* Redirects to index if no valid user session
* Form includes description field, terms checkbox and submit button
* An error is highlighted if terms is not checked on submission
* On successful submission a api key submission is generated, redirected to user home, success message shown

##Category

Landing page of a category, including navigation to subcategories and documents relating to a single category of the site's taxonomy. 

###Route name

`document_category`

###URL pattern

`/info/{categoryId}/{categorySlug}`

###Layout

`Modular`

###Module

`Publishing`

###Page class

`category-modular`

###Acceptance criteria 

* Category specific stylesheet is used
* Page does not error if no homepage is assigned
* Page errors if an invalid category ID is passed - 404 response
* Page errors if no documents, no subcategories or no homepage assigned - 404 response
* Breadcrumb includes category path
* Modular homepage widget block is rendered as in CMS
* Approved version is shown 
* List of documents assigned to category shown
* Homepage specific metadata is not used
* Modular content only rendered if homepage assigned
* Page supplements are shown
* HTML content is rendered unencoded

##Change details

Form to update the details of a user.

###Route name

`user_account_change_detail`

###URL pattern

`/account/change-detail`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`change-details-form`

###Acceptance criteria 

* Redirects to https if ssl is enabled
* Redirects to appropriate url if user adapter change details page is specified
* Must have valid user session to view
* Redirects to index if no valid user session
* Redirects to user home if user adapter change details is disabled
* Redirects to register authorisation if email has not been authorised
* Breadcrumb includes user home
* Form includes csrf token, email address field and save changes submit button
* Salutation field, forename, surname, birthday, age, sex, occupation, company, address, city, county, postcode, country, telephone, mobile, fax, website, data protection and targetting question fields when enabled in register preferences
* Fields are prefilled with user’s current details
* Error message is shown if CSRF token invalid on submission
* Error message is shown if email address is not a string in email address format
* Error message is shown if email address matches a different registered user
* Error message is shown if salutation is not one of Mr, Miss, Mrs, Ms, Mx, Dr or other
* Error message is shown if forename is blank
* Error message is shown if surname is blank
* Error message is shown if birthday is not a valid date
* Error message is shown if birthday is not in the past
* Error message is shown if age is not a number
* Error message is shown if sex is not one of “Male” or “Female”
* Error message is shown if address is blank
* Error message is shown if city is blank
* Error message is shown if postcode is blank or includes non alphanumeric characters
* Error message is shown if country is blank
* Error message is shown if an answer is not supplied for targetting question
* If errors are found, submitted values are shown in form fields
* If no errors found, user details are updated
* If user email is updated and email authentication is enabled, authentication email is sent
* If user is updated, redirected to user home and success message shown
* Breadcrumb includes user account link

##Change password

Form to update the password of a user. 

###Route name

`user_account_change_password`

###URL pattern

`/account/change-password`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`password-reset-form`

###Acceptance criteria

* Must have valid user session to view
* Redirects to https if ssl is enabled
* Redirects to appropriate url if user adapter change password page is specified
* Redirects to index and error message shown if user not logged in 
* Form includes old password field, new password field, new password confirmation field and submit button
* Error message is shown if password is less than 6 characters
* Error message is shown if password is greater than 30 characters
* Error message is shown if new password is not the same as new password confirmation
* If no errors found, password is updated
* If password is updated, reset code is disabled.
* If password is updated, redirects to user home, success message shown
* Breadcrumb includes user account link

##Councillor article

Details of a single Councillor, including their contact details and associated image. 

###Route name

`councillor_article`

###URL pattern

`/councillors/{councillorId}/{councillorSlug}`

###Layout

`Article`

###Module

`EGov`

###Page class

`councillor-article`

###Acceptance criteria 

* Approved version is shown 
* Page errors if invalid councillor ID is passed - 404 response
* Page errors if councillor is offline - 404 response
* Breadcrumb includes councillors list
* First name, second name, image, party, ward, position, address, telephone, fax, email, content are rendered
* Page does not error if party deleted
* Page does not error if ward deleted
* Multimedia is rendered in document editor content
* Image is only printed if completed
* Image Caption is rendered if completed
* Position is only printed if completed
* Address is only printed if completed
* Telephone is only printed if completed
* Telephone is rendered as a tel: link
* Fax is only printed if completed
* Email is only printed if completed
* Email is rendered as a mailto: link
* Content is only printed if completed
* HTML content is rendered unencoded

##Councillor list

Filtered list of councillors. 

###Route name

`councillor_list`

###URL pattern

`/councillors`

###Layout

`List`

###Module

`EGov`

###Page class

`councillor-list`

###Acceptance criteria

* I can view a list of councillors
* List is not paginated
* List can be filtered by party, ward
* List of records is sorted by alphabetical order
* Each item links to valid councillor path and includes first name and surname
* Message shown if no councillors in system

##Directory article

Directory home page including description and links to A to Z of records.

###Route name

`directory_article`

###URL pattern

`/directory/{directoryId}/{directorySlug}`

###Layout

`Article`

###Module

`Publishing`

###Page class

`directory-article`

###Acceptance criteria

* Page errors if an invalid directory ID is passed - 404 response
* Page errors if directory is offline - 404 response
* Directory specific metadata is used
* Directory title, description are rendered
* Description is only printed if completed
* Call to action to directory a to z is included
* Call to action to directory submission is included
* List of directory subcategories is included
* List item includes directory name, valid path to directory category

##Directory A to Z list

List of directory records begining with a particular letter.

###Route name

`directory_atoz`

###URL pattern

`/directory/{directoryId}/a-to-z/{startsWith}`

###Layout

`List`

###Module

`Publishing`

###Page class

`directory-record-list`

###Acceptance criteria 

* Page errors if an invalid directory id is passed - 404 response
* Page errors if directory is offline - 404 response
* Directory specific metadata is used
* I can view a list of A to Z records starting with the selected letter
* Each list item links to the correct record path
* List of records appears in alphabetical order
* All records starting with a letter are shown on one page (no pagination)
* List of records can be filtered by a different letter by clicking a letter in A-Z bar
* Letters with no records are shown as disabled
* Letters with records link to the correct A to Z list path
* Message shown if no records in directory
* Breadcrumb includes directory article

##Directory record article

Details of a particular directory record article. 

###Route name

`directory_record_details`

###URL pattern

`/directory-record/{recordId}/{recordSlug}`

###Layout

`Article`

###Module

`Publishing`

###Page class

`directory-record-article`

###Acceptance criteria

* Page errors if an invalid directory id is passed - 404 response
* Page errors if directory is offline - 404 response
* Page errors if an invalid record ID is passed - 404 response
* Page errors if record is offline - 404 response
* Directory record specific metadata is used
* Breadcrumb includes directory article
* Breadcrumb includes directory category path
* Record title, and fields are rendered
* If an optional field is not completed, it is not rendered 
* Multimedia in document editor content is rendered
* Google map is rendered, and pin includes fields configured within directory settings
* Link fields are rendered as a link
* Email fields are rendered as a mailto: link
* ESRI map is rendered 
* HTML content is rendered unencoded
* Image is rendered
* Image includes valid alt attribute

##Directory search result list 

List of records matching a search term in a directory.

###Route name

`directory_search`

###URL pattern

`/directory/search`

###Layout

`Article`

###Module

`Publishing`

###Page class

`directory-result-list`

###Acceptance criteria

* Page errors if an invalid directory id is passed - 404 response
* Page errors if directory is offline - 404 response
* Directory specific metadata is used
* Breadcrumb includes directory article
* List of results is paginated
* 50 results are shown per page
* If page number is greater than 1, a previous link is shown
* If more pages exist than the current page number, a next link is shown
* List of results matches the criteria submitted
* List item includes record title and link to valid record path
* If location search, results shown on map
* Pins include fields configured within directory settings
* Message shown if no results found
* Search form is shown

##Directory record list

List of directory records in a particular category.

###Route name

`directory_category`

###URL pattern

`/directory/{directoryId}/{directorySlug}/category/{categoryId}/{pageNumber}` 

###Layout

`List`

###Module

`Publishing`

###Page class

`directory-record-list`

###Acceptance criteria 

* Page errors if directory is offline - 404 response
* Page errors if an invalid category id is passed - 404 response
* Directory specific metadata is used
* Breadcrumb includes directory article
* Breadcrumb includes directory category path
* Category adverts are included
* Category description is only rendered if completed
* List of records in category is shown
* List item includes record title and link to valid directory record path
* List of subcategories is shown
* List item includes category name and link to valid directory category path
* List of records is paginated
* 50 records shown per page
* If page number is greater than 1, a previous link is shown
* If more pages exist than the current page number, a next link is shown

##Directory record submission

Form for public submission of a new record to a directory.

###Route name

`directory_submit`

###URL pattern

`/directory/{directoryId}/{directorySlug}/submit`

###Layout

`Form`

###Module

`Publishing`

###Page class

`directory-submit-form`

###Acceptance criteria 

* Page errors if an invalid directory id is passed - 404 response
* Page errors if directory is offline - 404 response
* Directory specific metadata is used
* Breadcrumb includes directory article

##Document article

A single page of a document with navigation to all other pages in that document. 

###Route name

`document_page`

###URL pattern

`/info/{categoryId}/{categorySlug}/{documentId}/{documentSlug}/{pageNumber}` 

###Layout

`Article`

###Module

`Publishing`

###Page class

`document-article`

###Acceptance criteria 

* Category specific stylesheet is used
* Document specific metadata is used
* Breadcrumb includes category path
* I can preview a document page
* Preview includes accessibility check javascript
* Approved version is shown 
* Page errors if an invalid document ID is passed - 404 response
* Page errors if a category ID not assigned to document is passed - 301 response, redirect to valid category
* Page errors if an invalid page number is passed - 404 response
* If no page number passed, default page number 1 is used
* If password protected and not authenticated, message and password form shown
* Submitting valid password in password form is saved against session
* If password protected and authenticated, or not password protected, document content is shown
* If access level is greater than current session, permission denied message shown
* If access level is less than or equal to current session, document content is shown
* Document title, page title, image, page content are rendered on page
* If document title is the same as page title, only document title is shown
* Image is only shown when completed
* Caption is rendered when completed
* Multimedia content is rendered in document editor content
* List of pages is shown if there are more than one page in document
* Current page is highlighted as active in the list
* Each list item is page title and link to valid document page path
* If page number is greater than 1, previous link is shown
* If page number is less than total number of pages, next link is shown
* Page supplements are shown
* HTML content is rendered unencoded

##Download article

Details of a single download, with a links to download all associated files. 

###Route name

`download_article`

###URL pattern

`/downloads/download/{downloadId}/{downloadSlug}`

###Layout

`Article`

###Module

`Publishing`

###Page class

`download-article`

###Acceptance criteria 

* Category specific stylesheet is used
* Page errors if an invalid download id is used - 404 response
* Page errors if download is offline - 404 response
* Page does not error if download if not visible - 200 response
* Approved version is shown 
* If password protected and not authenticated, message and password form shown
* Submitting valid password in password form is saved against session
* If password protected and authenticated, or not password protected, download content is shown
* Download title, description, list of files is rendered
* Each uploaded file includes filename, file size, extension and link to valid download path
* Each linked file includes filename and link to external path
* Description is only shown if completed

##Download file

Stream a file.

###Route name

`file_download`

###URL pattern

`/downloads/file/{fileId}/{fileSlug}`

###Layout

n/a - no HTML output

###Module

`Publishing`

##Event article

A single event and associated image. 

###Route name

`event_article`

###URL pattern

`/events/event/{eventId}/{eventSlug}`

###Layout

`Article`

###Module

`Publishing`

###Page class

`event-article`

###Acceptance criteria 

* I can view an event
* Page errors if an invalid event ID is passed - 404 response
* Page errors if the event is offline - 404 response
* Breadcrumb includes events list
* I can preview an event
* Event specific metadata is used
* Title, event date, date interval, event time, location address, esri map, cost, summary, image, content are rendered on the page
* Multimedia items are rendered in event document editor content
* Interval is only shown if it has been completed
* ESRI map is only shown if integration is enabled
* Time is only shown if it has been completed
* Document editor content is only shown if it has been completed
* Image is only shown if it has been completed
* Image caption is shown where it has been added
* Approved version is shown 
* Page does not error if location deleted
* HTML content is rendered unencoded

##Event list

Filtered and paginated list of events.

###Route name

`event_list`

###URL pattern

`/events`

###Layout

`List`

###Module

`Publishing`

###Page class

`event-list`

###Acceptance criteria 

* I can view a list of events
* A call to action is shown to submit your event
* 10 events are shown per page
* If page number is greater than 1, a previous link is shown
* If more pages exist than the current page number, a next link is shown
* Each event includes, title, summary, event date
* Each event links to a valid event path
* List of events can be filtered by date and location
* Events are shown in chronological order - from today ascending
* Message shown if no events in system

##Event submission

Form for public submission of a new event.

###Route name

`event_submission`

###URL pattern

`/event/new`

###Layout

`Form`

###Module

`Publishing`

###Page class

`event-submit-form`

###Acceptance criteria 

* Form includes title, start date, interval, end date, start time, end time, location, new location, cost, summary, description, image fields and submit button
* Error shown if start date is invalid date format or empty
* Error shown if end date is invalid date format
* Error shown if auth field is empty or invalid content
* Error shown if title empty or greater than 255 characters
* Error shown if new location is greater than 255 characters
* Error shown if location does not match a valid location id
* Error shown if summary is empty or greater than max summary character limit
* Error shown if description is greater than 65535 characters
* Error shown if start time is not in time format
* Error shown if end time is not in time format
* Error shown if cost is empty or greater than 255 characters
* Error shown if start date is after end date
* Error shown if image is not an image file of type jpg, jpeg, gif or png
* If errors are found, submitted values are shown in form fields
* If no errors found, event is submitted and image uploaded
* Image should be appended to description of submitted event
* Submitted event should not be live and visible on the website immediately after submission
* Image should appear in the site image library with valid title
* Event should have valid metadata
* Email notification of new event submission should be sent
* If event submitted, redirect to event list and show success message

##Forgot password

Form to request a password reset link. 

###Route name

`user_account_forget_password`

###URL pattern

`/account/forgot-password`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`forgot-password-form`

###Acceptance criteria

* Redirects to https if ssl is enabled
* Redirects to appropriate url if user adapter forgot password page is specified
* Redirects to signin page if user adapter change details is disabled
* Form includes email address field and submit button
* Error message shown if email is not valid format
* Password reset email sent if email matches an existing user
* Success message shown if password reset email is sent

##Index

The main homepage of the site.

###Route name

`index`

###URL pattern

`/`

###Layout

`Modular`

###Module

`Publishing`

###Page class

`index-modular`

###Acceptance criteria 

* No breadcrumb is shown
* Homepage specific stylesheet is used
* No h1 is shown
* Page does not error if no homepage is available
* Homepage specific metadata is used
* Approved version is shown 
* Modular homepage widget block is rendered as in CMS
* HTML content is rendered unencoded
* Homepage content relates to the independent homepage with highest position

##Homepage

A single independent landing page.

###Route name

`homepage`

###URL pattern

`/homepage/{homepageId}/{homepageSlug}`

###Layout

`Modular`

###Module

`Publishing`

###Page class

`homepage-modular`

###Acceptance criteria 

* Homepage specific stylesheet is used
* Page errors if an invalid homepage ID is passed - 404 response
* I can preview a homepage
* Preview includes accessibility check javascript
* Breadcrumb includes category path
* Homepage specific metadata is used
* Modular homepage widget block is rendered as in CMS
* Approved version is shown 
* Page supplements are shown
* HTML content is rendered unencoded
* Hide navigation uses a one column layout

##Meeting article

Details of a single meeting, including any agendas, minutes and other attachments.

###Route name

`meeting_article`

###URL pattern

`/meetings/meeting/{meetingId}/{meetingSlug}`

###Layout

`Article`

###Module

`EGov`

###Page class

`meeting-article`

###Acceptance criteria

* I can view a meeting article
* Page errors if an invalid meeting ID is provided - 404 response
* Page errors if meeting is offline - 404 response
* Breadcrumb includes a link to meeting list
* Committee title, meeting date, list of attachments are rendered on page
* Multimedia content in document editor content is rendered
* Meeting attachments can be downloaded
* HTML content is rendered unencoded
* Attachment types appear in the configured order
* Attachments are grouped by type
* Attachments appear in the configured position in their list
* Meeting specific metadata is used

##Meeting download

 Stream a meeting file attachment.

###Route name

`meeting_download`

###URL pattern

`/download/meetings/id/{attachmentId}/{attachmentSlug}`

###Layout

n/a - no HTML output

###Module

`EGov`

##Meeting list

Filtered and paginated list of meetings.

###Route name

`meeting_list`

###URL pattern

`/meetings`

###Layout

`List`

###Module

`EGov`

###Page class

`meeting-list`

###Acceptance criteria

* I can view a list of meetings
* Only live meetings are shown in the list
* List is ordered by meeting date ascending
* Current page defaults to today where no filter options are set
* Meetings can be filtered by committee
* Meetings can be filtered by committee status (archived/current)
* 10 meetings are rendered per page
* Each list item links to valid meeting path
* If page number is greater than 1, a previous link is shown
* If more pages exist than the current page number, a next link is shown
* Message shown if no meetings in system

##News article

A single news article and associated image.

###Route name

`news_article`

###URL pattern

`/news/article/{articleId}/{articleSlug}`

###Layout

`Article`

###Module

`Publishing`

###Page class

`news-article`

###Acceptance criteria 

* I can preview a news article
* Page errors if an invalid news ID is passed - 404 response
* Page errors if the news article is offline - 404 response
* Breadcrumb includes news list
* Category specific stylesheet is used
* News article specific metadata is used
* Title, summary, image, content, news date content is rendered on the page
* Image is only rendered if it has been completed
* If image has caption, caption is shown
* News date is rendered in a recognised date format
* Multimedia items are rendered in article document editor content
* Approved version is shown 
* HTML content is rendered unencoded

##News list

Filtered and paginated list of news articles.

###Route name

`news_list`

###URL pattern

`/news`

###Layout

`List`

###Module

`Publishing`

###Page class

`news-list`

###Acceptance criteria 

* I can view a list of news articles
* News articles are shown in chronological order - newest to oldest
* 10 articles are shown per page
* If page number is greater than 1, a previous link is shown
* If more pages exist than the current page number, a next link is shown
* List of news articles can be filtered by year and month
* Each article links to valid news article path
* Each article shows title, summary and news date
* Message shown if no news items in system

##Offline

Holding page shown when the site has been taken offline.

###Route name

`site_offline`

###URL pattern

`/offline`
 
###Layout

`Article`

###Module

`Utilities`

###Page class

`offline-article`

###Acceptance criteria

* If site is offline, 40X response
* Offline exception page is shown

##Password reset

Form to input a new password. 

###Route name

`user_account_password_reset`

###URL pattern

`/account/password-reset/{resetCode}`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`password-reset-form`

###Acceptance criteria

* Redirects to https if ssl is enabled
* Redirects to appropriate url if user adapter change password page is specified
* Redirects to index and error message shown if user not logged in and password reset code invalid
* Redirects to user home and error message shown if user logged in and password reset code invalid
* Form includes old password field, new password field, new password confirmation field and submit button
* If change has been forced, forced hidden input printed
* Error message is shown if password is less than 6 characters
* Error message is shown if password is greater than 30 characters
* Error message is shown if new password is not the same as new password confirmation
* If errors are found, submitted values are shown in form fields
* If no errors found, password is updated
* If password is updated, reset code is disabled.

##Register

Form to create a new user account.

###Route name

`user_registration`

###URL pattern

`/register`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`registration-form`

###Acceptance criteria 

* Redirects to https if ssl is enabled
* Redirects to change details if valid user session
* Redirects to sign in if user adapter register is disabled
* Form includes csrf token, email address field, email address confirmation, password, password confirmation and register submit button
* Salutation field, forename, surname, birthday, age, sex, occupation, company, address, city, county, postcode, country, telephone, mobile, fax, website, data protection and targetting question fields when enabled in register preferences
* Error message is shown if CSRF token invalid on submission
* Error message is shown if password is less than 6 characters
* Error message is shown if password is greater than 30 characters
* Error message is shown if password is not the same as password confirmation
* Error message is shown if email address is empty
* Error message is shown if email address is not a string in email address format
* Error message is shown if email address matches a different registered user
* Error message is shown if email address is not the same as email confirmation
* Error message is shown if salutation is not one of Mr, Miss, Mrs, Ms, Mx, Dr or other
* Error message is shown if forename is blank
* Error message is shown if surname is blank
* Error message is shown if birthday is not a valid date
* Error message is shown if birthday is in the future
* Error message is shown if age is not a number
* Error message is shown if age is blank
* Error message is shown if sex is not one of “Male” or “Female”
* Error message is shown if address is blank
* Error message is shown if city is blank
* Error message is shown if postcode is blank or includes non alphanumeric characters
* Error message is shown if country is blank
* Error message is shown if an answer is not supplied for targetting question
* If errors are found, submitted values are shown in form fields
* If no errors found, user is registered
* If email authentication is enabled, authentication email is sent, redirected to index and info message is shown
* If user is registered, redirected to user home and success message shown

##Restricted content login

Form used to access a restricted Galaxies site. 

###Route name

`restricted`

###URL pattern

`/restricted`

###Layout

`Article`

###Module

`Utilities`

##RSS

An RSS feed of recently published content

###Route name

`content_rss`

###URL pattern

`/rss/{contentType}`

###Layout

n/a - no HTML output

###Module

`Publishing`

##Search list

List of search results provided by the site's search provider.

###Route name

`search_list`

###URL pattern

`/site-search/results/`

###Layout

`List`

###Module

`Utilities`

###Page class

`search-list`


##Sign in 

Form to sign in to an existing user account. 

###Route name

`user_account_signin`

###URL pattern

`/account/signin`

###Layout

`Form`

###Module

`MyAccount`

###Page class

`signin-form`

###Acceptance criteria

* Redirects to https if ssl is enabled 
* Form includes email address, password, sign in button
* Error message is shown if details do not match user in system 
* Error message doesn’t specify the incorrect value
* If details match valid user, user session started, user redirected to user account, success message shown

##Unsubscribe

Form to unsubscribe from marketing newsletters sent by the site. 

###Route name

`unsubscribe`

###URL pattern

`/account/unsubscribe`
 
###Layout

`Form`

###Module

`MyAccount`

###Page class

`unsubscribe-form`

###Acceptance criteria

* If user id and email match valid user from database, success message shown, redirect to index
* If user id and email do not match valid user from database, error message shown, redirect to index
* If valid user from database is found, data protection value is changed to 0

##User home

User's account page detailing interactions with the site.

###Route name

`user_home`

###URL pattern

`/account`

###Layout

`List`

###Module

`MyAccount`

###Page class

`user-home-list`

###Acceptance criteria

* Redirects to https if ssl is enabled
* Must have valid user session to view
* Redirects to appropriate url if user adapter user home page is specified
* If user email authorisation is pending, message is shown and other functions disabled
* Submitted directory entries are shown on user home
* Valid api keys are shown on user home
* Welcome message naming user is shown
* If user adapter allows change details, link is shown
* If user adapter allows change password, link is shown
* Link is shown to logout of account

##Non-HTML response routes

For the following routes, output comes directly from the controller and is not rendered in a template:

* meeting_download
* content_rss
* file_download
* logout