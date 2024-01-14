---
description: Hash cracking tool.
---

# John the Ripper

### Introduction

John is one of teh most well known hash cracking tools, it has a fast cracking speed and a wide range of compatible hash types.&#x20;

Hashes are a way to take data of any length and output it as data of a fixed length. There are many  popular hashing algorithms like MD4, MD5, SHA1 and NTLM. If we took the string "polo" and ran it through a MD5 hash algorithm, we would get the output b53759f3ce692de7aff1b5779d3964da. This is a standard 32 character MD5 hash. If we took the string "polomints" and ran it through a MD5 hash algorithm we would get 584b6e4f4586e136bc280f27f9c64f3b. Also, a 32 character MD5 hash, even though "polomints" is a longer string.

Hashes are secure because they cannot be reversed using purely the output given. This is based on the complicated mathematical problem of [P vs NP](https://en.wikipedia.org/wiki/P\_versus\_NP\_problem). This problem means that the algorithm used to hash the value is "NP", and that can be calculated reasonably, however, to un-hash the value we would use "P", which is intractable to solve and therefore cannot be computed in reasonable time.

Although the algorithm is irreversible, John uses a dictionary of known hashes and their outputs to see if any match.

### Installation

Parrot OS & Kali Linux come with Jumbo John installed by default. This can be confirmed by typing `"john"` into a terminal and verifying the output reads "John the Ripper 1.9.0-jumbo-1" or something similar. If not, installation is done using `"sudo apt install john".`

Blackarch may not have it by default, the command `pacman -Qe | grep "john"` can be used to check, output should read "john 1.9.0.jumbo1-5" or similar. If it is not installed, `pacman -S john` should do it.

To install from source, follow the below steps:

1. Run `git clone https://github.com/openwall/john -b bleeding-jumbo john` to clone the Jumbo John repo.
2. Use `cd john/src` to move into the source code directory.
3. Use `./configure` to check dependencies and options that have been configured.
4. Use `make -s clean && make -sj4` to build a binary and then change to the above run directory using `cd ../run`.
5. Test using `./john --test`.

### Basic Usage

The very basic syntax to use john is:

```
john [options] [file path]
```

"john" invokes John the Ripper and \[file path] is the location of the file containing the hash you are trying to crack.

John can try to crack a file without being given the type of hash, this isn't always reliable but can be done simply using:

```
john --wordlist=[wordlist path] [file path]
```

John won't always like this and may need a format to be specified, there are tools to identify hash types like [Hashes.com](https://hashes.com/en/decrypt/hash) or [HashID](https://pypi.org/project/hashID/). Once a format has been identified, we can use this to tell john to use it with the following syntax:

```
john --format=[format] --wordlist=[wordlist path] [file path]
```

Sometimes, when telling john to use formats you may need to prefix it with `raw-` to tell john it is a standard hash type. To check if you need the prefix, you can use `john --list=formats` to check manually or search using `john --list=formats | grep -iF "md5"`.

### Unshadowing

For John to understand the hashes from /etc/shadow it needs to be combined with /etc/passwd. This can be done using the following syntax:

```
unshadow [passwd path] [shadow path]
```

Here, "passwd path" is a copy of the /etc/passwd file from the target machine, and "shadow path" is a copy of the /etc/shadow file from the target machine. This can either be done on the entire file or just on the relevant lines, an example of this in use would be:

```
unshadow local_passwd.txt local_shadow.txt > unshadow.txt
```

We can then use "unshadow.txt" with John as before to crack the hash. Format should not need to be specified but in some cases sha512crypt may need to be specified.

### Single Crack Mode

Single crack mode tells John to only use the information provided in the username to work out possible passwords by "mangling" the numbers and letters in the username.

Word mangling is where John builds its own dictionary of possible passwords based on the information it is given. For example, with username "James", possible passwords could be "James1, JAmes, James!" and so on. The syntax for using this is more or less the same as previous:

```
john --single --format=[format] [file path]
```

The only thing to note here is that for John to work in single-crack mode, it needs to have the file format changed slightly, for example, to use single crack with username "polo" on the hash b53759f3ce692de7aff1b5779d3964da, we need to change the text to polo:b53759f3ce692de7aff1b5779d3964da for John to understand.

### Custom Rulesets

John allows you to define your own set of rules, which it will use to dynamically create passwords. This is useful where you know more info about the password structure of your target. For instance, you may know that a password must contain a capital letter, a symbol and a number.

Custom rules are defined in the john.conf file which is located in /etc/john/john.conf. Full details of creating custom rules can be read in the [docs](https://www.openwall.com/john/doc/RULES.shtml).&#x20;

### Cracking Password Protected ZIP Files

John can be used to crack password protection on ZIP files, first, the John suite must convert the ZIP to a format which it can understand. The basic syntax for this is:

```
zip2john [options] [zip file] > [output path]
```

We can then take the output of this and pass it to John as we normally would using any required options.

### Cracking Password Protected RAR Archives

A similar method to the above can be used for cracking passwords on RAR files. The syntax for this is:

```
rar2john [rar file] > [output path]
```

Once again, the output of this can be fed to John as normal.

### Cracking SSH Keys

John can also be used to crack id\_rsa files used in SSH authentication. Again, we will need to convert the id\_rsa file to a format which John can understand, this can be done using the following syntax:

```
ssh2john [id_rsa file] > [output path]
```

Once again, we feed this output to John as normal to crack the hash.
