# Description

This image passes LSB statistical analysis, but we can't help but think there must be something to the visual artifacts present in this image... 

Download the image here

# Solution

The challenge is called MSG and the description says that it didn't pass LSB statistical analysis. This makes me think it is probably MSB (Most Signifigant Bit) analysis.

To install stegsolve:

```
wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve.jar
chmod +x stegsolve.jar
```

Then just run stegsolve:

```java -jar stegsolve.jar```

It will be a small pop-up in top left so just expand the window. Then go to file then open and then find the file "Ninja-and-Prince-Genji-Ukiyoe-Utagawa-Kunisada.flag.png" to put into stegsolve. 

Once you are there you could go through the planes and mess aroung with the other stegsolve features but since it is MSB I went straight to Analyse then data extract. 

Bit order set to MSB First and I used Row for extract by. From here I just tested many different options and scrolled through many options as to not miss anything. 

Eventually I found that if you check Red 7, Green 7, and Blue 7 with nothing else and then scroll up there is human readable text.

I then clicked save text and saved it in my directory (I called the file text). 

```cat text | grep pico```

After running this command I found this: ```picoCT F{15_y0u```. So I knew the flag was in there.

Then I ran this command ```strings text | less``` and used ```/pico``` to search for the flag. And there was the flag.

220a7069636f4354 467b31355f793075  ".picoCT F{15_y0u
725f71756535375f 7175317830373163  r_que57_ qu1.....
5f30725f68337230 31635f3234643535  _0r_...0 1c_24d55
6265657d0a0a2254 686f752068617374  bee}.."T hou hast

Just be sure to get rid of all the spaces in the flag before submitting.

Flag: ```picoCTF{15_y0ur_que57...d55bee}```

---

Resource [Stegsolve installation instructions](https://github.com/zardus/ctf-tools/blob/master/stegsolve/install)
