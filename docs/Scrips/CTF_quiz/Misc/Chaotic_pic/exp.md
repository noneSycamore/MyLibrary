# exp
```python
from PIL import Image
k1, k2 = 3.5606267076894413, 3.9101741242346346
k = [106, 80, 198, 220, 47, 18, 19, 230, 42, 202, 207, 196, 214, 132, 188, 190]
alpha = 2
sum, r = 0, 1
for i in range(16):
    sum += k[i]
    r ^= k[i]
a_1 = (sum/256) % 1
timea1 = 3 + int(1000 * a_1) % 30
b_1 = (r/256)	
timeb1 = 3 + int(1000 * b_1) % 30
xc_1 = a_1 * b_1
yc_1 = (a_1 + b_1) % 1

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

def from_pic(picture):
    img = Image.open(picture)
    w,h=img.size
    pic = []
    for i in range(w):
        for j in range(h):
            (r, g, b) = img.getpixel((i,j))
            pic.append(r)
            pic.append(g)
            pic.append(b)
    return pic, (w,h)

def decrypt():
    m, miu, omiga = [], [], []
    ta = timea1
    tb = timeb1
    c, (w,h) = from_pic('pic.png')
    for ci in c:
        miu.append(LC((k1, k2), a_1, ta, 1))
        omiga.append(LC((k1, k2), b_1, tb, 0))
        m.append((ci ^ (int(miu[-1] * 1000) + int(omiga[-1] * 1000)))%256)
        delta = ci/256
        for i in range(3):
            y = (yc_1 + delta) % 1
            y = k1 * y**3 + (1 - k1) * y
            x = xc_1
            x = k2 * x**3 + (1 - k2) * x
        ta = 3 + int(1000 * x) % 30
        tb = 3 + int(1000 * y) % 30
    k = 0
    img = Image.new('RGB', (w,h))
    for i in range(w):
        for j in range(h):
            img.putpixel((i,j), (m[k], m[k+1], m[k+2]))
            k += 3
    img.save('1.png')
decrypt()

```