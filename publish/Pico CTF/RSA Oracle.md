
How does RSA work?

- A pair of keys are generated, one _public_ key and one **private** key.
- The _public_ key has two parts - a modulus `n` and a public exponent `e`.
- The **private** key has the private exponent `d`.
- To encrypt:
    
			    c=me (mod n)c=me (mod n)
- To decrypt:
    
			    m=cd (mod n)m=cd (mod n)

the public exponent `e` that is commonly used is 65537.


For this challenge we learn to use pwntools

First, taking in the `password.enc` text and storing it in c. Then encrypting 2 which is sent in hex and put into the c_a variable. The multiply c and c_a to where it is now in a format that the program will allow it to be decrypted. Once decrypted it takes the hex version which is why it is converted from hex with the `int(x, 16)` function. Then it uses integer division to divide by 2 to get the password.

We can see the script in kali/data/RSA/rsaAttack.py

```python
from pwn import *

# create a remote connection to the instance
conn = remote("titan.picoctf.net", 64828)

# read until the end of the prompt
conn.recvuntil("decrypt.")

# read the encrypted password to a variable
with open("password.enc") as password_file:
    c_a = int(password_file.read())

# encrypting plaintext 2
conn.sendline(b"E")
conn.recvuntil("keysize): ")

# there is an important note here its \0x02 since \ is the start of a hex decimal /x02 is something completly different 
conn.sendline(b"\x02")
conn.recvuntil(b"mod n) ")

# reading the ciphertext for 2 to a variable
c_b = int(conn.recvline())

# decrypting c_b * c_a as described in the method above
conn.sendline(b"D")
conn.recvuntil(b"decrypt: ")
conn.sendline(str(c_b * c_a).encode())
conn.recvuntil(b"mod n): ")

# convert the receiving value from hex to int, and integer dividing it by 2 to obtain the password ciphertext
password = int(conn.recvline(), 16) // 2

print(password)

password = password.to_bytes(len(str(password)) - 7).decode("utf-8")

# we're done!
print(password)

## openssl aes-256-cbc -d -in secret.enc
## password=da099
```