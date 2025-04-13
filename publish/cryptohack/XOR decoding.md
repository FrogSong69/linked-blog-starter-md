
If you have a table like below, and need to decode we can use a simple techince:

When we have the product of KEY1^KEY2 since how XORing works we can XOR KEY1 ^ Product (KEY2 ^ KEY1) = KEY2

```python
KEY1 = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313 
KEY2 ^ KEY1 = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e 
KEY2 ^ KEY3 = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1 
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf
```

```python
#!/usr/bin/env python3

from Crypto.Util.number import *
import sys
import base64
from pwn import *


#!/usr/bin/env python3

from pwn import xor

# Given values in hexadecimal
key1 = bytes.fromhex("a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313")
key1_xor_key2 = bytes.fromhex("37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e")
key2_xor_key3 = bytes.fromhex("c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1")
result = bytes.fromhex("04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf")

# Step 1: Compute KEY2
key2 = xor(key1, key1_xor_key2)

# Step 2: Compute KEY3
key3 = xor(key2, key2_xor_key3)

# Step 3: Compute FLAG
flag = xor(result, key1, key2, key3)

# Print results
print("KEY2:", key2.hex())
print("KEY3:", key3.hex())
print("FLAG:", flag.decode(errors="ignore"))  # Decode FLAG to a readable string
```



If we have a random looking hex string, like below but we know portion of what is final text in this case the flag will start with crypto{ FLAG HERE }

0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104

We can use a website like this:
https://gchq.github.io/CyberChef/#recipe=From_Hex('Auto')XOR(%7B'option':'UTF8','string':'myXORkey'%7D,'Standard',false)&input=MGUwYjIxM2YyNjA0MWU0ODBiMjYyMTdmMjczNDJlMTc1ZDBlMDcwYTNjNWIxMDNlMjUyNjIxN2YyNzM0MmUxNzVkMGUwNzdlMjYzNDUxMTUwMTA0&oeol=CR