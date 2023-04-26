# Description

There's an interesting script in the user's home directory.

The work computer is running SSH. We've been given a script which performs some basic calculations, explore the script and find a flag.

Hostname: saturn.picoctf.net
Port:     64713
Username: picoplayer
Password: password

# Solution

```ssh picoplayer@saturn.picoctf.net -p 64713```

Then enter ```password``` as the password. You can use control+shift+v to paste it into the feild. 

```ls```

```./useless```

```
Outputs:
Read the code first
```

```cat useless```

```
Outputs:
#!/bin/bash
# Basic mathematical operations via command-line arguments

if [ $# != 3 ]
then
  echo "Read the code first"
else
        if [[ "$1" == "add" ]]
        then 
          sum=$(( $2 + $3 ))
          echo "The Sum is: $sum"  

        elif [[ "$1" == "sub" ]]
        then 
          sub=$(( $2 - $3 ))
          echo "The Substract is: $sub" 

        elif [[ "$1" == "div" ]]
        then 
          div=$(( $2 / $3 ))
          echo "The quotient is: $div" 

        elif [[ "$1" == "mul" ]]
        then
          mul=$(( $2 * $3 ))
          echo "The product is: $mul" 

        else
          echo "Read the manual"
         
        fi
fi
```

```man useless```

At the end of the manual there is the flag.

Flag: ```picoCTF{us3l3s...it3d_4373}```
