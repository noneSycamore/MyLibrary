# exp
```python
k1, k2 = 3.748382978074769, 3.915306786433355               
k = [157, 148, 123, 252, 219, 186, 81, 147, 42, 6, 160, 68, 
73, 175, 150, 240]                                          
c = [193, 87, 75, 93, 131, 224, 92, 106, 85, 151, 93, 126, 203, 232, 101, 96, 41, 33, 32, 84, 100, 128, 23, 31, 118, 87, 29, 59, 77, 28, 36, 23, 45, 171, 38, 129, 94, 36, 100, 122, 104]
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

def LC(x, times):
	xn = []
	xn.append(x)
	xn.append(1 - alpha * xn[0]**2)
	for i in range(times):
		assert xn[i]>=-1 and xn[i]<=1 and xn[i+1]>=-1 and xn[i+1]<=1
		xn.append((1 - alpha * xn[i]**2)*(k1 * xn[i+1]**3 + (1 - k1)*xn[i+1]))
	return xn[times + 1]

def CL(x, times):
	xn = []
	xn.append(x)
	xn.append(k2 * xn[0]**3 + (1 - k2)*xn[0])
	for i in range(times):
		assert xn[i]>=-1 and xn[i]<=1 and xn[i+1]>=-1 and xn[i+1]<=1
		xn.append((k2 * xn[i]**3 + (1 - k2)*xn[i])*(1 - alpha * xn[i+1]**2))
	return xn[times + 1]

def decrypt(c):
	m, miu, omiga = [], [], []
	ta = timea1
	tb = timeb1
	for ci in c:
		miu.append(LC(a_1, ta))
		omiga.append(CL(b_1, tb))
		m.append(chr((ci - int(miu[-1] * 1000) - int(omiga[-1] * 1000)) % 256))
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