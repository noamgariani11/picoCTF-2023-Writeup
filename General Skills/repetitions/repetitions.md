# Description

Can you make sense of this file?

Download the file here.

# Solution

```echo "cat enc_flag | base64 --decode | base64 --decode | base64 --decode | base64 --decode | base64 --decode | base64 --decode" > script.sh```

```sudo chmod +x script.sh```

```./script.sh```

You could also just put the text from the enc_flag file into cyberchef. You can just put decode from base64 many times until you see the flag. Cyberchef might also give you the magic pop-up to decode from base64. Also if your not in linux and you can't just do ```cat enc_flag``` than you can always open the file with notepad++.

Flag: ``` picoCTF{base64_n3st...e523f49} ```
