# chaos
```python
import random
from PIL import Image

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
    # k1 = random.uniform(3.2, 4)
    # k2 = random.uniform(3.2, 4)
    k1, k2 = 3.5606267076894413, 3.9101741242346346
    k = [106, 80, 198, 220, 47, 18, 19, 230, 42, 202, 207, 196, 214, 132, 188, 190]
    for i in range(16):
        # ran = random.randint(1,256)
        # if i == 0 or abs(ran-k[-1]) > 10:
            # k.append(ran)
        sum += k[i]
        r ^= k[i]
        # else:
        #     i -= 1
    a_1 = (sum/256) % 1
    timea1 = 3 + int(1000 * a_1) % 30
    b_1 = (r/256)
    timeb1 = 3 + int(1000 * b_1) % 30
    xc_1 = a_1 * b_1
    yc_1 = (a_1 + b_1) % 1
    print('k1, k2 = %r, %r'%(k1, k2))
    print('k = %r'%k)
    return (k1, k2), (a_1, timea1, b_1, timeb1, xc_1, yc_1)

def from_pic():
    img = Image.open('1_LSB.png')
    w,h=img.size
    pic = []
    for i in range(w):
        for j in range(h):
            (r, g, b, a) = img.getpixel((i,j))
            pic.append(r)
            pic.append(g)
            pic.append(b)
    return pic, (w,h)

def get_ints(key, data):
    (k1, k2) = key
    (a_1, timea1, b_1, timeb1, xc_1, yc_1) = data
    flist, (w, h) = from_pic()
    c, miu, omiga = [], [], []
    ta, tb = timea1, timeb1
    for mi in flist:
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
    img = Image.new('RGB', (w, h))
    k = 0
    for i in range(w):
        for j in range(h):
            img.putpixel((i, j), (c[k], c[k+1], c[k+2]))
            k += 3
    img.save('pic.png')

if __name__=="__main__":
    key, data = init()
    get_ints(key, data)

```