# Description

Can you make a CoreWars warrior that always loses, no ties? 

Your opponent is the Imp. The source is available here. 

If you wanted to pit the Imp against himself, you could download the Imp and connect to the CoreWars server like this: 

nc saturn.picoctf.net 62089 < imp.red

# Solution

```wget https://artifacts.picoctf.net/c/311/imp.red```

Modify imp.red to this:

```
;redcode
end
```

This would make you loose every time.

```nc saturn.picoctf.net 62089 < imp.red```

The flag shows up at the end when it's done running.

Flag: ```picoCTF{h3r0_...6d4cf}```
