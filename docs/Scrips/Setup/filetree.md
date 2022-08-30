# filetree
```python
import os

path = "docs"
files = os.listdir(path)
File = []
s = ""
for file in files:
    if "." in file and file != "index.md":
        File.append(file)
    elif "." not in file and file != "images":
        os.system("cd docs && tree " + file + "> ../1.txt")
        f = open("1.txt", 'r')
        str = f.read()
        limit = str.find("directories") - 2
        s += str[:limit]

for f1 in File:
    s += f1 + "\n\n"
print(s)
os.system("rm 1.txt")
s = "```\n" + s[:-1] + "```\n"
f = open("docs/index.md", "r+", encoding="utf-8")
content = f.read()
i = content.find("Tree:\n") + 6
j = content.find("\n## Every time")
content = content[:i] + "\n" + s + content[j:]
f.close()
fw = open("docs/index.md", 'w+', encoding="utf-8")
fw.write(content)
fw.close()

```