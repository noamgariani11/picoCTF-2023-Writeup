# Description

Can you make a CoreWars warrior that wins every single round? 

Your opponent is the Imp. The source is available here. If you wanted to pit the Imp against himself, you could download the Imp and connect to the CoreWars server like this: 

nc saturn.picoctf.net 54217 < imp.red 

To get the flag, you must beat the Imp all 100 rounds.

# Solution

I used this [website](https://corewar.co.uk/) for refrence in trying different warriors. More specifically the [strategy](https://corewar.co.uk/strategy.htm) guide. The Binary Launch Imp was very close to getting 100, in one attempt I was able to get 97 but not quite 100. Since it was so close I tried running a script that tried it 1000 times but it didn't get to 100.

Then I went on to try other startegies and eventually came across the [bomber](https://corewar.co.uk/bomber.htm) strategy. The first 3 weren't very good (around 50/60 wins) but the fourth one [Herem/Scimitar](https://corewar.co.uk/heremscimitar.htm) was the one that gave 100 wins instanly no need to try mutliple times.


Flag: ```picoCTF{d3m0n_3xpu...24e}```
