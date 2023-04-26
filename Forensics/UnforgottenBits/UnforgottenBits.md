# Description

Download this disk image and find the flag. 

Note: if you are using the webshell, download and extract the disk image into 

/tmp not your home directory.

* Download compressed disk image

# Solution

This is a large disk image so there will be a lot of documentation so as not to miss anything. There are things that come up later on that you can match with earlier documentation.

# Getting the disk into Autopsy

Start with getting the file:

```wget https://artifacts.picoctf.net/c/485/disk.flag.img.gz```

Then unzipping it (since it's a large file it might take some time):

```gunzip disk.flag.img.gz```

Then opening it in autopsy. Also a note that this process is asumming you are using the linux version of autopsy and not other versions (windows).

```sudo autopsy```

Open the link provided: ```http://localhost:9999/autopsy```

Click "New Case". 

![image](https://user-images.githubusercontent.com/91398631/232164990-5de3e85c-53b3-47c8-ac89-bcfec4e0a7d4.png)

Then fill in the "Case Name" and "Investigator Name" and click "New Case" again. 

![image](https://user-images.githubusercontent.com/91398631/232165154-eabf3a36-9c2f-42e4-af0e-4cd270a2eaf1.png)

Then click "add host" with the default investigator name.

![image](https://user-images.githubusercontent.com/91398631/232165281-256283ef-d832-4e9c-a0a3-54a4adcf3864.png)

No need to change any of the defualts, just click "add host" again. 

![image](https://user-images.githubusercontent.com/91398631/232165302-5a62c429-ce62-4b16-9553-abdfd26ba5be.png)

Then click "add image" 

![image](https://user-images.githubusercontent.com/91398631/232165368-847dbd91-222a-491f-8848-a6b597b856e2.png)

Then "add image file". 

![image](https://user-images.githubusercontent.com/91398631/232165409-f8e6a997-bc83-4b81-ab7b-426cd51df8d2.png)

To find the Location (full path) of the file run this command: ```realpath disk.flag.img```

![image](https://user-images.githubusercontent.com/91398631/232165425-82ccd2fb-338d-4e29-adc3-02ac3ccd766a.png)

It will give you the full path of that file. Alterantivly you can use pwd and then just append the file name to the end manually. Once you put the full path of the file in press "next".

Now just click "add", again with just the defualts.

![image](https://user-images.githubusercontent.com/91398631/232165528-dfeb08af-f390-4812-883d-928aa7e77e55.png)

Then "Ok".

![image](https://user-images.githubusercontent.com/91398631/232165554-7e79ba95-0e3d-43d5-a8c1-7681cb173a52.png)

I then selected "3" as it was the largest image, then clicked analyze.

![image](https://user-images.githubusercontent.com/91398631/232165605-f9da97f8-2a1c-4df3-b96d-97fe85f7324c.png)

Then click "File Analysis".

![image](https://user-images.githubusercontent.com/91398631/232165633-69156a75-1714-4991-b75c-aae86599ddd1.png)

I then clicked "Expand Directories" for convenience when going through the disk image.

![image](https://user-images.githubusercontent.com/91398631/232165674-2df952c3-d0ca-40e9-9e4c-edf90f648190.png)

# Findings

First thing I found is browsing history where it seems they are looking up some different types of encoding. This might be useful later.

![image](https://user-images.githubusercontent.com/91398631/232166533-ee6cc922-6b72-43a2-b7ce-4c3e50f1a85f.png)

In the gallery there are 4 different .bmp images.

![image](https://user-images.githubusercontent.com/91398631/232166639-7eec6391-6e61-4f77-8cb2-f7be7b0ed906.png)

Now looking at the irclogs of which there are many but the first one I saw was in this path ```/3/home/yone/irclogs/01/04/#avidreader13.log```.

This contains some information that related to the .bmp images that was just found earlier.

Key Points of the avidreader13.log:

* [08:15] <yone786\> First it’s steghide.
* [08:15] <yone786\> Use password: akalibardzyratrundle
* [08:18] <yone786> The next is the encryption. Use openssl, AES, cbc.
* [08:19] <yone786> salt=0f3fa17eeacd53a9 key=58593a7522257f2a95cce9a68886ff78546784ad7db4473dbd91aecd9eefd508 iv=7a12fd4dc1898efcd997a1b9496e7591

This log gave the method of hiding the message in the images, steganography (with steghide), and gives the password to extract the data. Once the data is extracted Yone even gives the salt, key, and iv to decrypt with openssl. Even tells us what tools to use.
  
Now I went back to the .bmp files and downdloaded all 4 different bmp images in the gallery:
  
* /3/home/yone/gallery/1.bmp
* /3/home/yone/gallery/2.bmp
* /3/home/yone/gallery/3.bmp
* /3/home/yone/gallery/7.bmp

I clicked each image, then clicked export. This downdloaded the files to the /Downloads folder.

![image](https://user-images.githubusercontent.com/91398631/232168502-94b31610-5c52-4f92-a4bc-59ee218120d4.png)
  
Now I would open up another terminal to analyse these images. I then navigated to the downloads folder and moved all of the files to my working directory for this challenge. You could just keep it in the downdloads if you wanted to.
  
```mv vol4-3.home.yone.gallery.[1237].bmp (../[filepath])```

I then navigated back to my working directory and ran steghide with the provided password on each of the images. Ran each command separately.
  
```
steghide extract -sf vol4-3.home.yone.gallery.1.bmp -p akalibardzyratrundle
steghide extract -sf vol4-3.home.yone.gallery.2.bmp -p akalibardzyratrundle
steghide extract -sf vol4-3.home.yone.gallery.3.bmp -p akalibardzyratrundle
steghide extract -sf vol4-3.home.yone.gallery.7.bmp -p akalibardzyratrundle
```

The only one this command didn't work on was ```vol4-3.home.yone.gallery.7.bmp```, but there might be a way to get something from this later.
  
"frankenstein.txt.enc", "dracula.txt.enc", and "les-mis.txt.enc" were the extracted files. When you run the ```file``` command you see that it is just data and if you cat it out you see the same. So now I used openssl to decrypt these files with the provided salt, key, and iv from the logs.
  
```salt=0f3fa17eeacd53a9 key=58593a7522257f2a95cce9a68886ff78546784ad7db4473dbd91aecd9eefd508 iv=7a12fd4dc1898efcd997a1b9496e7591```
  
Also it is good to note that in the irclogs it also mentioned aes, cbc. which is useful when trying to create the openssl command to decrypt these files.
  
These are the openssl commands I ran:
  
* ```openssl enc -aes-256-cbc -d -S 0f3fa17eeacd53a9 -K 58593a7522257f2a95cce9a68886ff78546784ad7db4473dbd91aecd9eefd508 -iv 7a12fd4dc1898efcd997a1b9496e7591 -in frankenstein.txt.enc -out frankenstein.txt```
* ```openssl enc -aes-256-cbc -d -S 0f3fa17eeacd53a9 -K 58593a7522257f2a95cce9a68886ff78546784ad7db4473dbd91aecd9eefd508 -iv 7a12fd4dc1898efcd997a1b9496e7591 -in dracula.txt.enc -out dracula.txt```
* ```openssl enc -aes-256-cbc -d -S 0f3fa17eeacd53a9 -K 58593a7522257f2a95cce9a68886ff78546784ad7db4473dbd91aecd9eefd508 -iv 7a12fd4dc1898efcd997a1b9496e7591 -in les-mis.txt.enc -out les-mis.txt```
  
Tried to grep different things and then I also looked through these files and didn't find anything of use.
  
Now back to looking through the disk image to see if anything else could be found. vol4-3.home.yone.gallery.7.bmp wasn't able to be extracted so hopefully something could be found to help with that.
  
I continued looking through the irc logs and found nothing much other than they really like league of legends. There are many (5) league of legends logs.
  
There was an email in Maildir which only said to delete all of your emails and scrub your trash.
  
Next was the notes which there were 3 files (1.txt, 2.txt, and 3.txt):
  
* 1.txt: chizazerite
* 2.txt: guldulheen
* 3.txt: I keep forgetting this, but it starts like: yasuoaatrox...
  
3.txt is the one that looks most interesting because of the "..." and text before it implying there is something more and this is potentially a password. Up until now the only password that is needed is one to extract vol4-3.home.yone.gallery.7.bmp with steghide. So far there isn't much to do other than keep looking.
  
I then looked aroung a lot, and got stuck on many red herrings. To spare going through all of that here, just going to "Keyword Search" and then from earlier from the irclogs I know that Yone's username is yone786, so I just did a search for "yone786@" in hopes to get all of Yone's mail. This worked.
  
There was an interesting email chain (Not allocated, so deleted email) between yone786@gmail.com (Sten Walker) and azerite17@gmail.com (Bob Bobberson). Here is an image of that email chain: 
  
![image](https://user-images.githubusercontent.com/91398631/232172772-ef13fa0e-fbfd-4d1b-a0a8-16cf23e820f6.png)

This email contains mutliple important messages:
  
* Mentioning adopting something for there most important passwords
* Link to philosophy of passwords ```https://xkcd.com/936/```
* Bob Bobberson's adapation is using unique words from his favorite game, World of Warcraft
  
The second I saw the adapatation of his favorite game, for Yone I knew that would be Leagure of Legends based on the irclogs. Additionally, the link basically says to create a password use 4 strong words.
  
Looking back at the start of the password from the other text file "yasuoaatrox" you can see something interesting when comparing it agaisnt league of legends. I found that there is a League of Legend Champion named "Yasuo" and "Aatrox". This means that to finish this password there are probably another 2 Leagure of legends champions at the end of this password.
  
Now just need to make a wordlist of all possible possibilities for this password.

To do so I initially got a list of League of Legends Champions (found online) and put it into a text file (I put that text file under the UnforgottenBits folder in github). I also made sure to convert all the champions to be entirely lowercase.
  
I then created this python script:
  
```
#!/usr/bin/env python3

arr = open('leagueOfLegendsChampions.txt', 'r').readlines()

with open('output.txt', 'w') as file:
	for i in range(len(arr)):
		for j in range(len(arr)):
			file.write('yasuoaatrox' + arr[i].strip() + arr[j].strip() + '\n')
```

After running it creates a wordlist called "output.txt".
  
I then tried to use stegcracker with this wordlist.
  
```stegcracker vol4-3.home.yone.gallery.7.bmp output.txt```
  
It tried 1259 passwords before getting to "yasuoaatroxashecassiopeia" and successfully cracking the bmp image. The output file is called "vol4-3.home.yone.gallery.7.bmp.out".
  
Like the others this is data. I tried using the same openssl command with this one to no avail. 
	
This took a while for me to realise, but looking at the slack space of the txt files in yone/notes shows something promising. I thought of this because of the title of the challenge "unforgotten bits". 

To check the slack space I only knew how to do this in the windows version of autopsy (I'm sure there's a way to do it in linux, but it's easier to do it in windows for me because I already know how). So I downdloaded the file again from picoctf then used 7zip to extract the disk image. Then I uploaded it to autopsy using a very similar process.
	
![image](https://user-images.githubusercontent.com/91398631/232177032-b395912e-dccd-4028-a66f-e2aa750221c4.png)
	
Be sure to click the settings button.
	
![image](https://user-images.githubusercontent.com/91398631/232177049-885a32ff-92e7-44f4-9346-320396d780df.png)

And under the "Hide slack files in the:" section uncheck both boxes.
	
I first checked 3.txt-slack because that's where the start of the password was, but it ended up being in 1.txt-slack. This was obvious because it was the only one with data. Also it looked like something that might be encoded data.
	
![image](https://user-images.githubusercontent.com/91398631/232177152-4799156a-eec7-4e4c-8f5b-abd57c0081c0.png)

When looking back at what was found earlier in the browsing history we seen multiple different searches about encoding:

```
www.google.com
https://www.google.com/search?q=number+encodings
https://en.wikipedia.org/wiki/Church_encoding
https://cs.lmu.edu/~ray/notes/numenc/
https://www.wikiwand.com/en/Golden_ratio_base
```
	
When browsing these sites the Golden_ratio_base looks most similar to what was found in the slack space of 1.txt-slack.

Then I just ran a python script to decode the data from the slack space using golden ratio base and got the salt, key, and iv to decode with openssl.	

This is the final openssl command to decrypt vol4-3.home.yone.gallery.7.bmp.out
	
```openssl enc -aes-256-cbc -d -S 2350e88cbeaf16c9 -K a9f86b874bd927057a05408d274ee3a88a83ad972217b81fdc2bb8e8ca8736da -iv 908458e48fc8db1c5a46f18f0feb119f -in vol4-3.home.yone.gallery.7.bmp.out -out finallyReleased.txt```
	
Then if you just output the files with the "cat" command you can see the flag.
	
```cat finallyReleased.txt```
	
If you want only the flag and nothing else, here is a command for that:
	
```cat finallyReleased.txt | grep "picoCTF{" | tr -d " "```

Flag: ```picoCTF{f473_53413d_de...}```
