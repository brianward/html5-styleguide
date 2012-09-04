#HTML5 stylguide

##Document Construction

There is a reason for the order and placement of all elements in a well-formed HTML document. A full HTML document should look like this, depending on which items are needed. Optional items could typically be the Google (or other) analytics script, the jQuery include, and the Apple Touch icon. However, these items have become standard in most HTML documents so they are included here.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="X-UA-Compatible" content="IE=edge,chome=1">
    <title>My Page Title</title>
    <meta name="description" content="">
    <meta name="viewport" content="width=device-width">
    <script><!-- Google Analytics script here --></script>
    <link rel="stylesheet" href="/stylesheets/main.css">
    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
    <script>window.jQuery || document.write('<script src="js/vendor/jquery-1.8.1.min.js"><\/script>')</script>
    <script src="/javascripts/main.js">
    <link rel="apple-touch-icon-precomposed" href="/images/apple-touch-icon-precomposed.png">
    <link rel="shortcut icon" href="/images/favicon.ico" type="image/x-icon">
</head>
<body>
    <div id="container">
    </div>
</body>
</html>
```

###Indentation

Standard indentation varies across different languages and organizations. Indentation is at two spaces by convention in the Ruby language, while most Java and C shops indent at four spaces. Your HTML indenation should follow the standard indentation within a project. If indenting at four spaces, indent the `<head>` and `<body>` tags at the same level as the `<html>` tag. This is the only time when it is acceptable to indent a nested tag at the same level as its parent tag. If indenting at two spaces, indent the `<body>` and `<head>` tags normally at the second level relative to the `<body>` tag as such:

```html
<html>
  <head>
    <title></title>
  </head>
  <body>
  </body>
</html>
```

###DOCTYPE

Specifying the HTML doctype is critical to correct browser rendering of the document. The HTML5 doctype is simply "html" which is easier to remember than older HTML4 and XHTML doctypes. Deprecate any HTML4 or XHTML doctypes within your projects unless there is a specific need for them and remember to test browser compatibility when doing so. By convention the word `DOCTYPE` is always capitalized so it is capitalized here for consistency. All other html tags are always lowercase.

###meta tags

The four critical meta tags are `charset`, `X-UA-Compatible`, `description`, and `viewport`. The `charset` meta tag should always be the first element. Prefer UTF-8 as encoding for an HTML document. By convention, UTF-8 is lowercase when used in the `charset` meta tag.

The `X-UA-Compatible` meta tag tells Internet Explorer to force rendering on the latest (edge) version of IE even if it encounters quirks in your document that would cause Internet Explorer to normally render the document in compatibility mode (at another browser mode), and also to use Chrome Frame (an open source IE plug-in from Google) if installed. Another way to do this is to configure your web server to send `X-UA-Compatible` as a document header, though that option does create more configuration overhead which may be undesirable.

The `description` meta tag is important since search engines such as Google will use this in search results if no other text content is able to be pulled from the page (e.g., there is no text content). There may also be some SEO value to a well-formed meta description. In contrast, the `keywords` meta tag is not used at all by the largest search engines - Google and Bing - and thus should not be included lest developers waste time creating useless content.

The `viewport` meta tag specifies how mobile browsers should render the page content. The device-width should at least be defined. Another common option is to set initial-scale=1.

In meta tags which take `name` and `content` as arguments, these should always be ordered as `name` then `content`, since `name` will usually be the shortest of the two texts.

A host of other meta tag conventions exist but many exist for specific needs (`google-site-verification`, `refresh`, `cache-control`) and others provide no added value (`author`, `copyright`, `keywords`, `terms`).

Any directives included in a `robots` meta tag should instead by included in a `robots.txt` file which exists in the root directory of a site.

###<title>

The `<title>` tag is a required element in a valid HTML document. By convention, the `<title>` tag comes as soon as possible within the `<head></head>`. Since the meta `charset` and `X-UA-Compatible` meta tag fundamentally change the way the browser renders the document, these are the only meta tags that should come before the `<title>`, by convention. All other meta tags should appear directly after the `<title>` tag.

###Analytics script

An analytics (JavaScript) script placed as high as possible within the document will record the most accurate bounce rate for your website. For example, if the analytics script was placed at the end of the HTML document, just before the `</body>` tag, and a user visits the website without it having been fully-loaded, then that visit will never be recorded. So for the most accurate bounce rate, the analytics script should be placed within the `<head></head>`, just before the stylesheet includes. If using a web application framework such as Rails or Django, a common analytics script should be separated out into a partial that can be included in multiple layouts.

###Stylesheets

Stylesheets should all be included within the `<head></head>`. If there is a main stylesheet, whether it is precompiled via SASS or LESS, or uncompiled css, it should be called `main.css`. Do not use @import to include uncompiled css within a `main.css` file since this has been shown to have a strong negative impact on performance. It is not necessary to include the css MIME type since it will be recognized as the standard `text/css` if omitted. It should therefore always be omitted for brevity, unless specifically needed.

###JavaScripts

It may be beneficial for performance reasons to include some, if not all your JavaScripts, just before the end of the `</body>`. However, if you are unsure, these JavaScripts should be included in the `<head></head>` of the document instead. Always include JavaScripts after stylesheets so that any DOM access within the JavaScripts will be performed on elements that have already been acted upon by the included styles. If using jQuery or other JavaScripts from the Google Ajax libraries, provide a local fallback if the vendor-provided version cannot be found. An example of this is shown at the beginning of this file. If there is a main JavaScript file, it should be called `main.js` so that its meaning is straigtforward. It is not necessary to include the JavaScript MIME type since it will be recognized as the standard `text/javascript` if omitted. It should therefore always be omitted for brevity, unless specifically needed.

###Apple Touch Icon

An Apple Touch icon is optional. If included, favor a precomposed icon so that Android can also recognize and use it.

###Favicon

Always include a favicon as browsers request this file by default, and your web server may throw an error if not found. Use the `image/x-icon` MIME type for maximum compatibility with old versions of IE.

###<body>

The `<body>` tag should contain at least one `<div>` tag that wraps all other content on the page. By convention this `<div>` has an id of `container`. Twitter Bootstrap defines this container element via a class instead of an id. If you needed to empty or change the entire page content within `container`, then an id makes for faster DOM access without the potential of affecting other elements that may have a class of `container`.

##Reference

[HTML5 Boilerplate on github](https://github.com/h5bp/html5-boilerplate)
[HTML5 Boilerplate on github (commit log)](https://github.com/h5bp/html5-boilerplate/commits/master)
[The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets - Joel Spolsky](http://www.joelonsoftware.com/articles/Unicode.html)
[Google Chrome Frame](https://developers.google.com/chrome/chrome-frame/)
[Google ignores meta keywords](http://googlewebmastercentral.blogspot.com/2009/09/google-does-not-use-keywords-meta-tag.html)
[Meta tags that matter - Google Webmasters](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=79812)
[Yahoo! performance best practices](http://developer.yahoo.com/performance/)
[Google performance best practices](https://developers.google.com/speed/docs/best-practices/rules_intro)
[HTML5 Standard - W3C](http://www.whatwg.org/specs/web-apps/current-work/multipage/#devices)
[Everything you always wanted to know about touch icons - Mathias Bynens](http://mathiasbynens.be/notes/touch-icons)
[Favicon - Wikipedia](http://en.wikipedia.org/wiki/Favicon)
[How Browsers Work: Behind the Scenes of Modern Web Browsers - Tali Garsiel & Paul Irish](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
[Twitter Bootstrap on github](https://github.com/twitter/bootstrap)