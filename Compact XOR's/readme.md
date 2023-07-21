# Compact XOR's
![image](https://github.com/0xd1sc0/AmateursCTF-2023/assets/117750351/372378cf-ba75-4e82-9043-88a9a4ba098d)

content in the given file fleg  <br>
###### fhex = '610c6115651072014317463d73127613732c73036102653a6217742b701c61086e1a651d742b69075f2f6c0d69075f2c690e681c5f673604650364023944' <br>
ct = bytes.fromhex(fhex) returns b'a\x0ca\x15e\x10r\x01C\x17F=s\x12v\x13s,s\x03a\x02e:b\x17t+p\x1ca\x08n\x1ae\x1dt+i\x07_/l\ri\x07_,i\x0eh\x1c_g6\x04e\x03d\x029D'
In the starting when you notice you see that
alternate characters of the flag are exposed at the sart. So after a bit of trial and error I figured out that the even bytes are exposed and odd bytes are xored with the next byte .
Also we know that the flag format is `amateursCTF{`  

## solve script 
```py
from pwn import xor
with open('/home/disco/Desktop/bi0s /ctfs/amateurs ctf 23/fleg', 'r') as fleg:
    fhex = fleg.read()
ct = bytes.fromhex(fhex)
x = 'amateurCTF{'
print(ct)
flag = ''
for i in range(len(ct)):
    if i % 2 == 0:
        flag += chr(ct[i])
    else:
        flag += chr(ct[i]^ct[i-1]) 

print(flag)
```
`amateursCTF{saves_space_but_plaintext_in_plain_sight_862efdf9}`
