# Description

You will find the flag after analysing this apk
Download here.

# Solution

```wget https://artifacts.picoctf.net/c/449/timer.apk```

First I downloaded jadx. You can also use mobsf if you want.

Steps to install jadx:

**Installing Java:**

```
sudo apt install default-jre
sudo apt install default-jdk
```

**Installing Git:**

```sudo apt install git```

**Installing JADX:**

```
git clone https://github.com/skylot/jadx.git
cd jadx
./gradlew dist
alias jadx-gui=’~/<directoryName>/jadx/build/jadx/bin/jadx-gui’
cd ..
```

**Using JADX:**

```jadx-gui timer.apk```

That command starts jadx. Once it is started you go to file then open where you open timer.apk at the file location. Then you go to navigation then search. I put "pico" to start and saw the flag at the start of my search. You could also do "picoCTF{" in the search to have it give less results.

Flag: ```picoCTF{t1m3r_r3...496}```
  
---
  
For installing JADX I used this guide:

[Resource used](https://www.secplicity.org/2019/10/04/android-apk-reverse-engineering-using-jadx/)
