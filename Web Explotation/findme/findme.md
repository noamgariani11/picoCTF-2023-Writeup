# Description

Help us test the form by submiting the username as test and password as test!

The website running here.

# Solution

Enter the site.

Press f12 to get into developer tools.

Go to the Network tab.

Then click perserve logs so it will log the logs when you log in.

Then enter with the username as ```test``` and password as ```test!```.

You will immeditaily see too different id's:

```id=cGlj...VzX2Fs```

```id=bF90aG...YmJhZTlhfQ==```

This looks like base64 so I intially put the second part as it had "==" which made it look like base64. I got this back ```...y_25bbae9a}``` which looks like the end of a flag. When you put both of the id's together you get the flag once you decode the base64.

Flag: ```picoCTF{prox...bae9a}```
