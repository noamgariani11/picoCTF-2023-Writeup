# Description

Can you solve this? 

What two positive numbers can make this possible: n1 > n1 + n2 OR n2 > n1 + n2 

Enter them here nc saturn.picoctf.net 60781. Source

# Solution

```wget https://artifacts.picoctf.net/c/456/flag.c```

Then ```cat flag.c``` to look at the source code. You can see to get the flag it wants you to add to positive integers to create integer overflow. If you add to big of a number it wont process. To do this you need to know the maximum integer value which is 2147483647. If you add 2147483647 and 2147483647 then you get the flag.

![image](https://user-images.githubusercontent.com/91398631/228923203-230cfb5b-ac6c-4914-91fb-4d6edec8c96c.png)

Flag: ```picoCTF{Tw0_Sum_Integer_Bu773R_0v3rf...8bd}```
