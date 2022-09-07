# chaos
```python
import random
import time
# from secret import flag
flag = 'flag{123vrthsdfhfgj}'
def LC(key, x, times, flags):
    (k1, k2) = key
    xn = []
    xn.append(x)
    if flags:
        xn.append(1 - 2 * xn[0]**2)
    else:
        xn.append(k2 * xn[0]**3 + (1 - k2)*xn[0])
    for i in range(times):
        assert xn[i]>=-1 and xn[i]<=1 and xn[i+1]>=-1 and xn[i+1]<=1
        if flags:
            xn.append((1 - 2 * xn[i]**2)*(k1 * xn[i+1]**3 + (1 - k1)*xn[i+1]))
        else:
            xn.append((k2 * xn[i]**3 + (1 - k2)*xn[i])*(1 - 2 * xn[i+1]**2))
    return xn[times + 1]

def init(): 
    sum, r, k = 0, 1, []
    k1 = random.uniform(3.2, 4) 
    k2 = random.uniform(3.2, 4)
    for i in range(16): 
        k.append(random.randint(1,256)) 
        sum += k[-1]
        r ^= k[-1]  
    a_1 = (sum/256) % 1 
    timea1 = 3 + int(1000 * a_1) % 30
    b_1 = (r/256)
    timeb1 = 3 + int(1000 * b_1) % 30
    xc_1 = a_1 * b_1
    yc_1 = (a_1 + b_1) % 1
    print('k1, k2 = %r, %r'%(k1, k2))
    print('k = %r'%k)
    return (k1, k2), (a_1, timea1, b_1, timeb1, xc_1, yc_1)

def encrypt(key, data, flag):
    (k1, k2) = key
    (a_1, timea1, b_1, timeb1, xc_1, yc_1) = data
    flag = list(flag)
    m, c = [], []
    miu, omiga = [], []
    ta = timea1
    tb = timeb1
    for tmp in flag:
        mi = ord(tmp)
        miu.append(LC(key, a_1, ta, 1))
        omiga.append(LC(key, b_1, tb, 0))
        c.append(((int(miu[-1] * 1000) + int(omiga[-1] * 1000)) ^ mi) % 256)
        delta = c[-1]/256
        for i in range(3):
            y = (yc_1 + delta) % 1
            y = k1 * y**3 + (1 - k1) * y
            x = xc_1
            x = k2 * x**3 + (1 - k2) * x
        ta = 3 + int(1000 * x) % 30
        tb = 3 + int(1000 * y) % 30
    print('c = %r'%(c))
    return c

if __name__=="__main__":
    # print(flag)
    key, data = init()
    c = encrypt(key, data, flag)

'''

'''

```