---
title: Web Scraping
tags: web, code
---

Part of me does not like the idea of web scraping, but it is a valuable skill if the goal is to ingest web content that doesn't offer an API. If an API is available, it's almost always better to go with the API. Web scraping could fail for a bunch of reasons and requires careful consideration if used in production. The content being scraped is likely not under your control and could change at a moment's notice.

>[!note]
>Web scraping in personal projects or scripts requires less consideration. If it fails, you can quickly change the code and run it again.

## Headless Chromium vs. Requests

One thing that took me far too long to understand is that JavaScript doesn't run when you use a `curl` request for example. It returns the HTML code to load the JavaScript, but it doesn't run anything. As a result, lots of modern websites do not provide the necessary page contents without a browser (except for pages like Hacker News and craigslist.)

This is where "Headless Chromium" comes in. The idea is that you can package Google Chrome (or other browsers) into your application and with code, you can automate what the browser does and read any element of the page. As a result, the JavaScript code *can* run and do everything it needs to finish loading the page.

>[!important]
>One of Cloudflare's goals is to block bots. This can be a challenge for websites that use Cloudflare, but in the next section, there are tools to bypass it.

>[!note]
>Once or twice, I've been able to workaround web scraping countermeasures by simply changing the `User-Agent` header. This is not enough to beat Cloudflare.
## The Best Tools

Here are the best tools I've come across for web scraping. The most complete list can be found in this [GitHub list](https://github.com/stars/ZaneH/lists/scraping-tools).

### Chromium

Before reaching for a Chromium browser, make sure that it's required. Sometimes, the data I'm looking for is available in the plain text response. The easiest way to check is by turning off JavaScript for the site and using the Developer Tools to <kbd>Cmd+F</kbd> and search for the data in the HTML code.

- **Playwright:** Great for E2E tests, but also great for web crawling! Waiting for elements to appear on-screen, scrolling, etc. It's the gold standard for Headless Chromium.
- **Puppeteer:** An alternative to Playwright. This one is my preference because of...
	- **puppeteer-extra:** Provides a [bunch of plugins](https://github.com/berstend/puppeteer-extra/tree/master/packages/puppeteer-extra) for Puppeteer. Some of which bypass reCaptcha/hCaptcha and Cloudflare. Pretty nifty.
- **Kimurai:** Provides a really nice way to crawl pages with Headless Chromium. You can build classes to handle each type of page that is linked.
- **requests-html:** I haven't used this, but it's for python and is very popular.

>[!note]
>Reusing cookies can also be a useful strategy to sign-in to websites without having to login. I recommend using the [Get cookies.txt LOCALLY](https://chrome.google.com/webstore/detail/get-cookiestxt-locally/cclelndahbckbenkjhflpdbgdldlbecc) plugin to export your browser cookies.
### Plain Text

Plain text web scraping is becoming less useful, but it has its place. Websites like craigslist for example are still viable candidates for these non-JavaScript scrapers. They do have the added benefit of being lighter dependencies than a full Chromium browser.

- **beautifulsoup4:** Python library for parsing HTML.
- **requests:** Built-in python library that provides a clean interface for `curl` essentially.
- **fetch:** Built-in for Node.js v18.17+. The equivalent of requests for JavaScript.
- Your favorite language probably has one. They typically come in a few flavors.
