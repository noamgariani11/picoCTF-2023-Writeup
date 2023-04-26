# Description

Can you read files in the root file? 

The system admin has provisioned an account for you on the main server: 

```ssh -p 54578 picoplayer@saturn.picoctf.net```

Password: ```Sd9KYTm5kr```

Can you login and read the root file?

# Solution

```ssh -p 54578 picoplayer@saturn.picoctf.net```

Then enter ```Sd9KYTm5kr``` as the password. You can use control+shift+v to paste it into the feild. 

```cd ../..```

```cd cd challenge/```

```ls```

I just did cat, and copied the flag with control-shift-c. Based on the tag on the challenge though it was probably meant to do this command:

```vim metadata.json```

Than you can copy the flag from there.

Flag: ```picoCTF{uS1ng_v1m_3di...f1a}```
