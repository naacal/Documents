## Rules:

### Check if SEM's are not blocked.

> * Check robots.txt file using [this tool](http://seositecheckup.com/tool/robots)
> * Folders with logic (server side code) should be blocked for crawling bots

**Example:** 
```
User-Agent: *

Disallow: /OAuth/
Disallow: /downloads/
Disallow: /heatmap/
    
Sitemap: https://www.taxback.com/sitemap.xml
```

> * `Ask the developer to protect those folders from direct access and crawling if they are not protected already!`

###  Check the sitemap.xml

> * Check the sitemap using [this tool](http://seositecheckup.com/tool/sitemap)
> * Check if page change frequency is correct
> * Check if page priority is correct
> * Check for pages that should not be listed in `sitemap.xml`

---
> * `All questions related to sitemaps should be addressed to the SEO team`

**Example sitemap structure for one entry:**
```
<url>
    <loc>http://taxback.com/es/corporate/global-mobility/</loc>
    <lastmod>2015-01-23</lastmod>
    <changefreq>daily</changefreq>
    <priority>0.8</priority>
</url>

```

### Check if the site has Favicon

> * The favicon should be provided by the designer
> * The file format should be **.ico**
> * The correct favicon html tag format is:

```
<link rel="shortcut icon" href="http://www.domain.com/favicon.ico" type="image/x-icon">
```

Use [this tool](http://favicon.cc) if the favicon is provided in **png** or **gif** format to convert it to **ico**



### Check Metadata

Use the tools listed below to check for metadata and rich snippets

> * http://www.google.com/webmasters/tools/richsnippets 
> * https://www.google.com/webmasters/markup-helper/


### Check for Meta tags

Make sure all meta tags are present in the header of the site for all pages

```

<!-- Basic rules -->
<meta charset="utf-8">
<meta name="robots" content="index, follow">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
<meta name="robots" content="index, follow">
<meta name="google-site-verification" content="add your code here">

<!-- for Google -->
<meta name="description" content="" />
<meta name="keywords" content="" />

<meta name="author" content="" />
<meta name="copyright" content="" />
<meta name="application-name" content="" />

<!-- for Facebook -->          
<meta property="og:title" content="" />
<meta property="og:type" content="" />
<meta property="og:image" content="" />
<meta property="og:url" content="" />
<meta property="og:description" content="" />

<!-- for Twitter -->          
<meta name="twitter:card" content="summary" />
<meta name="twitter:title" content="" />
<meta name="twitter:description" content="" />
<meta name="twitter:image" content="" />

<!-- for Microsoft -->          
<meta name="msapplication-TileColor" content="#ffffff">
<meta name="msapplication-square70x70logo" content="https://www.domain.com/tiny.png">
<meta name="msapplication-square150x150logo" content="https://www.domain.com/square.png">
<meta name="msapplication-wide310x150logo" content="https://www.domain.com/wide.png">
<meta name="msapplication-square310x310logo" content="https://www.domain.com/large.png">

<!-- for Apple -->
<link rel="apple-touch-icon" href="https://www.domain.com/touch-icon-iphone.png">
<link rel="apple-touch-icon" sizes="76x76" href="https://www.domain.com/touch-icon-ipad.png">
<link rel="apple-touch-icon" sizes="120x120" href="https://www.domain.com/touch-icon-iphone-retina.png">
<link rel="apple-touch-icon" sizes="152x152" href="https://www.domain.com/touch-icon-ipad-retina.png">
<meta name="apple-itunes-app" content="app-id=add yours">

```

### Print stylesheet 

> * Make sure that Print stylesheet exists and its tested for the pages meant to be printed by the user

### Footer related information includes

> * Copyright information
> * Link to Terms & Conditions
> * Link to Privacy Polices if applicable for this website

### JavaScript is error free

> * Press F12 and open the console tab to see if there are any erros

***

## Content / Copy

Writers and editors have strong attention to detail when it comes to the written content on your site. And this attention to detail can also be used for other tasks as well. Here’s what they can do pre-launch:

### Spelling, Grammar, Punctuation

> * Check for proper spelling, typos, and grammar sitewide.
> *  No Test Content should be present on the site. (Lorem ipsum dummy text)

### Web Forms / quote and contact forms

Fill out the forms on the site and go through the following questions:

> *   Check if the flow is not broken
> *   Check if the flow is correct (sequence of steps / wizard forms)
> *   Are the instructions accurate? / Tool-tips and Placeholders and meaningful
> *   Does the completed form get sent to the right people or person?

* * *

## User Interface

Web designers know what the original design intent is, and they have an eye for the visual details. They can usually spot when things don't look quite right pretty quickly.

### Call to actions and process

> * The descriptions and short and clear
> * All call to actions (CTA's) are clear and prominent
> * It is always clear what is happening on the site (easy to navigate)
> * Feedback is clear and meaningful
> * Standard colours are used for links and visited links
> * Error messages describe what action is necessary
> * Error and feedback messages provide assistance for the user
> * All functionality is clearly labelled


### Typography

> * Check if fonts are too small and not readable. Min font size should be 12px 
> * Check to see that the formatting is consistent
>  * Leading (line-height)
>  * Kerning
>  * Decoration
> * Check for header hierarchy is correct for all headings.  


### Media assets

> * Make sure all display text renders on the image when you hover over it (the alt attribute). 
> * Make sure the images display correctly. (Proportion, scaling, text covering important parts of the image )
> * Are they larger than 120 kilobytes? If so, find out of there is a good reason for that. 
> * Make sure ***.png** is not used if the image have no transparency.

* * *

## Front-end development

### Source code Validation

W3C-valid code is the one thing you can do prior to launch to have some confidence around a search engine spider being able to crawl your site. 

> * Check against [W3C validation tool](http://validator.w3.org/)

### Performance 

> * Concatenate all **CSS** files into one
> * Concatenate all **JS** files into one
> * Use image sprites for all non background assets


### Error (404) pages

> * When a 404 (“page not found”) error occurs, make sure you have a custom page to help your visitor find something else of use, even if it wasn't what they were looking for. 
> * Do you have an HTML sitemap there? 
> * Does the 404 page include a site search or HTML sitemap?

### External assets

#### Web Fonts 

> * Use hosted fonts if possible.  
> `Ask if you don't know how to implement hosted fonts`
> * Do not use Google font API dynamic font loading. 
> * The goal is to reduce HTTP Request 
> `This will reduce the load time of the site | DOM Ready response time`

#### External JavaScript libraries

> * Try to use only local JS libraries if possible to reduce HTTP requests

### Site speed

Check the size of your page sizes and their load time. Here’s how:

> *   Open Google Chrome
> *   Navigate to your site in Chrome
> *   Press F12
> *   View “network” tab

![enter image description here](https://developer.chrome.com/devtools/images/network-panel.png)

Type or paste this in Google chrome console tab

```
document.getElementsByTagName("*").length
```

> * Check how many Node elements do you have on all main pages.
> * The recommended number of node elements is less than 700
 
###  Cross Browser testing

Common Issues associated with Cross Browser testing

> * Inconsistency in Page Layout
> * Font size and font style: some browsers overwrite these properties.
> * Controls alignment: bullets, radio buttons and checkboxes might not be correctly aligned.
> * Text alignment: some dropdown items will look good in Chrome and FF but not in IE
> * Plugins developed by external sites: some jQuery plugins might not work correctly, like print functionalities in IE8 or carousel rotation when playing videos.

### Responsive versions

> * Desktop
>  * 1920x1080
>  * 1366x768 
>  * 1024x768
>  * Min width 960px
> * Tablets
>  * 1024x768
>  * 1280x800
>  * Min width 960px
> * Mobile devices
>  * From 768px to 320px


---
> Use [Screensizes](http://screensiz.es/) to see popular devices pixel dimensions 

* * *


## Search Engine Optimization

### Check Metadata

> * Make sure each title does not exceed more than 75 characters
> * Make sure each description contains the keywords present in title and does not exceed 180 characters.
> * For dynamic pages does the code generates an unique Title, Description and Keywords tag?
> * For static pages does the code generates an unique Title, Description and Keywords tag?


### Check page’s content

> * Make sure important content is contained outside JavaScript, flash or iframe
> * Make sure text is not rendered as image
> * Ensure the keywords are used in the H1 and H2 tags
> * Ensure there is only one H1 tag which contains the same content/keywords as page title. 
> * The heading tags H2 and H3 are used to create hierarchical structure for the main content of the pages.

### Broken Links

> * Use http://seositecheckup.com/ tool to check for broken links

### Check for Duplicate Content

> * Do a search to see if your content exists elsewhere on the Web. 
> You may want to check out http://copyscape.com and use it regularly.

### Dynamic pages 

> * Does the code generates unique Title, Description and Keywords tags

### Static pages 

> * Have unique Title, Meta Description and Meta Keywords tags

### 301 Redirects

Sometimes content gets moved to fit the new navigation structure of a site. 

> * Check If you have an existing site and you are changing the URL structure with your new site.


### Title Tags/Meta Data

This may sound like old news to some, but this easy-to-fix mistake happens every day. 

> * Make sure every page has a title tag and make sure they are unique
> * Also make sure each page has unique meta description

### Tools

> * Make sure all Webmaster Tools are set up and ready to go.  
>  * Google Analytics  
>  * Google Webmaster Tools  
>  * Bing Webmaster Tools


### Social Media

Make sure all social media links open another tab and have the correct url

> * Check social media buttons and icons
> * Check if they function properly  
>  * Like buttons  
>  * Share buttons


### SERP Display

> * Are the search engines displaying your pages correctly in the search engine results pages?  
> * Did you write proper meta descriptions, but they aren't being used?  
> * Are the images you placed on your Places page being displayed in the SERP?

### 20. PPC Setup

> * Make sure if you are running any PPC campaigns that it’s set up and ready to go with the site launch. 
> * To avoid a lapse in service, if you have a Google PPC rep, you can set and pause all your campaigns

* * *


## Usability / User Experience

### Interface and usability

> * Are all call to actions clear and descriptive
> * Is the content above the fold allowing the user to scan in in less than 5 sec
> * Does the site provide help guides for the user where needed
> * The purpose of the site and the critical actions are clear within 5 seconds
> * Does the websites provide responsive version as well as desktop version if requested
> * The site logo is easy to find and links to the home page
> * It's easy to find the About Us, Contact Us and Home links
> * The internal search function is easy to find and use (if applicable)
> * There is a custom 404 page for broken links
> * Forms and signups only require essential information and provide helpful feedback

### Text Clarity

> *  The title tags, meta descriptions, headers and URLs are clear and descriptive
> *  The text on the page is easy to read (Text to image ratio is good)
> *  The pages are easy to scan for important information and are free of errors

### Design Consistency

> * The navigation is clear, well organized and does not overwhelm
> * The important site content is viewable on a small monitor without scrolling
> * Links are obvious and take you to relevant pages
> * Animation, video, pop-ups and ads are kept to a bare minimum throughout the site

***

## Network Administration

These folks manage your web servers, the software that runs on them, and all the traffic components that keep your web traffic coming in. Their technical expertise on some of these tasks is like gold.

### Monitoring

> * A site monitor checks pages regularly to make sure it is available for visitors. 
> * Basic monitors check if the page is working.
> * Important pages within the site should have enhanced monitors that test if a completed form behaves the way it should. 
> * Enhanced monitors are more expensive to setup and keep running so the page in question needs to justify the additional expense.

### Backup System

> * Make sure the backup system is configured properly, and the recovery process has been tested so you know it works.

### Protected Pages

> * Make several attempts to get to those URLs without proper credentials to make sure the security is working as expected.

### Secure Certificate (if Required)

To do this, go to the encrypted section of your site. When the lock appears in the address bar, right click on it and read the message your visitors will read. It should have your name on it and state that it’s valid. If the lock doesn't appear or the name isn't right, let your provider know.
