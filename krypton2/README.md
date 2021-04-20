# Krypton Level 2 -> Level 3

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
After logging into krypton2 level I checked the **/krypton/krypton2** directory.  
```
krypton2@krypton:/krypton/krypton2$ ls -al
total 32
drwxr-xr-x 2 root     root     4096 May 19  2020 .
drwxr-xr-x 8 root     root     4096 May 19  2020 ..
-rwsr-x--- 1 krypton3 krypton2 9032 May 19  2020 encrypt
-rw-r----- 1 krypton3 krypton3   27 May 19  2020 keyfile.dat
-rw-r----- 1 krypton2 krypton2   13 May 19  2020 krypton3
-rw-r----- 1 krypton2 krypton2 1815 May 19  2020 README
```
There is 4 files *README*, *krypton3*, *encrypt* and *keyfile.dat*.

**README** contains the same information as the description on the overthewire site [overthewire.org/krypton2](https://overthewire.org/wargames/krypton/krypton2.html)

**krypton3** is the encrypted password for the next level.

**encrypt** is a executable file used to encrypt ASCII text.

**keyfile.dat** is used by the encrypt executable to perform encryption.


I followed the instructions at the bottom of the `README` to create a directory in `/tmp` and set up the files to begin cracking the encryption.

I created a `plaintext` file containing all `A`'s and run the `encrypt` executable.

```bash
krypton2@krypton:/tmp/tmp.grT4tZ71Y6$ /krypton/krypton2/encrypt plaintext
krypton2@krypton:/tmp/tmp.grT4tZ71Y6$ cat ciphertext
MMMMMMMMM
```
 
From this I could see A is encrypted as M.  
In order to find out the whole alphabet I write `ABCDEFGHIJKLMNOPQRSTUVWXYZ` to the plaintext file.  
Running the `encrypt` executable again will create a `ciphertext` file with the mapping of the whole alphabet.

```
plaintext  -> "ABCDEFGHIJKLMNOPQRSTUVWXYZ"  
ciphertext -> "MNOPQRSTUVWXYZABCDEFGHIJKL"
```

Now with the knowledge of what character encrypts to what character I can decrypt the password.

```bash
krypton2@krypton:/krypton/krypton2$ cat krypton3 
OMQEMDUEQMEK

krypton2@krypton:/krypton/krypton2$ cat krypton3 | tr M-ZA-L A-Z
<PASSWORD>
```