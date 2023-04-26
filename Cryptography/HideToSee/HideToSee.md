# Description

How about some hide and seek heh?

Look at this image here.

# Solution

```wget https://artifacts.picoctf.net/c/237/atbash.jpg```

Based on the name of the image it is probably decoding with atbash.

To get the extracted string from the image just run steghide without any passphrase.

```steghide extract -sf atbash.jpg```

From there I just did ```cat encrypted.txt``` and plugged it into cyberchef with the atbash cipher.

[cyberchef](https://gchq.github.io/CyberChef/)

Flag: ```picoCTF{atbash_crack_05...}```
