---
description: Second section in Jr Penetration Testing learning path.
---

# Content Discovery

### Introduction

Content on a website can be many things: a file, video, picture, backup, or feature. There are three primary ways to discover content on a website:

* Manual
* Automated
* OSINT

### Manual Discovery

There are multiple places on a website to check for more content.

The "robots.txt" file is a document which tells search engines what they can and cannot show in their results or ban specific search engines from crawling altogether. This file gives us a great list of locations on the website that the owners do not want us to discover.

The favicon is a small icon which is displayed in the browser's address bar or tab used for branding. Sometimes, when a framework is used to build a website, a favicon is leftover, which can give us a clue on which framework is in use.

The "sitemap.xml" file gives a list of all the files the owner wishes to be listed on a search engine. This can contain areas of the website that are hard to navigate to, or even list old webpages.

HTTP headers are seen when we make requests to a web server, headers can contain useful information like the web server software or potentially the programming/scripting language being used. We can use `curl http://[IP_ADDR] -v` to see this.

If you have located the framework a site is using, you can then locate the website for the framework and find other information.

### OSINT

Google hacking/dorking is the practice of utilising Google's advanced search engine features. Examples of this are:

| Filter   | Example         | Description                                                 |
| -------- | --------------- | ----------------------------------------------------------- |
| site     | site:google.com | returns results only from the specified web address.        |
| inurl    | inurl:admin     | returns results that have the specified URL in the address. |
| filetype | filetype:pdf    | returns results which are a particular file extension.      |
| intitle  | intitle:admin   | returns results with a specified word in the title.         |

[Wappalyzer](https://www.wappalyzer.com/) is an online tool/browser extension that can help identify what technologies a website is using, like frameworks, Content Management Systems (CMS), payment processors and more.

[The Wayback Machine](https://archive.org/) is a historical archive of sites dating back to the 90s, you can search for a domain name and it will return all the times it was scraped for content.

GitHub can be used to search for company names or websites to try and find repositories belonging to a target, if successful, you may have access to source code or other content.

S3 Buckets are a service provided by Amazon AWS, allowing files and website content to be accessible over HTTP and HTTPS. Sometimes these permissions are set wrong and allow access to the public, the general format of these is: http(s)://{name}.s3.amazonaws.com. Other common names are {name}-assets, {name}-www, {name}-public or {name}-private.

### Automated Discovery

Automated discovery allows the use of tools rather than manual crawling. Tools like ffuf, dirb or gobuster can be used for website crawling automations.
