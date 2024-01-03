---
description: Brute-forcing lab.
---

# Day 4: Baby, it's CeWLd Outside

### Introduction

It is identified that company credentials have been sold, leading to a hacker exploiting a portal. From logs, it is found that the brute force did not take a long time. This points to the use of a customised wordlist.

### Practical

CeWL is the tool we will use to generate a custom wordlist, CeWL spiders websites to generate wordlists based on their content. Generating a basic wordlist from CeWL and outputting it is very simple.

```
cewl http://IP_ADDR -w customlist.txt
```

This creates a wordlist from the target site and outputs it to customlist.txt. To try the brute-force here we need to use cewl to create a password list and a username list. To create the password list we use:

```
cewl -d 2 -m 5 -w passwords.txt http://IP_ADDR --with-numbers
```

\[SCREENSHOT TO ADD]

To create the username list we use:

```
cewl -d 0 -m 5 -w usernames.txt http://IP_ADDR --lowercase
```

The custom options here specify the following:

1. \-d : specifies how deep CeWL spiders, -d 2 would spider two links deep
2. \-m : specifies the minimum word length, -x can be used to specify a maximum word length
3. \-w : writes the output to a file
4. \--with-numbers : appends numbers to words
5. \--lowercase : forces all words lowercase

\[SCREENSHOT TO ADD]

With these lists we can now use wfuzz to brute-force /login.php. The following command uses our wordlists to brute force the /login.php page:

```
wfuzz -c -z file,usernames.txt -z file,passwords.txt --hs "Please enter the correct credentials" -u http://IP_ADDR/login.php -d "username=FUZZ&password=FUZ2Z"
```

The options defined here are:

1. \-z file,username.txt : loads usernames list
2. \-z file,passwords.txt : loads passwords list
3. \--hs : hides responses containing the string "Please enter the correct credentials"
4. \-u : specify target URL
5. \-d "username=FUZZ\&password=FUZ2Z" : provides the POST data format where FUZZ is replaced by usernames and FUZ2Z is replaced by passwords.

\[SCREENSHOT TO ADD]

### Answers for Day 4

<details>

<summary>Expand to see answers!</summary>

1. What is the correct username and password combination? Format username:password. **isaias:Happiness**
2. What is the flag? **THM{m3rrY4nt4rct1crAft$}**

</details>
