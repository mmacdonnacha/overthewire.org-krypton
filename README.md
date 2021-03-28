# Overthewire.org - Krypton

[overthewire.org/krypton](https://overthewire.org/wargames/krypton/)

|Level|
|---|
|[Krypton 0](##krypton-0)|
|[Krypton 1](##krypton-1)|



---


# Krypton 0
## Level Info  
**Krypton Level 0 → Level 1**  

Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:  

S1JZUFRPTklTR1JFQVQ=  

Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/  

## Walkthrough
```bash
~$ echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d
<PASSWORD>
```

Use the password to login to krypton1.

---


# Krypton 1
## Level Info  
**Krypton Level 1 → Level 2**  
The password for level 2 is in the file ‘krypton2’.  
It is ‘encrypted’ using a simple rotation.  
It is also in non-standard ciphertext format.  
When using alpha characters for cipher text it is normal to group the letters into 5 letter clusters, regardless of word boundaries.  
This helps obfuscate any patterns.  
This file has kept the plain text word boundaries and carried them to the cipher text. Enjoy!


## Walkthrough

Login to krypton1 using the password from obtained from previous level
```bash
~$ ssh krypton1@krypton.labs.overthewire.org -p 2231
```

Looking at the directory **/krypton/krypton1/** we can see 2 files krypton2 and README.  
README contains instructions for the level.
```
Welcome to Krypton!

This game is intended to give hands on experience with cryptography
and cryptanalysis.  The levels progress from classic ciphers, to modern,
easy to harder.

Although there are excellent public tools, like cryptool,to perform
the simple analysis, we strongly encourage you to try and do these
without them for now.  We will use them in later excercises.

** Please try these levels without cryptool first **


The first level is easy.  The password for level 2 is in the file
'krypton2'.  It is 'encrypted' using a simple rotation called ROT13.
It is also in non-standard ciphertext format.  When using alpha characters for
cipher text it is normal to group the letters into 5 letter clusters,
regardless of word boundaries.  This helps obfuscate any patterns.

This file has kept the plain text word boundaries and carried them to
the cipher text.

Enjoy!
```

According to the README the contents of **krypton2** is encrypted using a rotation cipher called ROT13. A becomes N, B becomes O, ... Y becomes L, Z becomes M.

Using the **tr** command we can reverse the ROT13 and get the decrypted contents of **krypton2**.

```bash
Krypton1@krypton:/krypton/krypton1$ cat krypton2
YRIRY GJB CNFFJBEQ EBGGRA

krypton1@krypton:/krypton/krypton1$ cat krypton2 | tr A-Z N-ZA-M
LEVEL TWO PASSWORD <PASSWORD>
```

