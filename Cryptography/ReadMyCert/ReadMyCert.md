# Description

How about we take you on an adventure on exploring certificate signing requests

Take a look at this CSR file here.

# Solution

```wget https://artifacts.picoctf.net/c/422/readmycert.csr```

Then I did ```cat readmycert.csr``` which gave:

-----BEGIN CERTIFICATE REQUEST-----
MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF8zNzNi
NGFiMH0xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAKr+AToJg/TVTvfd9XzYR0gC5TOXa2+T24gjE8n7SHqynuo0Zlfy
oCqZHkxLha4QZszow4M+klP9fe1hy90LAU2enQGELrF3OF5SbNIVnPq97qrSHNI7
D9faAdsBqvezCto1MuMrRD35gwhQPga3WobkMdbJdDwuBpem/Tl3ko3Y9sxq2nAF
cmMNPj40GLtCfW55O8Awn2uN5gGZe+Nw2ArU9AYFidPtFZjBovHv7BVJz5XlhRhu
oiBALZES9kgfOyiwZrcJYZCJh9cJz3d+n2roMyAYMM/VZIjl0aZqSdOPeGYzs3GP
p/jFku8KNBn+mjyyw0H1vRnrK1hkNKXrXOcCAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAG0c6ed5
a5zHU5IeI1KBvhGa+zGlrbm4lGQnGoI8wwlr6VN6v07/BGpwWfhjJatAOQ3txT5O
xDrM5A8caxpgGUXmat+C/9XCSQgRA+JckSk3rd6Wz7rYRuKsnycHzVIwyvIgSdjM
5/RKRdYHyFqYHPo9Tf1fThbV0tyQ+kr0tmsO6ZuaKgyDSxtky4U51XzSByKygHOT
Oi+VkzWvn74aOgbelBFMz+3vxaRHW85pe93jN6Gvc+HwYzUFja/SZXaN95sNRhcq
20SbOmg4r2pHUg0Lfs/0EHqDSg6JtKItqZmQUNhUQ7jmL6PtUpQQlkwlfMmEijRn
vlIEqBAkSbo63XQ=
-----END CERTIFICATE REQUEST-----

Because of the '=' at the end it makes me think this might just be base64. 

echo "MIICpzCCAY8CAQAwPDEmMCQGA1UEAwwdcGljb0NURntyZWFkX215Y2VydF8zNzNi
NGFiMH0xEjAQBgNVBCkMCWN0ZlBsYXllcjCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAKr+AToJg/TVTvfd9XzYR0gC5TOXa2+T24gjE8n7SHqynuo0Zlfy
oCqZHkxLha4QZszow4M+klP9fe1hy90LAU2enQGELrF3OF5SbNIVnPq97qrSHNI7
D9faAdsBqvezCto1MuMrRD35gwhQPga3WobkMdbJdDwuBpem/Tl3ko3Y9sxq2nAF
cmMNPj40GLtCfW55O8Awn2uN5gGZe+Nw2ArU9AYFidPtFZjBovHv7BVJz5XlhRhu
oiBALZES9kgfOyiwZrcJYZCJh9cJz3d+n2roMyAYMM/VZIjl0aZqSdOPeGYzs3GP
p/jFku8KNBn+mjyyw0H1vRnrK1hkNKXrXOcCAwEAAaAmMCQGCSqGSIb3DQEJDjEX
MBUwEwYDVR0lBAwwCgYIKwYBBQUHAwIwDQYJKoZIhvcNAQELBQADggEBAG0c6ed5
a5zHU5IeI1KBvhGa+zGlrbm4lGQnGoI8wwlr6VN6v07/BGpwWfhjJatAOQ3txT5O
xDrM5A8caxpgGUXmat+C/9XCSQgRA+JckSk3rd6Wz7rYRuKsnycHzVIwyvIgSdjM
5/RKRdYHyFqYHPo9Tf1fThbV0tyQ+kr0tmsO6ZuaKgyDSxtky4U51XzSByKygHOT
Oi+VkzWvn74aOgbelBFMz+3vxaRHW85pe93jN6Gvc+HwYzUFja/SZXaN95sNRhcq
20SbOmg4r2pHUg0Lfs/0EHqDSg6JtKItqZmQUNhUQ7jmL6PtUpQQlkwlfMmEijRn
vlIEqBAkSbo63XQ=
" | base64 --decode 

You can also just put this in [Cyberchef](https://gchq.github.io/CyberChef/) and it will have same effect.

Near the top of the output there is the flag.

Flag: ```picoCTF{read_mycert...b0}```
