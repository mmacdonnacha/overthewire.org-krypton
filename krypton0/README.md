# Krypton Level 0 -> Level 1
## Level Info  
**Krypton Level 0 → Level 1**  

Welcome to Krypton! The first level is easy. The following string encodes the password using Base64:  

S1JZUFRPTklTR1JFQVQ=  

Use this password to log in to krypton.labs.overthewire.org with username krypton1 using SSH on port 2231. You can find the files for other levels in /krypton/  

## Walkthrough
The description tells us the password has been encoded using base64 encoding. So we only need to decode the string to obtain the password. Linux terminal has a base64 command that can be used to decode the password.

```bash
~$ echo "S1JZUFRPTklTR1JFQVQ=" | base64 -d
<PASSWORD>
```

Use the password to login to krypton1.