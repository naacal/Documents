
# Website Performance Optimization Checklist
---
[toc]

## JavaScript & Optimizations

 Minify, Combine and Gzip (Compress) your code. Inline critical JavaScript and lazy-load the rest.

### Minify JavaScript

Benefits: reducing network latency, enhancing compression, and faster browser loading and execution.

[Closure Compiler](https://developers.google.com/closure/compiler/) ([Online](http://closure-compiler.appspot.com/home)), [PageSpeed Module](https://developers.google.com/speed/pagespeed/module), [JSMin](http://www.crockford.com/javascript/jsmin.html) or the [YUI Compressor](http://yui.github.io/yuicompressor/) ([Online YUI](http://refresh-sf.com/yui/)).

### Combine JavaScript

Combining external scripts into as few files as possible cuts down on round-trip time (RTT) and delays in downloading other resources.

[PageSpeed Module](https://developers.google.com/speed/pagespeed/module), [Minify](http://code.google.com/p/minify/) for PHP, [YUI](http://yui.github.io/yuicompressor/) for Java

 With the advent of [HTTP 2.0](http://en.wikipedia.org/wiki/HTTP_2.0) protocol, this process will have to be reversed for optimization because of request-response multiplexing.

### Compress JavaScript / Gzip

Compressing resources with `gzip` or `deflate` can reduce the number of bytes sent over the network. Most modern browsers support data compression for HTML, CSS, and JavaScript files.

 Don't use gzip for image or other binary files: Image file formats supported by the web, as well as videos, PDFs and other binary formats, are already compressed; using gzip on them won't provide any additional benefit, and can actually make them larger.

### Use CDN Hosted Libraries

Benefits: decreased latency, increased parallelism, better caching, high availability and scalability.

 Popular CDNs: [Google CDN](https://developers.google.com/speed/libraries/devguide), [Microsoft CDN](http://www.asp.net/ajaxlibrary/cdn.ashx), [cdnjs](http://cdnjs.com/), [ossCdn](http://osscdn.com/), [jsDelivr](http://www.jsdelivr.com/), [Bootstrap CDN](http://www.bootstrapcdn.com/).

 Don't forget to implement a fallback for your CDN hosted libraries in case the CDN goes offline. Example:

### Inline Critical JavaScript

If you do have some critical JavaScript code to modify DOM initially (not very common) or if you have a lazy loading code, inline the JavaScript at the bottom of your page to avoid some round-trip time (RTT).

### Defer loading

Deferring loading of JavaScript functions that are not called at startup reduces the initial download size, allowing other resources to be downloaded in parallel, and speeding up execution and rendering time. Here are a few options to defer the loading of JavaScript on your page:

*   Use `defer` attribute on `script` elements to indicate to a browser that the script is meant to be executed after the document has been parsed. This will not stop the browser from downloading the code, so better use the lazy loading techniques given below.

    The `defer` attribute is only for external scripts (should only be used if the `src` attribute is present).

        Be careful when using the `defer` attribute on core libraries like jQuery. It might cause errors if the code relying upon a core library executes before it's loaded.
*   Manually injecting Scripts with callbacks, it makes sure the script is loaded before we start using it.
*   XMLHttpRequest Script Injection
*   Use [LazyLoad](https://github.com/rgrove/lazyload/) library to load external JavaScript and CSS files on demand.
*   [jQuery](http://api.jquery.com/jQuery.getScript/) users can simply use `jQuery.getScript()` method to lazy load and execute scripts on demand.

### Defer parsing

In order to load a page, the browser must parse the contents of all `<script>` tags, which adds additional time to the page load. By minimizing the amount of JavaScript needed to render the page, and deferring parsing of unneeded JavaScript until it needs to be executed, you can reduce the initial load time of your page.

*   The simplest and preferred technique is to simply Defer loading of JavaScript as described in the step above.
*   Use HTML5 `async` attribute on `script` elements to indicate that the browser should, if possible, execute the script asynchronously.

    The `async` attribute is only for external scripts (should only be used if the `src` attribute is present).
*   Load the JavaScript code inside comments so it doesn't get parsed/executed immediately and later use `eval()` method to execute it on demand. Make sure you strip out (or replace) comment blocks in your JavaScript first. The only saving here is that you are not making one extra round-trip to get the JavaScript code and on the contrary if your JavaScript code is too big, you are increasing your initial payload. You should prefer the deferred loading techniques mentioned above over this. [More Info](http://googlecode.blogspot.com/2009/09/gmail-for-mobile-html5-series-reducing.html)

    The biggest pitfall to this technique is that you cannot debug the code executed by `eval()`.

### Leverage browser caching

Setting an expiry date or a maximum age in the HTTP headers for static resources instructs the browser to load previously downloaded resources from local disk rather than over the network. 

HTTP/1.1 provides the following caching response headers:

*   `Expires` and `Cache-Control: max-age`. These specify the “freshness lifetime” of a resource, that is, the time period during which the browser can use the cached resource without checking to see if a new version is available from the web server.
*   `Last-Modified` and `ETag`. These specify some characteristic about the resource that the browser checks to determine if the files are the same. In the Last-Modified header, this is always a date. In the ETag header, this can be any value that uniquely identifies a resource (file versions or content hashes are typical).

It is important to specify one of `Expires` or `Cache-Control` max-age, and one of `Last-Modified` or `ETag`, for all cacheable resources. It is redundant to specify both`Expires` and `Cache-Control: max-age`, or to specify both `Last-Modified` and `ETag`.

**Example**: 

```javascript

# If we're sending far-future expires headers (see below), ETags can
# `FileETag None` is not enough for every server.

<IfModule mod_headers.c>
    Header unset ETag
</IfModule>

FileETag None

# ------------------------------------------------------------------------------
# | Expires headers (for better cache control) |
# ------------------------------------------------------------------------------

# The following expires headers are set pretty far in the future. If you don't
# control versioning with filename-based cache busting, consider lowering the
# cache time for resources like CSS and JS to something like 1 week.

<IfModule mod_expires.c>

    ExpiresActive on
    ExpiresDefault "access plus 1 month"

  # CSS
    ExpiresByType text/css "access plus 1 year"

  # Data interchange
    ExpiresByType application/json "access plus 0 seconds"
    ExpiresByType application/xml "access plus 0 seconds"
    ExpiresByType text/xml "access plus 0 seconds"

  # Favicon (cannot be renamed!)
    ExpiresByType image/x-icon "access plus 1 week"

  # HTML components (HTCs)
    ExpiresByType text/x-component "access plus 1 month"

  # HTML
    ExpiresByType text/html "access plus 0 seconds"

  # JavaScript
    ExpiresByType application/javascript "access plus 1 year"

  # Manifest files
    ExpiresByType application/x-web-app-manifest+json "access plus 0 seconds"
    ExpiresByType text/cache-manifest "access plus 0 seconds"

  # Media
    ExpiresByType audio/ogg "access plus 1 month"
    ExpiresByType image/gif "access plus 1 month"
    ExpiresByType image/jpeg "access plus 1 month"
    ExpiresByType image/png "access plus 1 month"
    ExpiresByType video/mp4 "access plus 1 month"
    ExpiresByType video/ogg "access plus 1 month"
    ExpiresByType video/webm "access plus 1 month"

  # Web feeds
    ExpiresByType application/atom+xml "access plus 1 hour"
    ExpiresByType application/rss+xml "access plus 1 hour"

  # Web fonts
    ExpiresByType application/font-woff "access plus 1 month"
    ExpiresByType application/vnd.ms-fontobject "access plus 1 month"
    ExpiresByType application/x-font-ttf "access plus 1 month"
    ExpiresByType font/opentype "access plus 1 month"
    ExpiresByType image/svg+xml "access plus 1 month"

</IfModule>

```


### Leverage proxy caching

Enabling public caching in the HTTP headers for static resources allows the browser to download resources from a nearby proxy server rather than from a remote origin server.

You use the `Cache-control: public` header to indicate that a resource can be cached by public web proxies in addition to the browser that issued the request. With some exceptions (described below), you should configure your web server to set this header to `public` for cacheable resources.

Recommendations:

*   Don't include a query string in the URL for static resources.
*   Don't enable proxy caching for resources that set cookies.
*   Some public proxies have bugs that do not detect the presence of the `Content-Encoding` response header. This can result in compressed versions being delivered to client browsers that cannot properly decompress the files.

### Place JS at the end of page.

Because JavaScript code can alter the content and layout of a web page, the browser delays rendering any content that follows a script tag until that script has been downloaded, parsed and executed. It's advised to put JavaScript just before the closing `</body>` tag on your page. A sample from [HTML5 Boilerplate](https://github.com/h5bp/html5-boilerplate).

 One benefit to this approach is that you don't have to attach DOM load events because the DOM is already loaded when you reach the end of `</body>` tag.

### Use file/module loaders.

Use a file and module loader like [RequireJS](http://requirejs.org/) to load your script modules asynchronously with more control.

 JavaScript file and module loaders: [RequireJS](http://requirejs.org/), [curl.js](https://github.com/cujojs/curl), [yepnope](http://yepnopejs.com/), [HeadJS](http://headjs.com/), [LABjs](http://labjs.com/), [LazyLoad](https://github.com/rgrove/lazyload/)

### Don't mix markup and behavior.

Keeping the behavior logic outside of HTML will help you optimize the deferred loading of JavaScript code.

## CSS Optimizations

 Minify, Combine and Gzip (Compress) your code. Inline critical CSS in the head and lazy-load rest of the CSS styles.

### Minify CSS

Benefits: reducing network latency, enhancing compression, and faster browser loading and execution.

[PageSpeed Module](https://developers.google.com/speed/pagespeed/module), [CSS Minifier](http://cssminifier.com/), [CSS Compressor](http://www.csscompressor.com/), [YUI Compressor](http://yui.github.io/yuicompressor/) ([Online YUI](http://refresh-sf.com/yui/))

### Compress CSS / Gzip

Compressing resources with `gzip` or `deflate` can reduce the number of bytes sent over the network. Most modern browsers support data compression for HTML, CSS, and JavaScript files.

[Click here](http://lab.abhinayrathore.com/website-performance-optimization-checklist/#gzipModal) for an example on how to use gzip compression on Apache Servers.

 Don't use gzip for image or other binary files: Image file formats supported by the web, as well as videos, PDFs and other binary formats, are already compressed; using gzip on them won't provide any additional benefit, and can actually make them larger.

### Combine CSS

Combining external scripts into as few files as possible cuts down on round-trip time (RTT) and delays in downloading other resources.

[PageSpeed Module](https://developers.google.com/speed/pagespeed/module), [Minify](http://code.google.com/p/minify/) for PHP, [YUI](http://yui.github.io/yuicompressor/) for Java

 Try to keep only one external CSS include on a page. If your CSS code gets bigger, try the Critical CSS approach listed below and lazy-load the lower priority code.

 With the advent of [HTTP 2.0](http://en.wikipedia.org/wiki/HTTP_2.0) protocol, this process will have to be reversed for optimization because of request-response multiplexing.

### Inline Critical CSS

Usually you only need a small amount of CSS code for above-the-fold content or the basic structure of the page. It's always better to strip out the critical/essential CSS code and inline it in the page head and lazy load rest of the CSS. [css-tricks.com](http://css-tricks.com/authoring-critical-fold-css/) has more details on this.

 This is the best approach if you have single-page apps and you don't need to reload the same CSS again on a different page.

 You may not want to inline all your CSS because that will increase the size of your page and you don't get the benefits of Browser and Edge Caching.

### Defer Loading

After inlining all your important CSS, you can lazy-load rest of your styles.

 Use [LazyLoad](https://github.com/rgrove/lazyload/) library to load remaining CSS files on demand.

Or inject the stylesheet using this small script...

### Avoid different stylesheets for _media_ types

Don't use different includes for media types and combine them into one script, example: screen, print or the latest CSS3 media types. Most browsers will download your CSS no matter what media type your specify. [More Information](http://www.phpied.com/css-and-the-critical-path/)

### Avoid CSS @import

CSS @import allows stylesheets to import other stylesheets. When CSS @import is used from an external stylesheet, the browser is unable to download the stylesheets in parallel, which adds additional round-trip times to the overall page load. Instead of @import, use a tag for each stylesheet. This allows the browser to download stylesheets in parallel, which results in faster page load times.

### Put CSS in the document head

Moving inline style blocks and `<link>` elements from the document body to the document head improves rendering performance. It's important to put references to external stylesheets, as well as inline style blocks, in the head of the page.

### Order of styles and scripts

Correctly ordering external stylesheets and external and inline scripts enables better parallelization of downloads and speeds up browser rendering time. Browsers delays rendering any content that follows a script tag until that script has been downloaded, parsed and executed. Stylesheets when placed before script tags will be downloaded in parallel.

### Remove unused CSS

Removing or deferring style rules that are not used by a document avoid downloads unnecessary bytes and allow the browser to start rendering sooner.

[uncss](https://github.com/giakki/uncss), [Unused-CSS](http://unused-css.com/)

### Use CSS preprocessors

Using CSS preprocessors will help you in writing optimized CSS code.

[SASS](http://sass-lang.com/), [LESS](http://lesscss.org/), [Stylus](http://learnboost.github.io/stylus/), [Myth](http://www.myth.io/)

## Image Optimizations

 Reduce Image Size, use CSS Sprites and Lazy-Load when needed.

### Compress

Properly formatting and compressing images can save many bytes of data. You can perform basic optimization with any image editing program, such as [GIMP](http://www.gimp.org/) and[Paint.NET](http://www.getpaint.net/).

 Several tools are available that perform further, lossless compression on JPEG and PNG files, with no effect on image quality:

JPEG: [jpegtran](http://jpegclub.org/) or [jpegoptim](http://freshmeat.net/projects/jpegoptim/) (available on Linux only; run with the `--strip-all` option)

PNG: [OptiPNG](http://optipng.sourceforge.net/), [PNGGauntlet](http://pnggauntlet.com/), [PNGOUT](http://www.advsys.net/ken/util/pngout.htm)

Online Tools: [PNG Crush](http://pngcrush.com/), [JpegMini](http://www.jpegmini.com/), [JPG Optimiser](http://jpgoptimiser.com/)

 Sample [jpegtran](http://jpegclub.org/) command line optimization:

### Combine images using CSS sprites

Combining images into as few files as possible using CSS sprites reduces the number of round-trips and delays in downloading other resources, reduces request overhead, and can reduce the total number of bytes downloaded by a web page.

 Spriting services: [spriteme.org](http://spriteme.org/), [spritepad](http://wearekiss.com/spritepad), [css-sprit.es](http://css-sprit.es/), [spritecow](http://www.spritecow.com/), [spritegen](http://spritegen.website-performance.org/).

### Lazy-Load Images

Lazy loading the images which are not in users viewport will help you reduce initial page load time.

 Use plugin like [jQuery Lazyload](http://www.appelsiini.net/projects/lazyload):

### Image Data URI

For small images, use Data URIs to embed the image directly in CSS code.

 Conversion Tools: [Data URI Convertor](http://websemantics.co.uk/online_tools/image_to_data_uri_convertor/), [Data Url Maker](http://dataurl.net/#dataurlmaker)

Data URI Format:

CSS Example:

HTML Example:

Important Notes:

*   Size of embedded code is somewhat larger than size of resource by itself. GZip compression will help.
*   IE8 has the lowest maximum data URI size of 32768 Bytes.
*   Using PHP you can easily create Data URIs:

### Combine images using Base64 sprites

For loading multiple images in a dynamic environment where it's not feasable to generate CSS Sprites, you can convert the images to Data URI/Base64 encoding and transfer in a batch using text or JSON format. [Live Demo](http://lab.abhinayrathore.com/website-performance-optimization-checklist/base64-spriting/)

 Sample JSON to batch:

### Serve scaled images

To display the same image in various sizes, create thumbnails using image editing software so you can save bandwidth while serving the images.

### Specify dimensions

Specifying a width and height for all images allows for faster rendering by eliminating the need for unnecessary reflows and repaints. To prevent reflows, specify the width and height of all images, either in the HTML `<img>` tag, or in CSS.

### Don't Scale Images in HTML

Don't use a bigger image than you need just because you can set the width and height in HTML.

### Avoid Empty Image src

For every `img` tag with empty `src` attribute, some browsers make another request to your server. [More Info](http://www.nczonline.net/blog/2009/11/30/empty-image-src-can-destroy-your-site/)

*   **Internet Explorer** makes a request to the directory in which the page is located.
*   **Safari and Chrome** make a request to the actual page itself.
*   **Firefox** 3 and earlier versions behave the same as Safari and Chrome, but version 3.5 addressed this issue and no longer sends a request.
*   **Opera** does not do anything when an empty image src is encountered.

### Progressive JPEGs

Jpegs come in two flavors: baseline and progressive. A baseline jpeg is a full-resolution top-to-bottom scan of the image, and a progressive jpeg is a series of scans of increasing quality. [More Info](http://calendar.perfplanet.com/2012/progressive-jpegs-a-new-best-practice/)

 You can use [jpegtran](http://jpegclub.org/) as shown above to compress JPEGs progressively.

### Icon Fonts

Icon fonts are the best additions to modern web design. If you are using a lot of icons on your site, this is the way to go! Icon fonts are scalable and you can easily change their colors like regular fonts on your page. Font Icon payload is very low compared to good old GIFs and PNGs.

 Some popular fonts: [Font-Awesome](http://fortawesome.github.io/Font-Awesome/) (used on this page), [Entypo](http://www.entypo.com/), [Typicons](http://typicons.com/), [Iconic](http://www.somerandomdude.com/work/iconic/), [Modern Pictograms](http://www.fontsquirrel.com/fonts/modern-pictograms), [Meteocons](http://www.alessioatzeni.com/meteocons/), [Meteocons](http://www.alessioatzeni.com/meteocons/), [MFG-Labs](http://mfglabs.github.io/mfglabs-iconset/), [Linecons](http://freebbble.com/2013/02/11/linecons-48-outline-icons/), [Web-Symbols](http://www.fontsquirrel.com/fonts/web-symbols). You can use [Fontello](http://fontello.com/) to piece together your own icon font based on icons from a number of sources.

---

## HTML Optimizations

 Minify HTML, use Gzip (compression) and Lazy-Load when possible.

### Minify HTML

Removing extra line breaks and comments can reduce initial page load time. For attribute values without spaces, you can skip quotes around them to save a few bytes.

### Compress HTML

Compressing resources with `gzip` or `deflate` can reduce the number of bytes sent over the network. Most modern browsers support data compression for HTML, CSS and JavaScript files.

Example on how to use gzip compression on Apache Servers.

```javascript

<IfModule mod_deflate.c>

# Force compression for mangled headers.
# http://developer.yahoo.com/blogs/ydn/posts/2010/12/pushing-beyond-gzipping

<IfModule mod_setenvif.c>
    <IfModule mod_headers.c>
        SetEnvIfNoCase ^(Accept-EncodXng|X-cept-Encoding|X{15}|~{15}|-{15})$ ^((gzip|deflate)\s*,?\s*)+|[X~-]{4,13}$ HAVE_Accept-Encoding
        RequestHeader append Accept-Encoding "gzip,deflate" env=HAVE_Accept-Encoding
    </IfModule>
</IfModule>

# Compress all output labeled with one of the following MIME-types
# (for Apache versions below 2.3.7, you don't need to enable `mod_filter`
# and can remove the `<IfModule mod_filter.c>` and `</IfModule>` lines
# as `AddOutputFilterByType` is still in the core directives).

<IfModule mod_filter.c>
    AddOutputFilterByType DEFLATE application/atom+xml \
                application/javascript \
                application/json \
                application/rss+xml \
                application/vnd.ms-fontobject \
                application/x-font-ttf \
                application/x-web-app-manifest+json \
                application/xhtml+xml \
                application/xml \
                font/opentype \
                image/svg+xml \
                image/x-icon \
                text/css \
                text/html \
                text/plain \
                text/x-component \
                text/xml
</IfModule>

</IfModule>

```

### Reduce the Number of DOM Elements

Write better and more semantically correct markup. More DOM Elements means slower DOM access in JavaScript.

### Defer Loading

Keep you HTML modular and lazy-load it to minimize intial page payload. You can have empty containers like `div`/`iframe` and lazy-load the content via AJAX once the container comes into the viewport.

 Use plugin like [jQuery Waypoints](http://www.appelsiini.net/projects/lazyload) to lazy-load HTML blocks:

 Content required for SEO should not be lazy loaded.

### Optimize Page Repaint

Optimizing the way you manipulate the DOM using JavaScript can reduce page repaint time.

---

## Miscellaneous

### Avoid bad requests

Removing "broken links", or requests that result in 404/410 errors, avoids wasteful requests.

### Minimize HTTP Requests

Concatenate CSS and JavaScript and use image sprites to reduce additional round-trip time (RTT).

### Minimize request size

Keeping cookies and request headers as small as possible ensures that an HTTP request can fit into a single packet.

### Minimize redirects

Minimizing HTTP redirects from one URL to another cuts out additional round-trip time (RTT) and wait time for users.

### Reduce DNS Lookups

For every new server the DNS resolver is contacted by the browser which returns that server's IP address. It typically takes 20-120 milliseconds for DNS to lookup the IP address for a given hostname. The browser can't download anything from this hostname until the DNS lookup is completed.

### Use Domain Sharding

Serving resources from two different hostnames/domains increases parallelization of downloads. Doing this allows more resources to be downloaded in parallel, reducing the overall page load time. Make sure you're using not more than 2-4 domains because of the DNS lookup penalty. [More Info](http://www.stevesouders.com/blog/2009/05/12/sharding-dominant-domains/)

### Reduce Cookie Size

Cookies are sent to the server with every request you make so if you have a lot of cookies or cookies with large size, your total request size will increase. [More Info](http://yuiblog.com/blog/2007/03/01/performance-research-part-3/)

*   Eliminate unnecessary cookies
*   Keep cookie sizes as low as possible to minimize the impact on the user response time
*   Be mindful of setting cookies at the appropriate domain level so other sub-domains are not affected
*   Set an Expires date appropriately. An earlier Expires date or none removes the cookie sooner, improving the user response time

### Cache Stagnant Data

If you have data that does not change often, try caching it on the client to reduce server calls. You can use simple JavaScript object caching (good for single page apps) for dynamic apps (example: a small autocomplete list) or use HTML5 [SessionStorage](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage#sessionStorage) or [LocalStorage](https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage#localStorage) APIs for long term storage.

### Use GET for AJAX Requests

When using XMLHttpRequest (AJAX), POST is implemented in the browsers as a two-step process: sending the headers first, then sending data. So it's best to use GET, which only takes one TCP packet to send (unless you have a lot of cookies). The maximum URL length in IE is 2K, so if you send more than 2K data you might not be able to use GET.

### Serve resources from a consistent URL

It's important to serve a resource from a unique URL, to eliminate duplicate download bytes and additional RTTs.

### Improve server response time

Optimize your back-end code to respond faster. Your server needs to begin sending the first byte of the resource within 200ms of the request being sent.

### Specify a viewport for mobile browsers

If your page has been designed with mobile devices in mind, then you should utilize the viewport meta tag so that mobile devices can render the document at the correct size.

### Serve static content from a cookie-less domain

Serving static resources from a cookieless domain reduces the total size of requests made for a page. In Apache you can set or unset headers before requests are answered and block any front-end cookie setters like Google Analytics. [More Info](http://www.reginaldchan.net/serving-static-content-from-cookieless-subdomain/)

### Specify a character set

Specifying a character set in the HTTP response headers of your HTML documents allows the browser to begin parsing HTML and executing scripts immediately. Apache .htaccess setting for UTF-8:

## Tools to test you website performance

*   Google PageSpeed: [http://developers.google.com/speed/pagespeed/insights/](http://developers.google.com/speed/pagespeed/insights/)
*   Web Page Test: [http://www.webpagetest.org](http://www.webpagetest.org/)
*   Load Impact: [http://loadimpact.com](http://loadimpact.com/)
*   Neustar Web Performance: [http://www.neustar.biz/resources/tools/free-website-performance-test](http://www.neustar.biz/resources/tools/free-website-performance-test)
*   OctaGate SiteTimer: [http://www.octagate.com/service/SiteTimer/](http://www.octagate.com/service/SiteTimer/)
*   Pingdom: [http://tools.pingdom.com/fpt/](http://tools.pingdom.com/fpt/)
*   Which Loads Faster: [http://whichloadsfaster.com/](http://whichloadsfaster.com/)
*   Show Slow: [http://www.showslow.com](http://www.showslow.com/)
*   GTmetrix: [http://gtmetrix.com](http://gtmetrix.com/)

## Resources

*   Google: [https://developers.google.com/speed/docs/insights/rules](https://developers.google.com/speed/docs/insights/rules)
*   Yahoo: [http://developer.yahoo.com/performance/rules.html](http://developer.yahoo.com/performance/rules.html)
*   Web Performance Best Practices: [https://developers.google.com/speed/docs/best-practices/rules_intro](https://developers.google.com/speed/docs/best-practices/rules_intro)
*   PerfPlanet: [http://www.perfplanet.com](http://www.perfplanet.com/)
*   GTmetrix: [http://gtmetrix.com/recommendations.html](http://gtmetrix.com/recommendations.html)
*   [High-Performance Browser Networking](http://chimera.labs.oreilly.com/books/1230000000545/index.html) by [Ilya Grigorik](http://www.igvita.com/)
*   [High Performance JavaScript (Build Faster Web Application Interfaces)](http://www.amazon.com/Performance-JavaScript-Faster-Application-Interfaces/dp/059680279X) by [Nicholas C. Zakas](http://www.nczonline.net/)