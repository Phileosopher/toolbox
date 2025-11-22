
## web apps tools

[Appscope - Progressive Web Apps Examples](https://appsco.pe/)
Web App Index

[Bubble](https://bubble.io/)
Create Web Apps

[opensilver](https://opensilver.net/)
Create Web Apps

[Anvil](https://anvil.works/)
Create Web Apps

[Sktch.io](https://sktch.io/)
Create Web Apps

[MRSK: Deploy web apps anywhere | Hacker News](https://news.ycombinator.com/item?id=35753106)
[Kamal - Deploy web apps anywhere](https://kamal-deploy.org/)

[componently-com/awesome-building-blocks-for-web-apps: Standalone features to be integrated into web applications](https://github.com/componently-com/awesome-building-blocks-for-web-apps)

## website introduction software tools

[Show HN: Weekend project, Intro.js | Hacker News](https://news.ycombinator.com/item?id=5380056)
[Intro.js | Better introductions for websites and features with a step-by-step guide for your projects.](https://web.archive.org/web/20130804044223/http://usablica.github.io/intro.js/)
[User Onboarding and Product Walkthrough Library | Intro.js](https://introjs.com)

## WebSocket tools

[Show HN: DriftDB - an open source WebSocket backend for real-time apps | Hacker News](https://news.ycombinator.com/item?id=34639728)
[DriftDB | DriftDB](https://driftdb.com/)

# reference and cheatsheets

## browser - Firefox tools

[Firefox/Tweaks - ArchWiki](https://wiki.archlinux.org/title/Firefox/Tweaks#Performance)

## firefox about-config tools

[firefox.md · master · Madis Otenurm / Hidden settings · GitLab](https://gitlab.com/Madis0/hidden-settings/blob/master/firefox.md)

## front-end tools

[GitHub - thedaviddias/Front-End-Checklist: The perfect Front-End Checklist for modern websites and meticulous developers](https://github.com/thedaviddias/Front-End-Checklist)
Front-End Checklist
the perfect Front-End Checklist for modern websites and meticulous developers.
The Front-End Checklist is an exhaustive list of all elements you need to have / to test before launching your website / HTML page to production.

[The Front-End Checklist. An Exhaustive List of all the Elements… | by Brandon Morelli | codeburst](https://codeburst.io/the-front-end-checklist-8b2292fdda44)
another front-end checklist
an exhaustive list of all elements you need to have / to test before launching your site / HTML page to production

[GitHub - thedaviddias/Front-End-Design-Checklist: The Design Checklist for Creative Web Designers and Patient Front-End Developers](https://github.com/thedaviddias/Front-End-Design-Checklist)

[The Front-End Checklist](https://frontendchecklist.io/)
perfect for modern websites and meticulous developers!

## front-end - performance tools

[GitHub - flowforfrank/performance-checklist: comprehensive list of performance optimization techniques to improve your site's performance](https://github.com/flowforfrank/performance-checklist)

[thedaviddias/Front-End-Performance-Checklist: The only Front-End Performance Checklist that runs faster than the others](https://github.com/thedaviddias/Front-End-Performance-Checklist)
Front-End Performance Checklist that runs faster than the others.

[Vitaly Friedman](https://www.smashingmagazine.com/2018/01/front-end-performance-checklist-2018-pdf-pages/#front-end-performance-checklist-2017)
(2018) Front-End Performance Checklist 2018

## HTML+CSS+JS tools

[You Might Not Need JavaScript](https://youmightnotneedjs.com/)

## HTML tools

[Mozilla Developer Network: HTML reference](https://developer.mozilla.org/en/docs/Web/HTML/Element)
(mandatory)
(this site is extremely valuable!)

[HTML5 Please](http://html5please.com/)
Use the new and shiny responsibly.
Look up HTML5, CSS3, etc features, know if they are ready for use, and if so find out how you should use them – with polyfills, fallbacks or as they are.

[HTML Reference - A free guide to all HTML elements and attributes.](https://htmlreference.io/)
free guide to HTML featuring all elements and attributes, and explains them with illustrated and animated examples

[HTML Meta Tags](https://gist.github.com/lancejpollard/1978404)
List of Common HTML Meta Tags Complete

[HTML For Beginners The Easy Way: Start Learning HTML & CSS Today »](https://html.com/)
HTML Guide/Cheat Sheet

[All The Tags](https://allthetags.com/)
All HTML tags briefly explained.

[My Current HTML Boilerplate | Hacker News](https://news.ycombinator.com/item?id=26952557)
[My current HTML boilerplate - Manuel Matuzovic](https://www.matuzo.at/blog/html-boilerplate/)

[GitHub - susam/spcss: A simple, minimal, classless stylesheet for simple HTML pages](https://github.com/susam/spcss)

[HTML Guidelines](https://github.com/xfiveco/html-coding-standards)

## search engine - Google tools

[Daniel Miessler](https://danielmiessler.com/study/google/)
google search tips

## search engine tools

[Search Engine Party](https://searchengine.party/)

## search engine - Yandex tools

[Yandex Search Operator Cheat Sheets](https://yandex.com/support/direct/keywords/symbols-and-operators.html)
[25+ Yandex Search Operators (Yandex Advanced Search)](https://seosly.com/blog/yandex-search-operators/)
[Операторы поиска Google: самый полный список](https://seranking.com/ru/blog/operatory-poiska-google/)
[Yandex Search Operators Quick Reference](http://help.yandex.com/search?id=1113759)

## specific browser - Chrome tools

[chrome site data settings](chrome://settings/siteData) open `chrome://settings/siteData`in Chrome to manage cookies / sites data

[chrome notifications settings](chrome://settings/content/notifications) open `chrome://settings/content/notifications` in Chrome to manage notifications exceptions

## tags and opengraph tools

Ideas of things you can include based on my own site.

```html
  <link rel="icon" type="image/png" href="/favicon.png" />
  <link rel="webmention" href="<https://webmention.io/www.swyx.io/webmention>" />
  <link rel="pingback" href="<https://webmention.io/www.swyx.io/xmlrpc>" />
  <meta name="theme-color" content="#818CF8">
  <title>{frontmatter.title} ∊ swyx.io</title>
  <link rel="canonical" href={canonical} />
  <meta property="og:url" content={swyxioURL} />
  <meta property="og:type" content="article" />
  <meta property="og:title" content={seoTitle} />
  <meta name="Description" content={seoDescription} />
  <meta property="og:description" content={seoDescription} />
  {#if frontmatter.cover_image}
    <meta property="og:image" content={coverImage} />
  {/if}
  <meta
    name="twitter:card"
    content={frontmatter.cover_image ? 'summary_large_image' : 'summary'} />
  <meta name="twitter:domain" content="swyx.io" />
  <meta name="twitter:creator" content="@swyx" />
  <meta name="twitter:title" content={seoTitle} />
  <meta name="twitter:description" content={seoDescription} />
  <meta
    name="twitter:image"
    content={frontmatter.cover_image ? frontmatter.cover_image : '<https://www.swyx.io/swyx-ski.jpeg>'} />
  <meta name="twitter:label1" value="Last updated" content="Last updated" />
  <meta name="twitter:data1" value={metaDate} content={metaDate} />
  <meta name="twitter:label2" content="Read Time" />
  <meta name="twitter:data2" content={readTime} />
```


## bookmarklets

[Awesome Bookmarklets](https://priyank-vaghela.github.io/Awesome-Bookmarklets/)
A curated collection of awesome bookmarkslets!
[Source code](https://github.com/Priyank-Vaghela/Awesome-Bookmarklets)

[Reading Order Bookmarklet — Adrian Roselli](https://adrianroselli.com/2019/04/reading-order-bookmarklet.html)
(2019) Reading Order Bookmarklet
When a keyboard-only user or screen reader user comes to page that uses CSS to create a layout, there is a chance that what is on the screen does not match the flow of the page.

[Create a Trello card from any web page](https://trello.com/en/add-card)
Create a Trello card from any webpage

[n-st/view-on-archive-org.js](https://gist.github.com/n-st/0dd03b2323e7f9acd98e)
Bookmarklet to view current page on the [Internet Archive Wayback Machine](https://archive.org/)

## advanced search operators

[Google Search Guide](https://moz.com/blog/the-ultimate-guide-to-the-google-search-parameters)

[How to Use Search Operators for Advanced Google Search - Moz](https://moz.com/learn/seo/search-operators)

[Mastering Google Search Operators in 67 Easy Steps - Moz](https://moz.com/blog/mastering-google-search-operators-in-67-steps)

[Mastering Google Operators](https://moz.com/blog/mastering-google-search-operators-in-67-steps)
