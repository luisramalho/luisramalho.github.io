---
layout: post
title: RSA Public Key Encryption
---
University assignment that demonstrate the RSA public key encryption in Java.

>Public-key cryptography is a cryptographic approach which involves the use of asymmetric key algorithms instead of or in addition to symmetric key algorithms.

RsaCoder encrypts or decrypts a message with given key. The RsaKey simply represents a pair of two large numbers. The RsaKeyPair represents a generated RSA key pair. Modular exponentiation is used for encryption and decryption. The total number of operations is logarithmic in the size of i or j, by combining exponents that are powers of 2. The ‘mod n’ operation was applied on the intermediate results of exponentiation, to avoid excessively big numbers.

Receiver generates a key pair, of which the public key is made available. It has another public method receive, which takes cipher text (of type BigInteger), decrypts it and outputs it.

Sender has a public method sendTo, with a Receiver as argument. This method generates a random number that is not too big. This message is then encrypted by the public key obtained from the receiver and this is communicated to the receiver. (The message before encryption is also output, in order to test the correctness.)

Source code is [here](https://github.com/luisramalho/rsa-public-key-encryption.git).