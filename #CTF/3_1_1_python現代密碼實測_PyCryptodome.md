## GOOGLE COLAB實作
```
!pip install pycryptodome
```

- [PyCryptodome](https://github.com/Legrandin/pycryptodome)


## AES加密
```python
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

data =b'falg(HappyCryptoDay)'
key = get_random_bytes(16)
cipher = AES.new(key, AES.MODE_EAX)
ciphertext, tag = cipher.encrypt_and_digest(data)

file_out = open("encrypted.bin", "wb")
[ file_out.write(x) for x in (cipher.nonce, tag, ciphertext) ]
file_out.close()
```
## AES解密
```
from Crypto.Cipher import AES

file_in = open("encrypted.bin", "rb")
nonce, tag, ciphertext = [ file_in.read(x) for x in (16, 16, -1) ]

# let's assume that the key is somehow available again
cipher = AES.new(key, AES.MODE_EAX, nonce)
data = cipher.decrypt_and_verify(ciphertext, tag)
```
