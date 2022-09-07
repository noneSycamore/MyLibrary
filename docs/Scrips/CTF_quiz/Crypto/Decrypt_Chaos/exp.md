# exp
```python
k1, k2 = 3.656308509451218, 3.835783526337498
k = [194, 102, 123, 240, 64, 71, 229, 95, 77, 80, 116, 246, 102, 26, 130, 169]
c = [7, 255, 171, 143, 96, 91, 78, 40, 79, 18, 148, 81, 10, 226, 204, 238, 128, 135, 83, 221]
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

def LC(x, times, flags):
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

def decrypt(c):
	m, miu, omiga = [], [], []
	ta = timea1
	tb = timeb1
	for ci in c:
		miu.append(LC(a_1, ta, 1))
		omiga.append(LC(b_1, tb, 0))
		m.append(chr(((ci ^ (int(miu[-1] * 1000) + int(omiga[-1] * 1000))) % 256)))
		delta = ci/256
		for i in range(3):
			y = (yc_1 + delta) % 1
			y = k1 * y**3 + (1 - k1) * y
			x = xc_1
			x = k2 * x**3 + (1 - k2) * x
		ta = 3 + int(1000 * x) % 30
		tb = 3 + int(1000 * y) % 30
	print(''.join(m))

decrypt(c)

```