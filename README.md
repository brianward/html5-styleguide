# HTML5 Styleguide

## Document Construction

The base of a full HTML document should be ordered in exactly this way. Optional items could be an analytics script, a jQuery include, or an Apple Touch icon but all other items in this document should be standard. However, these items have become common so they are included here to show best-practice order and placement. The following writing will describe the meaning and the placement of the following elements.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="X-UA-Compatible" content="IE=edge,chrome=1">
  <title>My Page Title</title>
  <meta name="description" content="">
  <meta name="viewport" content="width=device-width">
  <script><!-- Google Analytics JavaScript here --></script>
  <link rel="stylesheet" href="/css/main.css">
  <script src="//ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
  <script>window.jQuery || document.write('<script src="js/vendor/jquery-1.8.1.min.js"><\/script>')</script>
  <script src="/js/main.js"></script>
  <link rel="apple-touch-icon-precomposed" href="/images/apple-touch-icon-precomposed.png">
  <link rel="shortcut icon" href="/images/favicon.ico" type="image/x-icon">
</head>
<body>
  <div id="container">
  </div>
</body>
</html>
```

### Indentation

Standard indentation width varies across different languages and organizations [1][2]. Ruby is most commonly indented at two spaces and C and Java is most commonly indented at four spaces [3]. Four spaces is the default indentation given in most text editors including vim, xcode, and eclipse. No matter what your preferred indentation width, ALWAYS indent nested tags no matter how insignificant the element may seem at the time. This is good practice in planning for the future when the nested area may grow to include other elements. Code readability should always take precedence over code length (although sometimes code length can be a detriment to code readability) [4].

```html
<p>
  <a href="http://example.com/">Justin Bieber is my hero.</a>
</p>
```

One of the only known bugs that can arise from this is when an image is nested within an anchor tag but not on the same line [5]. This problem is well known and can be fixed with the following css which is in any number of standard css reset scripts. The most extensive and well-documented one of these to date is Necolas' normalize.css [6].

```html
<a href="http://example.com/">
  <img src="path_to_image.png">
</a>
```

```css
/* The fix */
a img {
  display: block;
}
```

The only exception to this rule of strict indentation is at the very outer nesting of a document where the `<head>` and `<body>` tags are always listed in the same place relative to the outermost `<html>` tags. Since these tags are always listed in the same place in a valid html document, there cannot be any confusion about where these tags start and end, which is the original problem that proper indentation attempts to solve [7].

```html
<!DOCTYPE html>
<html>
<head>
  <title></title>
</head>
<body>
</body>
</html>
```

Section Footnotes
[1] [Google styleguide]()
[2] [Github styleguide]()
[3] [Microsoft styleguide]()
[4] [Steve Ballmer's comments on code length]()
[5] [CSS bottom image spacing bug]()
[6] [normalize.css]()
[7] [link to article on why we indent]()

### Self-closing tags

Since self-closing tags for single-tag elements are no longer required in the html5 specification [1], do not include them in your markup. Avoiding the trailing slash both saves us unnecessary keystrokes and also reduces the likelihood that a document will contain self-closing tags that are closed with a forward-slash or a space followed by a forward slash since both have become common in XHTML.

```html
<!-- Poor -->
<img src="path-to-image.png" />
<img src="path-to-image.png"/>

