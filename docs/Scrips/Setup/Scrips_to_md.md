# Scrips_to_md
```python
import os

def findAllFile(base):
	for root, ds, fs in os.walk(base):
		for f in fs:
			fullname = os.path.join(root, f)
			yield fullname.replace('\\', '/')

def get_header(path):
	return path.split('/')[-1][:-3]

def transfer(path, type):
	f = open(path, 'r+', encoding="utf-8")
	content = f.read()
	content = '# ' + get_header(path) + '\n```' + type + '\n' +content + '\n```'
	f.close()
	fw = open(path, 'w+', encoding="utf-8")
	fw.write(content)
	fw.close()
	os.rename(path, path[:-2]+'md')


def main():
	base = 'docs/'
	for i in findAllFile(base):
		if i[-2:] == 'py':
			transfer(i, 'python')
		elif i[-2:] == 'sh':
			transfer(i, 'shell')

if __name__ == '__main__':
	main()
```