---
description: OWASP Juice Shop room write-up
---

# OWASP Juice Shop

### Recon

Performing a manual site walkthrough we can identify:

| IP            | Destination      | Description                                                                                 |
| ------------- | ---------------- | ------------------------------------------------------------------------------------------- |
| 10.10.126.152 | /search          | Site home page, list of products for sale.                                                  |
| 10.10.126.152 | /contact         | Contact form to submit user feedback. Has CAPTCHA challenge.                                |
| 10.10.126.152 | /about           | About the company page. Generic text and link to download "legal.md". Has links to socials. |
| 10.10.126.152 | /photo-wall      | Page containing photos.                                                                     |
| 10.10.126.152 | /login           | Login form for site.                                                                        |
| 10.10.126.152 | /forgot-password | Forgot password form, has security question mandatory field.                                |
| 10.10.126.152 | /register        | Registration form for new account.                                                          |

Seemingly an admin email can be gleaned by checking the reviews on items in /seach. Admin email is potentially admin@juice-sh.op.&#x20;

### Injection

A flag can be acquired by entering the string " ' OR 1==1" in the email field at /login.

A flag can be acquired by intercepting and modiying the login request on Burp to read:&#x20;

```
{"email":"' or 1=1--","password":"test"}
```

This will allow us to login to the administrator account. The ' will close the SQL query, 1=1 evaluates to try and -- comments out the rest of the data. Same technique can be adapted to login to the email address we are given:

```
{"email":"bender@juice-sh.op '", "password":"a"}
```

This works as the email is valid, which returns true.

### Brute-Force

To get the admin password we can brute-force using Burp intruder. We use the following request in intruder:

\[SCREENSHOT TO ADD]

Which gives us the admin password:

\[SCREENSHOT TO ADD]

We can find the login for Jim (jim@juice-sh.op) through reviews on the /search page. Here there is a Star Trek reference. Trying to reset Jim's password gives us his security question: "Your eldest siblings middle name?" Googling "jim star trek" gives us the name of James T. Kirks brother, which is the answer we need to Jim's security question to reset his password.

### Public Exposed Document

From the /about page where we can download "legal.md" we can see from the link that we can access "/ftp/". From here we can download acquisitons.md, then navigate to the home page again to get a flag.

We are unable to download /package.json.bak/ due to an error preventing download of any file that is not a .md or .pdf. We can bypass this by changing the URL to /package.json.bak%2500.md to mimick a .md file. Downloading this and navigating home gives a flag.

### Broken Access Control

A path to /#/administration can be found if the debugger is used to read /main-es2015.js. Logging into the admin account and navigating here gives a flag. We can also access other users shopping baskets by intercepting and modifying the request made when clicking "View Basket". Changing the basket/1 to basket/2 shows others baskets.

### XSS

Inserting:

```
<iframe src="javascript:alert(`xss`)">
```

into the site search bar returns an XSS alert box which gives us a flag and indicates the site is vulnerable to XSS.

We can create persistent XSS here by intercepting a logout request and adding the header "True-Client-IP" with the value:

```
<iframe src="javascript:alert(`xss`)">
```

