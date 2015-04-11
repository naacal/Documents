
## Websites optimization technical breakdown: 

----------


Google factors in many technical loading elements while rating a page for its popular search engine. Among these concerns are:

- Time to first request with server
- Page load speed
- Image optimization
- HTTP Requests
- CSS, Javascript files compression and delivery

----------

### Page load speed

#### 1 File delivery 

- All **css** files should be combined into one file 
- All **js** files should be concatenated into one file

#### 2 File placement

2.1 The combined **css** file should be place in the head of the document (template), before the closing tag

```
Example:

    <link rel="stylesheet" href="link/to/stylesheet.min.css">
    ....
</head>
```
----------

2.2 The combined **js** file should be place in the head of the document (template), before the closing tag

```
Example:

    <script type="text/javascript" src="src/functions.min.js"></script>
    ....
</body>
```

> This is done to remove the render blocking scripts from the **DOM** (Document Object Model)

#### 3 Defer parsing of scripts

How to defer loading of javascript?

The below code is what Google recommends. This code should be placed in your HTML just before the </body> tag (near the bottom of your HTML file). I highlighted the name of the external JS file.

``` javascript
    <script type="text/javascript">
        function downloadJSAtOnload() {
        var element = document.createElement("script");
            element.src = "defer.js";
            document.body.appendChild(element);
        }
        if (window.addEventListener)
        window.addEventListener("load", downloadJSAtOnload, false);
        else if (window.attachEvent)
        window.attachEvent("onload", downloadJSAtOnload);
        else window.onload = downloadJSAtOnload;
    </script>

```

#### 4 Externalize all JS and CSS files:

It is a good practice to place your website’s JS and CSS in external files. When the page loads the browser caches these files externally and reduces the page load time. Moreover, having the **JS** and **CSS** files externally allows for easy site maintenance.

----------

### Optimizing images

For  ***.jpg** files use this tool to optimize the images
    
    https://tinyjpg.com/


For  ***.png** files use this tool to optimize the images

    https://tinypng.com/

----------

### Gzip compression

As it sounds pretty technical, it should be noted that enabling gzip compression is the most technically difficult item on this list. You may want to consult with your host or web agency before modifying this if you are concerned.

What gzip compression does is compress files on the server level to reduce the size of files being loaded on the site. Enabling gzip compression is done through the .**htaccess** file found within your website files.

You want to add this code to your **.htaccess** file:
```
<ifModule mod_gzip.c>
    mod_gzip_on Yes
    mod_gzip_dechunk Yes
    mod_gzip_item_include file .(html?|txt|css|js|php|pl)$
    mod_gzip_item_include handler ^cgi-script$
    mod_gzip_item_include mime ^text/.*
    mod_gzip_item_include mime ^application/x-javascript.*
    mod_gzip_item_exclude mime ^image/.*
    mod_gzip_item_exclude rspheader ^Content-Encoding:.*gzip.*
</ifModule>
```

----------

### Avoid Redirects

Avoiding redirects increases serving speed. Some redirects are unavoidable and need to be in place but you must remember that this requires an additional HTTP which increases the page load time. Check for broken links and fix them immediately.

```
    http://www.domain.com
    http://domain.com/
    http://www.domain.com/
    http://domain.com
```

----------

### Use consistent URL convention

What if your site serves duplicate content on these two URLs:

```
    http://domain.com/directory/
    http://domain.com/directory
```

meaning that both URLs return **200** (neither has a **redirect** or contains **rel=”canonical”**), and you want to change the situation?

Choose one URL as the preferred version. If your site has a directory structure, it’s more conventional to use a trailing slash with your directory URLs (e.g., **example.com/directory/** rather than **example.com/directory**), but you’re free to choose whichever you like.

Be consistent with the preferred version. Use it in your internal links. If you have a Sitemap, include the preferred version (and don’t include the duplicate URL).

> Sitemaps should not include the canonical version of the page

Use a **301** redirect from the duplicate to the preferred version. If that’s not possible, **rel=”canonical”** is a strong option. **rel=”canonical”** works similarly to a **301** for Google’s indexing purposes, and other major search engines as well.

Test your **301** configuration through Fetch as **Googlebot** in Webmaster Tools. 

```
http://domain.com/foo/
http://domain.com/foo
```
    
Make sure your URL's are behaving as expected. The preferred version should return **200**. The duplicate URL should be redirected using **301** to the preferred URL.

Check for Crawl errors in Webmaster Tools, and, if possible, your web server logs to ensure that the **301**'s are implemented.

----------

### Reduce DNS Lookups

DNS (Domain Name System) Lookup occurs when a URL (hostname) is typed in a browser and a DNS resolver returns that server’s IP address. The time needed for this process is around 20 – 120 milliseconds, however, multiple host names can be used for various elements on a website, which includes the URL, images, script files, style sheets and flash elements. With multiple unique hostnames the DNS lookup also increases thus increasing the page load time. 

Reducing the number of unique hostnames will reduce the number of parallel downloads, which may increase the page loading time.  It is thus ideal to use one host when you have less than six resources. You can also use URL paths instead of hostnames. 

This means that if you have a blog page that is hosted on **blog.yoursite.com**, you can instead host it on **www.yoursite.com/blog**.

----------

### Use Expires/Cache-Control Header

You can use Expires headers for static components of the site and Cache-Control headers for dynamic ones. Using these headers makes the various components of a site, including images, stylesheets, scripts and flash, cacheable. This in turn minimizes HTTP requests and thus improves the page load time. With the use of Expires headers you can actually control the length of time that components of a web page can be cached, as shown in the example below:

```
Expires: Wed, 20 Apr 2015 20:00:00 GMT
```
If your server is Apache you can set the time for cached content by using the **ExpiresDefault** directive. This sets the expiration date as a certain number of years from the current date:
```
ExpiresDefault “access plus 15 years”
```
----------

### Reduce Cookie Size:

The data stored in cookies is exchanged between servers and browsers. Hence, by reducing the size of the cookies you reduce the size of the data that is transferred and increase the page load time. Eliminate unnecessary cookies and set your Expires date to a sooner time period, or provide no Expires date at all to reduce the size of the cookies.

----------

### When to use Canonical

- Duplicate content but you want to keep both pages live
- Dynamic pages with multiple URLs of a single page (from sorting features, tracking options, etc.)
- Site-wide considerations like the examples below can be easier with canonical's.

        http://domain/page/index.html 
        http://domain/page/ for the same page 

- Cross-domain considerations where both sites are similar, but need to remain live
