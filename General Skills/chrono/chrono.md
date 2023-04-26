# Description

How to automate tasks to run at intervals on linux servers? Use ssh to connect to this server:

Note: The information below will be different for everyone and will be given when you launch an instance.

Server: saturn.picoctf.net

Port: 49702

Username: picoplayer 

Password: ekj2GJuiv4

# Solution

```ssh picoplayer@saturn.picoctf.net -p 49702```

Then enter ```ekj2GJuiv4``` as the password. You can use control+shift+v to paste it into the feild. 

```cd ../..```

```cd challenge/```

```cat metadata.json```

The flag is in that file. You could also use grep if you wanted to, but it's a small file. You can easily just copy paste the flag from the top.

Flag: ```picoCTF{Sch3...44}```
