# Description

What can you do with this file?

I forgot the key to my safe but this file is supposed to help me with retrieving the lost key. Can you help me unlock my safe?

# Solution

```wget https://artifacts.picoctf.net/c/290/SafeOpener.class```

```cat SafeOpener.class```

The flag near the end of the file.

Alternatively if you want to do the challenge the way it was probably intended (decompling the file) you can use jd-gui.

```sudo apt install jd-gui```

I then opened the file.

![image](https://user-images.githubusercontent.com/91398631/233233553-28ecb0a9-92bd-4ba6-b4f9-426080b03901.png)

Than saved the file.

![image](https://user-images.githubusercontent.com/91398631/233233612-14895f51-b1b8-4432-8ffc-d25965ef5877.png)

Once it was saved I ran this command to get only the flag.

```cat SafeOpener.java | grep pico | cut -d "\"" -f1```

Grep gets the line with "pico" which is the flag. And cut looks at the " delimiter where I used \ as an escape charater, -f1 is for looking at the first feild.

Flag: ```picoCTF{SAf3_0p3...8a993}```
