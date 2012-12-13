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
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
  <script>window.jQuery || document.write('<script src="js/vendor/jquery-1.8.1.min.js"><\/script>')</script>
  <script src="/js/main.js"></script>
  <link rel="apple-touch-icon-precomposed" href="/images/apple-touch-icon-precomposed.png">
  <link rel="shortcut icon" href="/images/favicon.ico" type="image/x-icon">
</head>
<body>
  <div class="container">
  </div>
</body>
</html>
```

### Indentation

Standard indentation width varies across different languages and organizations [1]. Ruby is most commonly indented at two spaces[2] and C and Java is most commonly indented at four spaces [3][4]. Four spaces is the default indentation given in most text editors including vim, xcode, and eclipse. No matter what your preferred indentation width, ALWAYS indent nested tags no matter how insignificant the element may seem at the time. This is good practice in planning for the future when the nested area may grow to include other elements. Code readability should always take precedence over code length (although sometimes code length can be a detriment to code readability).

```html
<p>
  <a href="http://example.com/">Justin Bieber is my hero.</a>
</p>
```

One of the only known bugs that can arise from this is when an image is nested within an anchor tag but not on the same line [5]. This problem is well known and can be fixed with the following css which is standard in any number of standard css reset scripts. The most extensive and well-documented one of these to date is Necolas' normalize.css [6].

```html
<a href="http://example.com/">
  <img src="path_to_image.png">
</a>
```

```css
/* The fix */
a img {
  vertical-align: bottom;
}
```

The only exception to this rule of strict indentation is at the very outer nesting of a document where the `<head>` and `<body>` tags are always listed in the same place relative to the outermost `<html>` tags. Since these tags are always listed in the same place in a valid html document, there cannot be any confusion about where these tags start and end, which is the original problem that proper indentation attempts to solve.

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
* [1] [Google JavaScript Styleguide](http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
* [2] [GitHub Ruby Styleguide](https://github.com/styleguide/ruby)
* [3] [Google C++ Styleguide](http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml)
* [4] [Microsoft Coding Techniques and Programming Practices](http://msdn.microsoft.com/en-us/library/aa260844%28VS.60%29.aspx)
* [5] [CSS bottom image spacing bug](http://askthecssguy.com/articles/inline-images-showing-a-gap-of-space-on-the-bottom-and-one-way-to-get-around-it/)
* [6] [normalize.css](http://necolas.github.com/normalize.css/)

### Self-closing tags

Since self-closing tags for single-tag elements are no longer required in the html5 specification [1], do not include them in your markup. Avoiding the trailing slash both saves us unnecessary keystrokes and also reduces the likelihood that a document will contain self-closing tags that are closed with a forward-slash or a space followed by a forward slash since both have become common in XHTML.

```html
<!-- Leads to inconsistency and more keystrokes -->
<img src="path_to_image.png" />
<br />
<img src="path_to_image.png"/>
<br/>

