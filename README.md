# Overthewire.org - Krypton

[overthewire.org/krypton](https://overthewire.org/wargames/krypton/)

|Level|
|---|
|[Krypton 0](##krypton-0)|
|[Krypton 1](##krypton-1)|
|[Krypton 2](##krypton-2)|


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

---


# Krypton 2
## Level Info  
**Krypton Level 2 → Level 3**  
Krypton 2

ROT13 is a simple substitution cipher.

Substitution ciphers are a simple replacement algorithm.  In this example
of a substitution cipher, we will explore a 'monoalphebetic' cipher.
Monoalphebetic means, literally, "one alphabet" and you will see why.

This level contains an old form of cipher called a 'Caesar Cipher'.
A Caesar cipher shifts the alphabet by a set number.  For example:

plain:  a b c d e f g h i j k ...
cipher: G H I J K L M N O P Q ...

In this example, the letter 'a' in plaintext is replaced by a 'G' in the
ciphertext so, for example, the plaintext 'bad' becomes 'HGJ' in ciphertext.

The password for level 3 is in the file krypton3.  It is in 5 letter
group ciphertext.  It is encrypted with a Caesar Cipher.  Without any
further information, this cipher text may be difficult to break.  You do
not have direct access to the key, however you do have access to a program
that will encrypt anything you wish to give it using the key.
If you think logically, this is completely easy.

One shot can solve it!

Have fun.

Additional Information:

The `encrypt` binary will look for the keyfile in your current working
directory. Therefore, it might be best to create a working direcory in /tmp
and in there a link to the keyfile. As the `encrypt` binary runs setuid
`krypton3`, you also need to give `krypton3` access to your working directory.

Here is an example:

```bash
krypton2@melinda:~$ mktemp -d
/tmp/tmp.Wf2OnCpCDQ
krypton2@melinda:~$ cd /tmp/tmp.Wf2OnCpCDQ
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ln -s /krypton/krypton2/keyfile.dat
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
keyfile.dat
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ chmod 777 .
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ /krypton/krypton2/encrypt /etc/issue
krypton2@melinda:/tmp/tmp.Wf2OnCpCDQ$ ls
ciphertext  keyfile.dat
```

## Walkthrough

README is the same as description
followed bash steps to create a directory in the tmp folder
/krypton/krypton2/encrypt <INPUT_FILE> outputs to a ciphertext file.

created file with "AAAAAAA" to run encrypt
ciphertext contained "MMMMMMM"
So "A" maps to "M"

created file with alphabet "ABCDEFGHIJKLMNOPQRSTUVWXYZ" and ran encrypt to see what each letter maps to
plaintext -> "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
ciphertext -> "MNOPQRSTUVWXYZABCDFGHIJKL"


```bash
krypton2@krypton:/krypton/krypton2$ cat krypton3 
OMQEMDUEQMEK

krypton2@krypton:/krypton/krypton2$ cat krypton3 | tr M-ZA-L A-Z
<PASSWORD>
```
---