<!-- Better -->
<img src="path-to-image.png">
```

Section Footnotes
[1] [HTML5 Standard - W3C](http://www.whatwg.org/specs/web-apps/current-work/multipage/#devices)

### DOCTYPE

Specifying the HTML doctype is critical in order for the browser to render the document correctly [link to article describing doctypes]. Deprecate any older HTML4 or XHTML doctypes within your projects unless there is a specific need for them and remember to test browser compatibility after doing so. By convention the word `DOCTYPE` is always capitalized so it is capitalized here for consistency. All other html tags are always all lowercase by convention.

Section Footnotes
[1] [link to article describing doctypes]()

### meta tags

The four most common meta tags are `charset`, `X-UA-Compatible`, `description`, and `viewport`. The `charset` meta tag should always be the first element. Prefer UTF-8 as encoding for an HTML document. By convention, UTF-8 is lowercase when used in the `charset` meta tag.

The `X-UA-Compatible` meta tag tells Internet Explorer to force rendering on the latest (edge) version of IE even if it encounters quirks in the document that would normally cause Internet Explorer to render the document in compatibility mode (with an older IE browser mode), and also to use Chrome Frame (an open source IE plug-in from Google) if installed. Another way to do this is to configure the web server to send `X-UA-Compatible` as a document header, though that option does create more configuration overhead which may be undesirable.

The `description` meta tag is important since search engines such as Google will use this in search results if no other text content is able to be pulled from the page (e.g., there is no text content). There may also be some SEO value to a well-written meta description. In contrast, the `keywords` meta tag is not used at all by the largest search engines - Google and Bing - and thus should not be included lest developers waste time creating unnecessary content.

The `viewport` meta tag specifies rules that mobile browsers should obey when rendering the page content. The `device-width` should at least be defined. Another common option is to set `initial-scale=1`.

In meta tags which have `name` and `content` as attributes, these should always be ordered as `name` then `content`, since `name` will usually be the shortest of the two texts.

A host of other meta tags are sometimes used but many exist for specific needs (`google-site-verification`, `refresh`, `cache-control`) and others provide no real value at all (`author`, `copyright`, `keywords`, `terms`) and should be avoided.

Any directives included in a `robots` meta tag should instead by included in a `robots.txt` file which exists in the root directory of a site. A `robots.txt` file offers more functionality and the search engine bots will find the directives there.

Section Footnotes
[] [The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets - Joel Spolsky](http://www.joelonsoftware.com/articles/Unicode.html)
[] [Google Chrome Frame](https://developers.google.com/chrome/chrome-frame/)
[] [Google ignores meta keywords](http://googlewebmastercentral.blogspot.com/2009/09/google-does-not-use-keywords-meta-tag.html)
[] [Meta tags that matter - Google Webmasters](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=79812)

### `<title>`

The `<title>` tag is a required element in a valid HTML document [1]. By convention, the `<title>` tag comes as soon as possible within the `<head></head>`. Since the meta `charset` and `X-UA-Compatible` meta tag fundamentally alter the mode in which the browser renders the document, these are the only meta tags that should come before the `<title>`. All other meta tags should appear directly after the `<title>` tag.

Section Footnotes
[1] [The smallest valid html document]()

### Analytics script

An analytics (JavaScript) script placed as high as possible within the document will record the most accurate bounce rate for your website. For example, if the analytics script was placed at the end of the HTML document, just before the `</body>` tag, and a user visits the website without it having been loaded (at least to the point of the analytics script), then that visit will never be recorded. So for the most accurate bounce rate, the analytics script should be placed within the `<head></head>` [1], just before the stylesheet includes, which are typically the first point of material download time. If using a web application framework, a common analytics script should be separated into a partial that can be included in templates as needed.

Section Footnotes
[1] [link to google analytics page where the script include is given]()

### Stylesheets

Stylesheets should all be included within the `<head></head>` [1].

If there is a main stylesheet, whether it is precompiled via Sass or LESS, or uncompiled css, it should be called `main.css`. Do not use @import to include uncompiled css within a `main.css` file since this has been shown to have a strong negative impact on performance [2]. It is standard practice to name css files with words separated by hyphens.

It is not necessary to include the css MIME type since it will be processed as the standard `text/css` if omitted [3]. It should therefore always be omitted for the sake of brevity.

Section Footnotes
[1] [link to description of where stylesheets should be in head]()
[2] [link to yahoo performance blog describing where css @import is bad]()
[3] [HTML5 Standard - W3C](http://www.whatwg.org/specs/web-apps/current-work/multipage/#devices)

### JavaScripts

It may be beneficial for performance reasons to include some, if not all the JavaScripts, just before the end of the `</body>` [1]. However, most of the time, these JavaScripts should be included in the `<head></head>` of the document instead. Always include JavaScripts after stylesheets so that any DOM access within the JavaScripts will be performed on elements that have already been acted upon by the included styles [2].

If using jQuery or other JavaScripts from an outside source, it may be a good idea to provide a local fallback if the vendor-provided version cannot be found [3].

If there is a main JavaScript file, it should be called `main.js` so that its meaning is straigtforward [4]. A JavaScript file with a specific purpose, however, should be named appropriately. It is standard practice to name JavaScript files with words separated by hyphens or periods such as `jquery-carousel.min.js` where the `.min` specifies that it is the minified source. Minification should preferably be done as part of an automated build process.

It is not necessary to include the JavaScript MIME type since it will be recognized as the standard `text/javascript` if omitted. It should therefore always be omitted for the sake of brevity.

Section Footnotes
[1] [link to article describing javascript placement]()
[2] [link to the article describing putting javascript after stylesheets]()
[3] [HTML5 Boilerplate on github](https://github.com/h5bp/html5-boilerplate)
[4] [HTML5 Boilerplate on github (commit log) - change to main.js](https://github.com/h5bp/html5-boilerplate)

### Apple Touch Icon

An Apple Touch icon is optional. If included, favor a precomposed icon so that Android devices can also recognize and use it [1].

Section Footnotes
[1] [Everything you always wanted to know about touch icons - Mathias Bynens](http://mathiasbynens.be/notes/touch-icons)

### Favicon

Always include a favicon as browsers request this file by default, and your web server may log an error if not found. Use the `image/x-icon` MIME type for maximum compatibility when supporting old versions of IE.

A favicon will also be found if there is a valid favicon named `favicon.ico` at the root directory of a site.

Section Footnotes
[1] [Favicon - Wikipedia](http://en.wikipedia.org/wiki/Favicon)

### `<body>`

The `<body>` tag should contain at least one `<div>` tag that wraps all other content on the page. By convention this `<div>` has an id or class of `container` [1]. Twitter Bootstrap defines this container element via a class instead of an id. However, if one needed to empty or change the entire page content within `container`, then an id makes for faster DOM access without the potential hazard of affecting other elements that may also have the class `container`.

Section Footnotes
[1] [Twitter Bootstrap on github](https://github.com/twitter/bootstrap)

## Additional Reference

* [HTML5 Boilerplate on github (commit log)](https://github.com/h5bp/html5-boilerplate/commits/master)
* [Yahoo! performance best practices](http://developer.yahoo.com/performance/)
* [Google performance best practices](https://developers.google.com/speed/docs/best-practices/rules_intro)
* [How Browsers Work: Behind the Scenes of Modern Web Browsers - Tali Garsiel & Paul Irish](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
* [Web performance best practices by Jatinder Mann]()
look for more references in saved links
