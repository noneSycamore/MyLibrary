# Library_readin
```python
import os
path = "docs"
files = os.listdir(path)
str = ''
for file in files:
	if '.' in file or file == 'images':
		continue
	else:
		str += '    - ' + file + ':\n'
		files2 = os.listdir(path+'/'+file)
		str += '        - ' + file+'/'+'Starting.md' + '\n'

		for file2 in files2:
			if '.' in file2 and file2 != 'Starting.md':
				str += '        - ' + file+'/'+file2 + '\n'
			elif file2 != 'Starting.md':
				str += '        - ' + file2 + ':\n'
				files3 = os.listdir(path+'/'+file+'/'+file2)
				for file3 in files3:
					str += '            - ' + file+'/'+file2+'/'+file3 + '\n'

print(str)
f = open("mkdocs.yml", 'r+', encoding="utf-8")
line = f.readline()
while line:
	if 'index.md' in line:
		pos = f.tell()
		break
	line = f.readline()
f.seek(pos, 0)
f.write(str)   
f.close()  

```