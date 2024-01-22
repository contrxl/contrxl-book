---
description: Usage of Burp Suite Repeater tool.
---

# Repeater

### Introduction

Repeater enables the modification and resending of intercepted requests to a target of our choosing. Requests which are captured by the Burp Proxy can be taken, manipulated and sent as needed. Alternatively, requests can be created from scratch similar to using cURL. The Repeater interface has six key components:

1. Request List : top left of the tab, displays repeater requests. Multiple can be managed simultaneously and each new request will appear here.
2. Request Controls : directly below the request list, allows sending of requests, cancellation of requests and navigation of request history.
3. Request and Response View : occupies the majority of the interface, can be used to edit the request and view the response.
4. Layout Options : located in the top right of Request/Response, allows customisation of the layout of the request & response views.
5. Inspector : on right hand side, allows analysis and modification of requests in a more intuitive manner.
6. Target : above the Inspector, specifies the IP address or domain which requests are sent to.

### Message Analysis Toolbar

Repeater provides many presentation options, the section located above the response box gives us four choices:

1. Pretty : default option, takes teh raw response and applies slight formatting enhancements to improve readability.
2. Raw : displays unmodified response directly from server without formatting.
3. Hex : see the response in a byte level representation.
4. Render : see the page as it would appear in a web browser.

Next to these options on the right hand side, we see the "Show Non-Printable Characters" button (\n). This displays characters that are not typically visible, for example, each line in the response typically ends with `\r\n`.

### Inspector

Inspector is supplementary to the request/response views in repeater. It can be used to obtain a visually organised breakdwon of requests and responses. Inspector can be used from the far right side of the Proxy and Repeater modules. The inspector allows for viewing and editing of:

* Request Query Parameters : data sent to server in URL, for example, a GET request like `https://example.com/?redirect=false` has the query parameter "redirect" set to false.
* Request Body Parameters : similar to the above but specific to a POST request, any data sent as part of a POST request will show here.
* Request Cookies : a modifiable list of cookies.
* Request Headers : view, access and modify headers sent with requests.
* Response Headers : headers returned to us by the server in response to our request.
