# Description

Don't power users get tired of making spelling mistakes in the shell? Not anymore! Enter Special, the Spell Checked Interface for Affecting Linux. Now, every word is properly spelled and capitalized... automatically and behind-the-scenes! Be the first to test Special in beta, and feel free to tell us all about how Special streamlines every development process that you face. When your co-workers see your amazing shell interface, just tell them: That's Special (TM) 

Start your instance to see connection details. 

```ssh -p 56058 ctf-player@saturn.picoctf.net ```

The password is d8819d45

# Solution

```ssh -p 56058 ctf-player@saturn.picoctf.net``` Then entering the password ```d8819d45```. 

This challenge turned all the normal commands into unusable ones. For instance, ls turns to Ls, clear turns to Clear, cd.. turns into Ad i, and so on.

There were many things I tried and found to partially work, but here is the path I went down when I found a right way to do it:

| Command | Output | 
| :---:   | :---:  |
|${parameter?ls} | parameter: ls|
|${:ls} | Bad substitution|
|${parameter=ls} | blargh|
|${parameter=cat blargh} | cat: blargh: Is a directory|
|${parameter=cd blargh} | ${parameter=cd blargh}|
|${parameter=ls blargh} | flag.txt |
|${parameter=cat < blargh/flag.txt} | This gave the flag |

This took a long time of testing different commands and seeing what works. I'm sure there are many ways to do this as I stumbled upon other potential ways to complete this challenge but ended up going with this. 

Flag: ```picoCTF{5p311ch3ck_15_7h3_w0...35}```