<!-- Better -->
<img src="path_to_image.png">
<br>
```

Section Footnotes
* [1] [HTML4 Specification - SGML Features with limited support](http://www.w3.org/TR/html4/appendix/notes.html#h-B.3.3)

### DOCTYPE

Specifying the HTML doctype is critical in order for the browser to render the document correctly. Deprecate any older HTML4 or XHTML doctypes within your projects unless there is a specific need for them and remember to test browser compatibility after doing so. By convention the word `DOCTYPE` is nearly always capitalized [1] so it is capitalized here for consistency. All other html tags are always all lowercase by convention.

Section Footnotes
* [1] [Mathias Bynens - The smallest possible valid (X)HTML documents](http://mathiasbynens.be/notes/minimal-html)

### meta tags

The four most common meta tags are `charset`, `X-UA-Compatible`, `description`, and `viewport`. The `charset` meta tag should always be the first element. Prefer UTF-8 as encoding for an HTML document. By convention, UTF-8 is lowercase when used in the `charset` meta tag [1][2].

The `X-UA-Compatible` meta tag tells Internet Explorer to force rendering on the latest (edge) version of IE even if it encounters quirks in the document that would normally cause Internet Explorer to render the document in compatibility mode (with an older IE browser mode), and also to use Chrome Frame [3] (an open source IE plug-in from Google) if installed. Another way to do this is to configure the web server to send `X-UA-Compatible` as a document header, though that option does create more configuration overhead which may be undesirable.

The `description` meta tag is important since search engines such as Google will use this in search results if no other text content is able to be pulled from the page (e.g., there is no text content). There may also be some SEO value to a well-written meta description. In contrast, the `keywords` meta tag is not used at all by the largest search engines - Google[4] and Bing - and thus should not be included lest developers waste time creating unnecessary content for this tag.

The `viewport` meta tag specifies rules that mobile browsers should obey when rendering the page content. The `device-width` should at least be defined. Another common option is to set `initial-scale=1` [5].

In meta tags which have `name` and `content` as attributes, these should always be ordered as `name` then `content`, since `name` will usually be the shortest of the two texts.

A host of other meta tags are sometimes used but many exist for specific needs (`google-site-verification`, `refresh`, `cache-control`) and others provide no real value at all (`author`, `copyright`, `keywords`, `terms`) and should be avoided [6].

Any directives included in a `robots` meta tag should instead by included in a `robots.txt` file which exists in the root directory of a site. A `robots.txt` file offers more functionality and the search engine bots will find the directives there [7].

Section Footnotes
* [1] [The Absolute Minimum Every Software Developer Absolutely, Positively Must Know About Unicode and Character Sets - Joel Spolsky](http://www.joelonsoftware.com/articles/Unicode.html)
* [2] [UTF-8: The Secret of Character Encoding](http://htmlpurifier.org/docs/enduser-utf8.html)
* [3] [Google Chrome Frame](https://developers.google.com/chrome/chrome-frame/)
* [3] [Google ignores meta keywords](http://googlewebmastercentral.blogspot.com/2009/09/google-does-not-use-keywords-meta-tag.html)
* [4] [Andreas Bovens - Understanding Viewport](https://github.com/andreasbovens/understanding-viewport)
* [5] [Meta tags that matter - Google Webmasters](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=79812)
* [6] [Block or remove pages using a robots.txt file](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=156449)

### `<title>`

The `<title>` tag is a required element in a valid HTML document [1]. By convention, the `<title>` tag comes as soon as possible within the `<head></head>`. Since the meta `charset` and `X-UA-Compatible` meta tag fundamentally alter the mode in which the browser renders the document, these are the only meta tags that should come before the `<title>`. All other meta tags should appear directly after the `<title>` tag.

Section Footnotes
* [1] [Mathias Bynens - The smallest possible valid (X)HTML documents](http://mathiasbynens.be/notes/minimal-html)

### Analytics script

An analytics (JavaScript) script placed as high as possible within the document will record the most accurate bounce rate for your website. For example, if the analytics script was placed at the end of the HTML document, just before the `</body>` tag, and a user visits the website without it having been loaded (at least to the point of the analytics script), then that visit will never be recorded. So for the most accurate bounce rate, the analytics script should be placed within the `<head></head>` [1], just before the stylesheet includes, which are typically the first point of material download time. If using a web application framework, a common analytics script should be separated into a partial that can be included in templates as needed.

Section Footnotes
* [1] [link to google analytics page where the script include is given]()

### Stylesheets

Stylesheets should all be included within the `<head></head>` [1].

If there is a main stylesheet, whether it is precompiled via Sass or LESS, or uncompiled css, it should be called `main.css`. Do not use @import to include uncompiled css within a `main.css` file since this has been shown to have a strong negative impact on performance [2]. It is standard practice to name css files with words separated by hyphens.

It is not necessary to include the css MIME type since it will be processed as the standard `text/css` if omitted [3]. It should therefore always be omitted for the sake of brevity.

A proper stylesheet link element should look like this:

```html
<link rel="stylesheet" href="/css/main.css">
```

Section Footnotes
* [1] [link to description of stylesheet placement in head]()
* [2] [Steve Souders - don't use @import](www.stevesouders.com/blog/2009/04/09/dont-use-import/)
* [3] [HTML Living Standard - The Link Element](http://www.whatwg.org/specs/web-apps/current-work/multipage/semantics.html#the-link-element)

### JavaScripts

It may be beneficial for performance reasons to include some, if not all the JavaScripts, just before the end of the `</body>` [1]. However, most of the time, these JavaScripts should be included in the `<head></head>` of the document instead. Always include JavaScripts after stylesheets so that any DOM access within the JavaScripts will be performed on elements that have already been acted upon by the included styles [2].

If using jQuery or other JavaScripts from an outside CDN, it may be a good idea to provide a local fallback if the vendor-provided version cannot be found [3]. Also, when including JavaScripts from an outside source, the specific version number should be used as even large libraries like jQuery occassionally deprecates features [4][5].

If there is a main JavaScript file, it should be called `main.js` so that its meaning is straightforward [6]. A JavaScript file with a specific purpose, however, should be named appropriately. It is standard practice to name JavaScript files with words separated by hyphens or periods such as `jquery-carousel.min.js` where the `.min` specifies that it is the minified source. Minification should preferably be done as part of an automated build process.

It is not necessary to include the JavaScript MIME type since it will be recognized as the standard `text/javascript` if omitted [7]. It should therefore always be omitted for the sake of brevity.

A proper script element should look like this:

```html
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js"></script>
```

Section Footnotes
* [1] [link to article describing javascript placement]()
* [2] [link to the article describing putting javascript after stylesheets]()
* [3] [HTML5 Boilerplate on GitHub](https://github.com/h5bp/html5-boilerplate)
* [4] [Differences Between jQuery .bind() vs .live() vs .delegate() vs .on()](http://www.elijahmanor.com/2012/02/differences-between-jquery-bind-vs-live.html)
* [5] [jQuery commit log](https://github.com/jquery/jquery/commits/master)
* [6] [HTML5 Boilerplate on GitHub (commit log)](https://github.com/h5bp/html5-boilerplate)
* [7] [HTML Living Standard - The Script Element](http://www.whatwg.org/specs/web-apps/current-work/multipage/scripting-1.html#the-script-element)

### Apple Touch Icon

An Apple Touch icon is optional. If included, favor a precomposed icon so that Android devices can also recognize and use it [1]. A precomposed Apple touch icon is an icon that the designer add gloss to, rather than having the gloss be added automatically by the iPhone.

Section Footnotes
* [1] [Everything you always wanted to know about touch icons - Mathias Bynens](http://mathiasbynens.be/notes/touch-icons)

### Favicon

Always include a favicon as browsers request this file by default, and your web server may log an error if not found. Use the `image/x-icon` MIME type for maximum compatibility when supporting old versions of IE.

A favicon will also be found if there is a valid favicon named `favicon.ico` at the root directory of a site [1].

Section Footnotes
* [1] [HTML5 Boilerplate on GitHub](https://github.com/h5bp/html5-boilerplate)

### `<body>`

The `<body>` tag should contain at least one `<div>` tag that wraps all other content on the page. By convention this `<div>` has an id or class of `container` [1]. Twitter Bootstrap defines this container element via a class instead of an id. However, if one needed to empty or change the entire page content within `container`, then an id makes for faster DOM access without the potential hazard of affecting other elements that may also have a class of `container`.

Section Footnotes
* [1] [Twitter Bootstrap on GitHub](https://github.com/twitter/bootstrap)

### Images

Images should almost always be of type png. PNG gives the best middleground between quality and compression for images with graphics like lines, shapes, and text. There are many well documented ways of achieving transparency in IE6 I find the easiest is to compress your pngs in Adobe Fireworks at 8bit compression with alpha transparency [1]. This is the only program, as far as I know, that can produce pngs with transparency that show correctly in IE6. However, IE6 must die [2] so consider forgetting supporting this horrible browser entirely. All other pngs should be compressed at 16bit or 32bit compression to avoid banding on gradients or jagged edges on corners.

JPEGs offer a good quality at a lower bytesize than pngs if the images have widely varied bits such as in photos. Flickr uses jpegs for this reason [3].

Consider building icon libraries as fonts [4][5] so that icons can scale with different resolutions such on mobile devices.

Section Footnotes
* [1] [IE6 Transparent PNG Fix](http://www.3232design.com/blog.cfm?id=94)
* [2] [IE6 Countdown](http://www.ie6countdown.com/)
* [3] [Flickr](http://flickr.com/)
* [4] [GitHub Styleguide](https://github.com/styleguide/css/7.0)
* [5] [Fontawesome icon library](http://fortawesome.github.com/Font-Awesome/)

### Anchors



* [1] [To slash or not to slash](http://googlewebmastercentral.blogspot.com/2010/04/to-slash-or-not-to-slash.html)

### HTML5 Elements



Section Footnotes
* [1] [HTML5 Sectioning Flowchart](http://html5doctor.com/downloads/h5d-sectioning-flowchart.png)

## Additional Reference

#### Best Practices
* [HTML5 Boilerplate on GitHub (commit log)](https://github.com/h5bp/html5-boilerplate/commits/master)
* [Twitter Bootstrap on GitHub](https://github.com/twitter/bootstrap)
* [HTML Living Standard](http://www.whatwg.org/specs/web-apps/current-work/multipage/)
* [HTML5 Rocks](http://html5rocks.com/)
* [Google Webmaster Tools Support](http://support.google.com/webmasters/)
* [HTML5 Snippets](http://html5snippets.com/)
* [Broken Promises of HTML5](http://www.youtube.com/watch?v=r7xnKSPWTjo)
* [HTML5 Security Cheatsheet](http://html5sec.org/)
* [Move the Web Forward](http://movethewebforward.org/)
* [Mozilla HTML5 and Friends](https://developer.mozilla.org/en-US/learn/html5)

#### Performance
* [Yahoo! web performance best practices](http://developer.yahoo.com/performance/)
* [Google web performance best practices](https://developerlopers.google.com/speed/docs/best-practices/rules_intro)
* [Steve Souders' Blog](http://www.stevesouders.com/)
* [How Browsers Work: Behind the Scenes of Modern Web Browsers - Tali Garsiel & Paul Irish](http://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)
* [Web performance best practices by Jatinder Mann](http://channel9.msdn.com/Events/Build/2012/3-132)

#### Tools
* [When Can I Use?](http://caniuse.com/)
* [HTML5 Please](http://html5please.com/)
* [Web Directions](http://webdirections.org/tools)
* [HTML Email Boilerplate](http://htmlemailboilerplate.com/)
