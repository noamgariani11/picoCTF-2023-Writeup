# Description

Someone just sent you an email claiming to be Google's co-founder Larry Page but you suspect a scam.

Can you help us identify whose mail server the email actually originated from?

Download the email file here. Flag: picoCTF{FirstnameLastname}

# Solution

If you open email-export.eml in outlook and then go to File then Properties you will see the ip adress.

``` client-ip=173.249.33.206; ```

I used this website for the whois search: https://www.whois.com/whois/

If you scroll down you will see:

person:         Wil____ Zwa____

Then put it in the correct format and you have your flag.

Flag: ```picoCTF{Wil...Zwa...}```
