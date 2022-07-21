# Basically RSA 

An easy crypto challenge too xD !

Hello Welcome to My write up about a cryptographie challenge that i've been played on BDsec CTF 2022 .

> First of all , let's take a view about the description : 

```
Basically RSA

RSA cryptosystem uses modular arithmetic to create an asymmetric encryption system. 
However, there are some pitfalls and weakness. Can you exploit it?

    N: 1280678415822214057864524798453297819181910621573945477544758171055968245116423923

    E: 65537

    C: 241757357533719849989659127349827982677055294256023833052829147857534659015212862
```

Cool , since we have The N factor , and the E , and The cipher encrypted which is C , we need to find a way to get the public key and decrypt the cipher .

What's comes to my mind as always when i play rsa cipher stuff , is i need to make simple  script which decrypt it .

Cool , let's jump to it .

> First , we need factor the N , we can use factordb.com for that : 

![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/crypto3.png)

Cool , now we have q and the p , which can help us to create phi and inverse it to get the d which is the public key .
let's put this in our code : 
```python
n = 1280678415822214057864524798453297819181910621573945477544758171055968245116423923
e = 65537
c = 241757357533719849989659127349827982677055294256023833052829147857534659015212862
q = 1899107986527483535344517113948531328331
p = 674357869540600933870145899564746495319033
phi = (p-1)*(q-1)
d = pow(e, -1, phi)
print(d)
```
niiiceee , now we get the public key : 

`d = 449332735606084960351204406909610297301574728466820933515942864925459265983556193`

cool , now let's decrypt all that with pow function which it takes the `(c,d,n)`

now let's do this again : 
```python
n = 1280678415822214057864524798453297819181910621573945477544758171055968245116423923
e = 65537
c = 241757357533719849989659127349827982677055294256023833052829147857534659015212862
q = 1899107986527483535344517113948531328331
p = 674357869540600933870145899564746495319033
phi = (p-1)*(q-1)
d = pow(e, -1, phi)
flag = pow(ct,d,n)
print(flag)
```
> The flag output was : `1624859552418716967141738223597582357281207838060523765629`

it's seems weird right , we have a long bytes
we need to decrypt it with a lib in python which is :  `Crypto.Util.*`

well , let's write our last script : 

```python
from Crypto.Util.number import *
n = 1280678415822214057864524798453297819181910621573945477544758171055968245116423923
e = 65537
c = 241757357533719849989659127349827982677055294256023833052829147857534659015212862
q = 1899107986527483535344517113948531328331
p = 674357869540600933870145899564746495319033
phi = (p-1)*(q-1)
d = pow(e, -1, phi)
flag = pow(ct,d,n)
print(long_to_bytes(flag))
```
![image info](https://github.com/Shakun8/BDSecCTF-2022/blob/main/images/crypto4.png)

flag = `BDSEC{r54_i5_fUn_r16h7?}`


# I Hope you enjoy it !
