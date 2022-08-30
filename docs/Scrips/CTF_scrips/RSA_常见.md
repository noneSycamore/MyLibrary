# RSA_常见
```python
#coding:utf-8
import gmpy2,libnum
from Crypto.PublicKey import RSA
from Crypto.Util.number import bytes_to_long
def egcd(a,b):
    if a==0:
        return(b,0,1)
    else:
        g,y,x=egcd(b%a,a)
    return(g,x-(b // a)*y,y)

def extended_gcd(a, b):
    x,y = 0, 1
    lastx, lasty = 1, 0
    while b:
        a, (q, b) = b, divmod(a,b)
        x, lastx = lastx-q*x, x
        y, lasty = lasty-q*y, y
    return (lastx, lasty, a)

def CRT(items):#中国剩余定理
    N = 1
    for a, n in items:
        N *= n
    result = 0
    for a, n in items:
        m = N//n
        r, s, d = extended_gcd(n, m)
        if d != 1:
            N=N//n
            continue
        result += a*s*m
    return result % N, N

def p_q_e():
    p=int(input("p="))
    q=int(input("q="))
    e=int(input("e="))
    c=int(input("c="))
    phi=(p-1)*(q-1)
    n=p*q
    d=gmpy2.invert(e,phi)
    m=pow(c,d,n)
    print("明文：",libnum.n2s(m))

def Common_Modulus():
    n=int(input("n=")) 
    e1=int(input("e1=")) 
    c1=int(input("c1=")) 
    e2=int(input("e2=")) 
    c2=int(input("c2="))

    s=egcd(e1,e2)
    s1=s[1]
    s2=s[2]
    # 求模反元素
    if s1<0:
        s1 = - s1
        c1 = gmpy2.invert(c1,n)
    elif s2<0:
        s2 = - s2
        c2 = gmpy2.invert(c2,n)

    m = pow(c1,s1,n)*pow(c2,s2,n)%n
    print("明文：",libnum.n2s(m))

def Small_plaintext_e3():
    e=int(input("e="))
    n=int(input("n="))
    c=int(input("c="))
    for k in range(200000000):
        if gmpy2.iroot(c + n * k, e)[1] == 1:
            m=gmpy2.iroot(c + n * k, e)[0]
            print("明文：",libnum.n2s(m))
            break

def n_e_dp():
    n=int(input("n="))
    e=int(input("e="))
    dp=int(input("dp="))
    c=int(input("c="))
    for i in range(1,65538):
        if (dp*e-1)%i == 0:
            if n%(((dp*e-1)//i)+1)==0:
                p=((dp*e-1)//i)+1
                q=n//p
                phi = (p-1)*(q-1)
                d = gmpy2.invert(e,phi)%phi
                print(libnum.n2s(pow(c,d,n)))
def N2_equal_P():
    n1=int(input("n1="))
    n2=int(input("n2="))
    e1=int(input("e1="))
    e2=int(input("e2="))
    c1=int(input("c1="))
    c2=int(input("c2="))
    p=gmpy2.gcd(n1,n2)
    #print(p)
    q1=n1//p
    q2=n2//p    
    phi_1=(p-1)*(q1-1)
    phi_2=(p-1)*(q2-1)
    d1=gmpy2.invert(e1,phi_1)
    d2=gmpy2.invert(e2,phi_2)
    print("m1：",libnum.n2s(pow(c1,d1,n1)))
    print("m2：",libnum.n2s(pow(c2,d2,n2)))

def Prime_3():
    p=int(input("p="))
    q=int(input("q="))
    r=int(input("r="))
    e=int(input("e="))
    c=int(input("c="))
    s=(p-1)*(q-1)*(r-1)
    d=(gmpy2.invert(e, s))
    n=p*q*r
    m=pow(c,d,n)
    print("明文：",libnum.n2s(m))

def RSA_File():
    public_name = input("请输入公钥文件名(没有直接回车)：")
    flag_name = input("请输入加密文件名：")
    private_name = input("请输入私钥文件名(没有直接回车)：")
    with open(flag_name,'rb') as f:
        c = bytes_to_long(f.read())
    if private_name=="":
        pass
    else:
        with open(private_name,'r') as private:
            Key = RSA.importKey(private.read())
            n,e,d,p,q=Key.n,Key.e,Key.d,Key.p,Key.q
            m=pow(c,d,n)
            print("明文：",libnum.n2s(m))
            return
    with open(public_name,'r') as public:
        key = RSA.importKey(public.read())
        n, e = key.n, key.e
    
    print("n=",n)
    print("e=",e)
    print("c=",c)
    
def next_prime():
    n=int(input("n="))
    e=int(input("e="))
    c=int(input("c="))
    i = gmpy2.isqrt(n)
    p, q = 0, 0
    while True:
        if n - (i * (n // i)) == 0:
            p = i
            q = n//i
            break
        i += 1
    phi=(p-1)*(q-1)
    d=gmpy2.invert(e,phi)
    m=pow(c,d,n)
    print("明文：",libnum.n2s(m))

def Broadcast():
    print('n,e,c由文件导入，请确保格式为[{"c": , "e": , "n":}]')
    print("不同组用逗号隔开，如[{},{}]")
    file_name=input("请输入文件名：")
    with open(file_name,'r') as f:
        f=f.read()
    sessions=eval(f)
    data = []
    for session in sessions:
        e=session['e']
        n=session['n']
        msg=session['c']
        data = data + [(msg, n)]
    print("Please wait, performing CRT")
    x, n = CRT(data)
    e=session['e']
    m=gmpy2.iroot(x,e)[0]
    print("明文：",libnum.n2s(m))

if __name__=="__main__":
    print("1.已知p,q,e")
    print("2.共模攻击")
    print("3.小明文攻击，e一般为3")
    print("4.已知n,e,dp")
    print("5.模不互素，求出共因子p")
    print("6.三个素数的RSA")
    print("7.读取RSA公钥文件，私钥文件和密文")
    print("8.p,q相近")
    print("9.低加密指数广播攻击")
    x=input("请选择解密方法：")
    
    if x=='1':
        p_q_e()
    if x=='2':
        Common_Modulus()
    if x=='3':
        Small_plaintext_e3()
    if x=='4':
        n_e_dp()
    if x=='5':
        N2_equal_P()
    if x=='6':
        Prime_3()
    if x=='7':
        RSA_File()
    if x=='8':
        next_prime()
    if x=='9':
        Broadcast()

```