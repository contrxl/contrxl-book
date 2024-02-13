---
description: Other modules in Burp Suite.
---

# Other Modules

### Decoder

Decoder provides data manipulation capabilities, it can decode data intercepted during an attack as well as encode data we provide it for transmission. It can also create hash sums of data and offers a Smart Decode feature, which tries to decode data recursively until it is plaintext again. Encoder and decoder offer:

* Plaintext
* URL Encoding
* HTML
* Base64
* ASCII Hex
* Hex Octal
* Binary
* Gzip

### Comparer

Comparer allows for the comparison of two pieces of data, either by ASCII words or bytes.

### Sequencer

Sequencer allows the evaluation of the randomness of "tokens". Tokens are strings used to identify something which should be generated in a cryptographically secure manner. These could be cookies or Cross-Site Request Forgery (CSRF) tokens, if these aren't generated securely, we could predict upcoming values.
