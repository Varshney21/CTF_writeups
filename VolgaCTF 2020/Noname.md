## CRYPTO Noname 

The Challenge gave two file `encryptor.py` and `encrypted`.

```
from Crypto.Cipher import AES
from secret import flag
import time
from hashlib import md5


key = md5(str(int(time.time()))).digest()
padding = 16 - len(flag) % 16
aes = AES.new(key, AES.MODE_ECB)
outData = aes.encrypt(flag + padding * hex(padding)[2:].decode('hex'))
print outData.encode('base64')
```
encryptor.py

```
uzF9t5fs3BC5MfPGe346gXrDmTIGGAIXJS88mZntUWoMn5fKYCxcVLmNjqwwHc2sCO3eFGGXY3cswMnO7OZXOw==
```
encrypted

From encrypted.py we get that the md5 hash of current time is the key for AES and ECB mode is used for encryption. So the base64 string in file encrypted is the base64 encoded Cipher of the flag, which we need.

We need the time at which the python file was executed or the encrypted file was created. So for that I used exiftool to get the metadata of the files I downloaded using wget because it doesnt overwrites the metadata ie the time of creation and etc.

But that value didnt worked.

![exif](https://i.imgur.com/7Ca3oMo.png?1)

There was a message in the Challenge : `I have Noname; I am but two days old.`

So I ran a brute force from 24/03/2020.

```
from Crypto.Cipher import AES
import time
from hashlib import md5

cipher = '''\xbb1}\xb7\x97\xec\xdc\x10\xb91\xf3\xc6{~:\x81z\xc3\x992\x06\x18\x02\x17%/<\x99\x99\xedQj\x0c\x9f\x97\xca`,\\T\xb9\x8d\x8e\xac0\x1d\xcd\xac\x08\xed\xde\x14a\x97cw,\xc0\xc9\xce\xec\xe6W;'''

t = (2020,03,24,0,0,0,2,84,-1)
i = int(time.mktime(t))
while(i>0):
    key = md5(str(i)).digest()
    aes = AES.new(key, AES.MODE_ECB)
    pt = aes.decrypt(cipher)
    if('CTF{' in pt):
		    print time.localtime(i)
		    print '>>>'            
		    print pt
		    print '\n\n'
    i=i+1
```
![flag](https://i.imgur.com/MZQkUEy.png?1)

