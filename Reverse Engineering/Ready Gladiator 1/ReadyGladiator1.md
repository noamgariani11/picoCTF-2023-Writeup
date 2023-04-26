# Description

Can you make a CoreWars warrior that wins? Your opponent is the Imp. 

The source is available here. 

If you wanted to pit the Imp against himself, you could download the Imp and connect to the CoreWars server like this: 

nc saturn.picoctf.net 63042 < imp.red 

To get the flag, you must beat the Imp at least once out of the many rounds.

# Solution

```wget https://artifacts.picoctf.net/c/408/imp.red```

Modify imp.red to this:

```
;redcode
;name Imp Ex
add #4, 3
mov 2, @2
jmp -2
dat #0, #0
end
```

This was found in the documentation under warriors. Here is the [link](https://corewar-docs.readthedocs.io/en/latest/corewar/warriors/).

```nc saturn.picoctf.net 63042 < imp.red```

The flag appears after it finishes running.

Flag: ```picoCTF{1mp_1n...5_ec57a42e}```
