#Default routes

The default theme consists of the following routes and associated page controllers that output their response in a template. Page controllers are found in the theme `Page` directory.

##A to Z article

A single A to Z of services entry and any associated contact details.

###Route name

`atoz_article`

###URL pattern

`/a-to-z/service/{serviceId}/{serviceSlug}`

###Type

`Article`

###Module

`EGov`

##A to Z list

Filtered list of A to Z entries and aliases.

###Route name

`atoz_list`

###URL pattern

`/a-to-z/{startsWith}`

###Type

`List`

###Module

`EGov`

##Accessibility settings

Form to customise the appearance of the site in line with a user's accessibility needs.

###Route name

`accessibility_settings`

###URL pattern

`/accessibility/settings`

###Type

`Form`

###Module

`Utilities`

##API apply

Form to apply for an API key linked with a user's account. 

###Route name

`user_account_api_apply`

###URL pattern

`/account/api/apply`

###Type

`Form`

###Module

`MyAccount`

##Category

Landing page of a category, including navigation to subcategories and documents relating to a single category of the site's taxonomy. 

###Route name

`document_category`

###URL pattern

`/info/{categoryId}/{categorySlug}`

###Type

`Modular`

###Module

`Publishing`

##Change details

Form to update the details of a user.

###Route name

`user_account_change_detail`

###URL pattern

`/account/change-detail`

###Type

`Form`

###Module

`MyAccount`


##Councillor article

Details of a single Councillor, including their contact details and associated image. 

###Route name

`councillor_article`

###URL pattern

`/councillors/{councillorId}/{councillorSlug}`

###Type

`Article`

###Module

`EGov`

##Councillor list

Filtered list of councillors. 

###Route name

`councillor_list`

###URL pattern

`/councillors`

###Type

`List`

###Module

`EGov`

##Directory article

Directory home page including description and links to A to Z of records.

###Route name

`directory_article`

###URL pattern

`/directory/{directoryId}/{directorySlug}`

###Type

`Article`

###Module

`Publishing`

##Directory a to z list

List of directory records begining with a particular letter.

###Route name

`directory_atoz`

###URL pattern

`/directory/{directoryId}/a-to-z/{startsWith}`

###Type

`List`

###Module

`Publishing`

##Directory record article

Details of a particular directory record article. 

###Route name

`directory_record_details`

###URL pattern

`/directory-record/{recordId}/{recordSlug}`

###Type

`Article`

###Module

`Publishing`

##Directory search result list 

List of records matching a search term in a directory.

###Route name

`directory_search`

###URL pattern

`/directory/search`

###Type

`Article`

###Module

`Publishing`

##Directory record list

List of directory records in a particular category.

###Route name

`directory_category`

###URL pattern

`/directory/{directoryId}/{directorySlug}/category/{categoryId}/{pageNumber}` 

###Type

`List`

###Module

`Publishing`

##Directory record submission

Form for public submission of a new record to a directory.

###Route name

`directory_submit`

###URL pattern

`/directory/{directoryId}/{directorySlug}/submit`

###Type

`Form`

###Module

`Publishing`

##Document article

A single page of a document with navigation to all other pages in that document. 

###Route name

`document_page`

###URL pattern

`/info/{categoryId}/{categorySlug}/{documentId}/{documentSlug}/{pageNumber}` 

###Type

`Article`

###Module

`Publishing`

##Download article

Details of a single download, with a links to download all associated files. 

###Route name

`download_article`

###URL pattern

`/downloads/download/{downloadId}/{downloadSlug}`

###Type

`Article`

###Module

`Publishing`

##Download file

Stream a file.

###Route name

`file_download`

###URL pattern

`/downloads/file/{fileId}/{fileSlug}`

###Type

n/a - no HTML output

###Module

`Publishing`

##Event article

A single event and associated image. 

###Route name

`event_article`

###URL pattern

`/events/event/{eventId}/{eventSlug}`

###Type

`Article`

###Module

`Publishing`

##Event list

Filtered and paginated list of events.

###Route name

`event_list`

###URL pattern

`/events`

###Type

`List`

###Module

`Publishing`

##Event submission

Form for public submission of a new event.

###Route name

`event_submission`

###URL pattern

`/event/new`

###Type

`Form`

###Module

`Publishing`

##Forgot password

Form to request a password reset link. 

###Route name

`user_account_change_password`

###URL pattern

`/account/change-password`

###Type

`Form`

###Module

`MyAccount`

##Index

The main homepage of the site.

###Route name

`index`

###URL pattern

`/`

###Type

`Modular`

###Module

`Publishing`

##Homepage

A single independent landing page.

###Route name

`homepage`

###URL pattern

`/homepage/{homepageId}/{homepageSlug}`

###Type

`Modular`

###Module

`Publishing`

##Meeting article

Details of a single meeting, including any agendas, minutes and other attachments.

###Route name

`meeting_article`

###URL pattern

`/meetings/meeting/{meetingId}/{meetingSlug}`

###Type

`Article`

###Module

`EGov`

##Meeting download

 Stream a meeting file attachment.

###Route name

`meeting_download`

###URL pattern

`/download/meetings/id/{attachmentId}/{attachmentSlug}`

###Type

n/a - no HTML output

###Module

`EGov`

##Meeting list

Filtered and paginated list of meetings.

###Route name

`meeting_list`

###URL pattern

`/meetings`

###Type

`List`

###Module

`EGov`

##News article

A single news article and associated image.

###Route name

`news_article`

###URL pattern

`/news/article/{articleId}/{articleSlug}`

###Type

`Article`

###Module

`Publishing`

##News list

Filtered and paginated list of news articles.

###Route name

`news_list`

###URL pattern

`/news`

###Type

`List`

###Module

`Publishing`

##Offline

Holding page shown when the site has been taken offline.

###Route name

`site_offline`

###URL pattern

`/offline`
 
###Type

`Article`

###Module

`Utilities`

##Password reset code

Form to input a new password. 

###Route name

`user_account_password_reset`

###URL pattern

`/account/password-reset/{resetCode}`

###Type

`Form`

###Module

`MyAccount`

##Register

Form to create a new user account.

###Route name

`user_registration`

###URL pattern

`/register`

###Type

`Form`

###Module

`MyAccount`

##Restricted content login

Form used to access a restricted Galaxies site. 

###Route name

`restricted`

###URL pattern

`/restricted`

###Type

`Article`

###Module

`Utilities`

##RSS

An RSS feed of recently published content

###Route name

`content_rss`

###URL pattern

`/rss/{contentType}`

###Type

n/a - no HTML output

###Module

`Publishing`

##Search list

List of search results provided by the site's search provider.

###Route name

`search_list`

###URL pattern

`/site-search/results/`

###Type

`List`

###Module

`Utilities`

##Sign in 

Form to sign in to an existing user account. 

###Route name

`user_account_signin`

###URL pattern

`/account/signin`

###Type

`Form`

###Module

`MyAccount`

##Unsubscribe

Form to unsubscribe from marketing newsletters sent by the site. 

###Route name

`unsubscribe`

###URL pattern

`/account/unsubscribe`
 
###Type

`Form`

###Module

`MyAccount`

##User home

User's account page detailing interactions with the site.

###Route name

`user_home`

###URL pattern

`/account`

###Type

`List`

###Module

`MyAccount`

##Non-HTML response routes

For the following routes, output comes directly from the controller and is not rendered in a template:

* meeting_download
* content_rss
* file_download
* logout