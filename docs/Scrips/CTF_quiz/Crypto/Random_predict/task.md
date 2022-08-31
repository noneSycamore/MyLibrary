# task
```python
from Crypto.Cipher import AES
from binascii import b2a_hex
from libnum import s2n
from random import *
from secret import flag

def add_to_16(text):
    if len(text.encode('utf-8')) % 16:
        add = 16 - (len(text.encode('utf-8')) % 16)
    else:
        add = 0
    text = text + ('\0' * add)
    return text.encode('utf-8')

def init():
    r1 = getrandbits(64)
    r2 = getrandbits(32)
    m = "{:X}".format(r1).encode('utf-8')
    salt = "{:X}".format(r2).encode('utf-8')
    m += salt
    return add_to_16(m.decode())
 
def encrypt(m, key, iv):
    mode = AES.MODE_CBC
    cryptos = AES.new(key, mode, iv)
    cipher_text = cryptos.encrypt(m)
    return cipher_text

def chall(key, iv):
    old_m = init()
    c = encrypt(old_m, key, iv)
    return b2a_hex(c)

if __name__=="__main__":
    f = open("msg.txt", 'w+')
    old_key = b'73E5602B54FE63A5'
    old_iv = b'B435AE462FBAA662'
    for i in range(208):
        old_c = chall(old_key, old_iv)
        f.write("{}\n".format(old_c.decode()))

    salt = "{:X}".format(getrandbits(32)).encode('utf-8')
    m = flag.encode() + salt
    key = "{:X}".format(getrandbits(64)).encode('utf-8')
    iv = "{:X}".format(getrandbits(64)).encode('utf-8')
    c = encrypt(add_to_16(m.decode()), key, iv)
    print("c = %r"%(b2a_hex(c)))

# c = b'c82dc20b7512d03f1a0982eb8a6e855db20f6fe3ff8d202a6fb74c6522fa6e623c6abe6725cafe78f9624ad59f3e90af6f985f38f75ec4d62ff7e02bd7c2f051'
```