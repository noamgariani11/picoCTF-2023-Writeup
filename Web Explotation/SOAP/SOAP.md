# Description

The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?

Web Portal

# Getting Started

Simple Object Access Protocol (SOAP) and the tag on the challenge says XXE.

XXE is XML external entity injection. [PortSwigger](https://portswigger.net/web-security/xxe) has a good page describing almost exactly this challenge.

This is the XXE payload that is on the PortSwigger site linked above:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```

# Setting Up BurpSuite

To implement the injection it is easiest with BurpSuite. BurpSuite is software that is very useful for web penetration testing.

Steps in BurpSuite:

* Create a Temporary project as soon as BurpSuite opens by just pressing "Next" with the default configurations.

![image](https://user-images.githubusercontent.com/91398631/232889427-3a7e912a-4f38-4273-8bf0-507f8758507b.png)

* Then click "Start Burp" with Burp Defaults.

![image](https://user-images.githubusercontent.com/91398631/232889471-ea12a95d-3faf-4613-889a-ac54b5f96c3a.png)

* Then go to the proxy tab.

![image](https://user-images.githubusercontent.com/91398631/232889613-e2e0dd3f-8da5-453c-8b58-87e58930e75c.png)

* Then open the BurpSuite browser. Now anything you do in that browser you can see and manipulate incoming packets.

![image](https://user-images.githubusercontent.com/91398631/232889733-f9593a72-1521-4e55-8f53-85a2ef77b65b.png)

* Once you're in the BurpSuite web browser paste the link from the challenge ```http://saturn.picoctf.net:52948/``` 

# Solution

Back in BurpSuite turn Intercept to on. This will stop all traffic so you can inspect the packets before they are sent. You can than change the packets however you want.

![image](https://user-images.githubusercontent.com/91398631/232891071-e480c306-20fe-49fe-adaf-bf746afe8b60.png)

If you click the "Details" button under "Carnegie Mellon University Africa" (Any of the three will also work) you can see XML in the intercepted packet.

![image](https://user-images.githubusercontent.com/91398631/232891406-a476216f-a371-44c5-8781-6129390694e7.png)

Now looking at the earlier XXE Payload

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>
```

This is the important part: ```<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>```. All you have to do is place that under the ```<?xml version="1.0" encoding="UTF-8"?>``` and then you have done the injection. 

![image](https://user-images.githubusercontent.com/91398631/232892937-ee203b72-93b0-433f-ab9b-b668f8eef44d.png)

Now all you have to do is add ```&xxe;``` before the 1 to show the output of the injection. Then you can forward the packet and you will see the flag on the page.

![image](https://user-images.githubusercontent.com/91398631/232893005-5f96218f-9190-4973-818a-e2626f0a7e55.png)

Flag: ```picoCTF{XML_3xtern@l_3nt1t1ty_4db...}```
