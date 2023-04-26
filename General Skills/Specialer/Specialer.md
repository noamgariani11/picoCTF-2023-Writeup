# Description
Reception of Special has been cool to say the least. That's why we made an exclusive version of Special, called Secure Comprehensive Interface for Affecting Linux Empirically Rad, or just 'Specialer'. With Specialer, we really tried to remove the distractions from using a shell. Yes, we took out spell checker because of everybody's complaining. But we think you will be excited about our new, reduced feature set for keeping you focused on what needs it the most. 

Please start an instance to test your very own copy of Specialer. 

ssh -p 57125 ctf-player@saturn.picoctf.net.

The password is 483e80d4

# Solution

```ssh -p 57125 ctf-player@saturn.picoctf.net``` then enter the password.

If you click tab twice you see a list of commands:

![image](https://user-images.githubusercontent.com/91398631/228917813-664a2531-98d7-47c1-b265-c1492bd22894.png)

```echo "$(<file.txt)"``` is how you print contents of the file with echo. I already know echo works because I previously used ```echo Hi``` and messed aroung with other commands.

If you write cd in the main directory and click tab twice you can see everything there.

![image](https://user-images.githubusercontent.com/91398631/228919044-5b3949e3-96f6-40ea-936f-f169c5105539.png)

I then entered the abra/ directory with ```cd abra/``` and then did cd and clicked tab twice again. That showed cadabra.txt and cadaniel.txt files. echo "$(<cadabra.txt)" gives "Nothing up my sleeve!" and echo "$(<cadaniel.txt)" gives "Yes, I did it! I really did it! I'm a true wizard!". Since there was nothing in the abra/ directory I did ```cd ..```.

Then I went into the next directory with ```cd ala/```. There was kazam.txt and mode.txt files. echo "$(<kazam.txt)" gave the flag "return 0 picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01...8b71}".

Flag: ```picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01...8b71}```
