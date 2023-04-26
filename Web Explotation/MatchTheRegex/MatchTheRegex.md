# Description

How about trying to match a regular expression

The website is running here.

# Solution

I started with trial and error using regex then looked at the source code at it became obvious. 

![image](https://user-images.githubusercontent.com/91398631/230785350-5f85a222-98b2-4561-a2a6-58f2b206ae24.png)

The comment in the source code gives a very big hint into what it is.

```// ^p.....F!?```

The comment shows that it started with 'p' and ends with 'F' which based on the challenge is probably "picoCTF" (case-sensitive) which it was and it gets the flag.

"picoCTF!" and "picoCTF!?" also result in the flag.

Flag: ```picoCTF{succ3s...ad436ed}```
