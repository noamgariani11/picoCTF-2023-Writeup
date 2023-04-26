# Description

Someone might have hidden the password in the trace file.

Find the key to unlock this file. This tracefile might be good to analyze.

# Solution

I initially opened the wireshark file and saw some interesting strings in some of the packets. From there I decided just to run strings on the pcap file.

```strings dump.pcap```

This gave many results but notably:

iBwaWNvQ1RGe1 Could the flag have been splitted?

AABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8=

PBwaWUvQ1RGesabababkjaASKBKSBACVVAVSDDSSSSDSKJBJS

PBwaWUvQ1RGe1 Maybe try checking the other file

From here I tried to decode these strings in basae64 together. This did not work as I always seemingly got part of the flag. ```picoCTF{R34DING_LOKd_```

I decoding something similiar to this string: 
PBwaWUvQ1RGesabababkjaASKBKSBACVVAVSDDSSSSDSKJBJSiBwaWNvQ1RGe1AABBHHPJGTFRLKVGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8

Although you could just use VGhpcyBpcyB0aGUgc2VjcmV0OiBwaWNvQ1RGe1IzNERJTkdfTE9LZF8= to get the partial flag.

Based on the last string "Maybe try checking the other file", I looked back at the zip file. This is because both a pcap and a locked zip file was given. If you use the partial flag as the password for the zip file that it extracts and you are given a flag file.

Flag: ```picoCTF{R34DING_LOKd_fil56...9b}```
