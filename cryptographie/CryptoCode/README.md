# CryptoCode

An easy crypto challenge !

Hello Welcome to My write up about a cryptographie challenge that i've been played on BDsec CTF 2022 .

> First of all , let's take a view about the description : 

`
CryptoCode:
I convert plain text to cipher text by using Cryptocode library . Always Remember BDSEC is a KEY .`

Cipher :

`c00EtfL9GPq2EItQrkFyPKIMfVFZy0O4ssXtr/V2Io7NMbNS*Brue6Cex4JuWkWU0lUEK2w==*f8EsezuHu2WBstRDlWZiLg==*CZ/4FNMavWZu3kznPrAyeg==
`

And now let's understand the things more  .
Here we can see that this cipher is crypted with Cryptocode library

Let's look if we have this lib on python  : 
![image info](https://github.com/Shakun8/BDSec-CTF-2022/blob/main/images/crypto1.png)

Well , after reading the doc of this lib , I realize that there is a function called : `cryptocode.decrypt(cipher , key)`
this function take 2 arguments , first argument take the cipher and the key of the decryption .
> Let's back to the description we can see that they said : 

`Remember BDSEC is a KEY .`

So the key is : `BDSEC`

Cool , now let's decrypt xD .
let's write own python code to decrypt  : 

```python
import cryptocode

def decrypt():
	key = "BDSEC"
	myDecryptedMessage = cryptocode.decrypt("c00EtfL9GPq2EItQrkFyPKIMfVFZy0O4ssXtr/V2Io7NMbNS*Brue6Cex4JuWkWU0lUEK2w==*f8EsezuHu2WBstRDlWZiLg==*CZ/4FNMavWZu3kznPrAyeg==", key)
	return myDecryptedMessage
print(decrypt())

```

after we run it , we get the flag : 
![image info](https://github.com/Shakun8/BDSec-CTF-2022/blob/main/images/crypto2.png)

Flag : `BDSEC{cryp70_and_pyth0n_ar3_aw3s0me`

# I Hope you Enjoyt it XD
