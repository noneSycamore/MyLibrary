# exp
```python
from randcrack import RandCrack
from Crypto.Cipher import AES
from binascii import a2b_hex
from libnum import s2n
rc = RandCrack()

f = open("msg.txt", "r")
old_key = b'73E5602B54FE63A5'
old_iv = b'B435AE462FBAA662'
clist = f.readlines()
c = b'c82dc20b7512d03f1a0982eb8a6e855db20f6fe3ff8d202a6fb74c6522fa6e623c6abe6725cafe78f9624ad59f3e90af6f985f38f75ec4d62ff7e02bd7c2f051'

def decrypt(text, key, iv):
	mode = AES.MODE_CBC
	cryptos = AES.new(key, mode, iv)
	plain_text = cryptos.decrypt(text)
	return plain_text

for old_c in clist:
	m = decrypt(a2b_hex(old_c.strip('\n')), old_key, old_iv)
	m = m.replace(b'\0', b'')
	r = bin(int(m, 16))[2:].zfill(96)
	r1 = r[:32]
	r2 = r[32:64]
	r3 = r[64:]
	rc.submit(int(r2, 2))
	rc.submit(int(r1, 2))
	rc.submit(int(r3, 2))

salt = "{:X}".format(rc.predict_getrandbits(32)).encode('utf-8')
key = "{:X}".format(rc.predict_getrandbits(64)).encode('utf-8')
iv = "{:X}".format(rc.predict_getrandbits(64)).encode('utf-8')
flag = decrypt(a2b_hex(c), key, iv).replace(b'\0', b'')
print(flag)
```