# secret
```python
import string
import secrets
import re
alphabet = string.ascii_lowercase + string.digits
password = ''.join(secrets.choice(alphabet) for i in range(32))
st2 = re.findall(r'.{8}', password)
flag = 'flag{' + ('-'.join(s for s in st2)) + '}'
# print(flag)
```