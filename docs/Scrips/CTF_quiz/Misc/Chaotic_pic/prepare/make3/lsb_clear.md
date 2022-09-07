# lsb_clear
```python
from PIL import Image
im = Image.open("zaiti.png")
width = im.size[0]
height = im.size[1]
for h in range(0, height):
	for w in range(0, width):
		pixel = im.getpixel((w, h))
		a = pixel[0]      # R
		b = pixel[1]      # G
		c = pixel[2]      # B
		if ((a % 2) != 0) or ((b % 2) != 0) or ((c % 2) != 0):
			a = a - (a % 2)
			b = b - (b % 2)
			c = c - (c % 2)
		im.putpixel((w, h), (a, b, c))
im.save("zaiti_clean.png")
```