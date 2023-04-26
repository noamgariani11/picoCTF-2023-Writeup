# Description

Every file gets a flag.
The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye here.

# Solution

```wget https://artifacts.picoctf.net/c/260/flag.png```

```binwalk flag.png```

| DECIMAL |       HEXADECIMAL  |   DESCRIPTION |
| :-------------: |:-------------:| :-----:|
| 0     |        0x0       |      PNG image, 512 x 504, 8-bit/color RGBA, non-interlaced |
| 41      |      0x29      |      Zlib compressed data, compressed |
| 39739    |     0x9B3B    |      Zip archive data, at least v1.0 to extract, name: secret/ |
| 39804    |     0x9B7C    |      Zip archive data, at least v2.0 to extract, compressed size: 2944, uncompressed size: 3095, name: secret/flag.png |
|42983      |   0xA7E7      |    End of Zip archive, footer length: 22 |

```unzip flag.png```

(you could also use ```binwalk -e flag.png```)

```cd secret```

```eog flag.png```

The flag is the image

Flag: ```picoCTF{Hiddinng_An_i...678a337}```

