# Caser_爆破
```python
model = "abcdefghijklmnopqrstuvwxyz"
model2 = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'

str1 = "AFFPGS{Unehxv_vf_AFF_FHCREZNA_fb_guvf_gnfx_vf_rnfl}"

for key in range(1,27):
    for s in str1:
        if s.islower():
            n = model.find(s)
            s = model[n-key]
        elif s.isupper():
            n = model2.find(s)
            s = model2[n-key]
        print(s, end='')
    print('')
```