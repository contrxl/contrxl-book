---
description: First section in Jr Penetration Tester learning path.
---

# Walking an Application

### Exploring a Website

Finding interactive website sections is important in recon, a good way to start is explore the website manually and take a note of any interesting pages/areas/features. An example version of this would look like the below:

| Feature      | URL                | Summary                                                                                 |
| ------------ | ------------------ | --------------------------------------------------------------------------------------- |
| Home Page    | /                  | Summary of what ACME IT Support does, with a staff photo.                               |
| Latest News  | /news              | List of recently published articles, each one has an ID number like article?id=1.       |
| News Article | /news/article?id=1 | Displays individual articles, some articles are blocked/reserved for premium customers. |

### Page Source

Page source can be viewed in most browsers by right-clicking the page and selecting "View Page Source", alternatively you can put "view-source:" in front of the address, like: view-source:https://www.google.com.&#x20;

In page source you can view HTML code, look for comments left behind by developers, denoted by code that starts with `<!--` and ends with `-->`. Links to other pages can also be seen in anchor tags, these start with `<a href` and enmd with `</a>`.

External files like CSS, JavaScript and images can be included in HTML. These files should lead to a 403 or blank page stating no access. If these are viewable to the public there is a chance they could expose private information to the public.

### Developer Tools - Inspector

The inspector allows for live client-side editing of interactive page elements.

### Developer Tools - Debugger

Debugger is used for debugging JavaScript, this is called debugger in Firefox and Safari, but is referred to as "Sources" in Google Chrome.

### Developer Tools - Network

This tab can be used to keep track of all the external requests a web page makes.
