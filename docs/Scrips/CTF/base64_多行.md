# base64_多行
```python
import base64

def base64stego_decrypt(lines):
    base64char = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"     #Base64字符集 已按照规范排列
    bintext = ""
    for line in lines:
        if line.find("==") > 0:
            tmp = bin(base64char.find(line[-3]) & 15)[2:]
            bintext = bintext+"0"*(4-len(tmp))+tmp
        elif line.find("=") > 0:
            tmp = bin(base64char.find(line[-2]) & 3)[2:]
            bintext = bintext+"0"*(2-len(tmp))+tmp
    text = ""
    if(len(bintext) % 8 != 0):
        print("error")
        for i in range(0, len(bintext), 8):
            if(i+8 > len(bintext)):
                text = text+"-"+bintext[i:]
                return text
            else:
                text = text+chr(int(bintext[i:i+8], 2))
    else:
        for i in range(0, len(bintext), 8):
            text = text+chr(int(bintext[i:i+8], 2))
        return text
def base64string_decrypt(text):
    try:
        detext = str(text).encode("utf-8")
        detext = base64.b64decode(detext)
        detext = detext.decode("utf-8")
    except:
        return 0
    return detext

if __name__ == "__main__":
    path = "flag.txt"
    file = open(path, "r")
    line = file.read().splitlines()
    print("显：", end="")
    for l in line:
        print(base64string_decrypt(l),end="")
    print()
    print("隐：", base64stego_decrypt(line))
```