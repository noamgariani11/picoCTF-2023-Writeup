# Description

Get the flag and reach the exit. 

Welcome to BabyGame! 

Navigate around the map and see what you can find! The game is available to download here. There is no source available, so you'll have to figure your way around the map. 

You can connect with it using nc saturn.picoctf.net 52987.

# Solution

```wget https://artifacts.picoctf.net/c/221/game```

Running it locally works faster, but you can only get the flag if you do it with ```nc saturn.picoctf.net 52987```. But to run it locally you just have to do ```sudo chmod +x game``` then ```./game```.

I looked around the game a lot and saw that if you go to the very top there is a segmentation fault. If you go to the very right then it puts you on a level below and on the very left. If you go the the very left it puts you on a level above and to the very right. Also if you just go to the "X" then it says "You Win" and does not give the flag. I then tried going to the very bottom and although there was no segmentation fault nothing happened. 

Knowing the mechanics of the game the only place that going to the very left or very right doesn't put you in the same place in the game is the very top left corner. 

If you go left in the top left corner with "a" 4 times you see now that "Player has flag: 64" if you go 5 times there is a segmentation fault. 

If you go back out with flag being 64 to the X now then it changes to "Player has flag: 46" 

Once you get to the X it will print this "flag.txt not found in current directory". 

This is good because if you do the same thing but while using ```nc saturn.picoctf.net 52987``` then you will get the flag.

Flag: ```picoCTF{gamer_m0d3_enabl...8e6}```
