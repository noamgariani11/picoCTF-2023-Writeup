# Description

How about some hide and seek heh?

Download this file and find the flag.

# Solution

```wget https://artifacts.picoctf.net/c/371/trace.pcap```

Open trace.pcap in wireshark

If you go to the first TCP Retransmission then you will see the flag.

The way I went about solving this was I just clicked the starting TCP packet and followed the TCP stream. In the first TCP stream (1) you see this: ```username root    password toorc4e803f}```. If you click the malformed packet in that stream you will also see the flag.

Flag: ```picoCTF{P64P_4N...803f}```
