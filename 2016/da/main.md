#Dynamic Analysis

廖子慶  
2016/11/22 <!-- .element: align="right" -->

---

# Tool

1. strace
1. ltrace
1. GDB

---

# strace

system trace

```shell
strace elf
```

--

# ltrace

library

```shell
ltrace elf
```

---

# GDB

1. run
1. attach
1. remote

--

# Command

| command |  function   |
|   ---   |     ---     |
|    r    |     run     |
|    b    | break point |
|    c    |  continue   |
|   si    |  step into  |
|   ni    | step cross  |
|   fin   |  step out   |
|    q    |    quit     |

--

# Command(Cont.)

|       command       |        function        |
|         ---         |          ---           |
|     x/4wx $esp      | print 4 word from $esp |
|    info function    |     show function      |
|     p function      |   function location    |
|   disass function   |  disassemble function  |
|        find         |      find string       |
|         bt          |       backtrace        |
|       record        |         record         |
|         rsi         |       step back        |
| set {type}adr=value | change value in memory |


--

# SOP

1. IDA first
1. info functions
1. b
1. lay regs (peda)
1. r
1. record
1. ni, si, rsi, fin
1. set
1. c
1. q

---

# Run

--

# Demo

[wait](https://drive.google.com/open?id=0B5w3KuqR3zoBaVpJd3ZndWRWb3M) <!-- .element: target="_blank" -->

```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
int main(int argc, char *argv[])
{
    if(sleep(60*60*24*365*30)!=1){
        exit(1);
    }
    puts({{flag}});
    return 0;
}
```

---

# Attach

```shell
pidof elf
```

```gdb
attach {{pid}}
```

--

# pwngdb

```gdb
at elf
```

---

# Remote

cross-architecture

```shell
qemu-arm -g 5566 ./elf
gdb-multiarch -q -n
```

```gdb
file elf
set architecture arm
target remote 127.0.0.1:566
```

[magic_bof](https://drive.google.com/open?id=0B5w3KuqR3zoBdUdLT3JaVlZSQXc) <!-- .element: target="_blank" -->

---

# Practice

--

[can't_pass](https://drive.google.com/open?id=0B5w3KuqR3zoBRHVyZFRBM2FnLWs) <!-- .element: target="_blank" -->

```c
#include <stdio.h>
#include <unistd.h>
int main(int argc, char *argv[])
{
    int a=0;
    while(a!=10000){
        sleep(1);
        puts("loop");
    }
    puts("{{flag}}");
    return 0;
}
```

--

[random](https://drive.google.com/open?id=0B5w3KuqR3zoBUFRoQU5rUEN6REU) <!-- .element: target="_blank" -->
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
unsigned char flag[] = {
    0x6a, 0x0a, 0x68, 0x61, 0x73, 0x79, 0x7d, 0x68, 0x69, 0x73, 0x20, 0x65,
    0x68, 0x64, 0x6f, 0x6d, 0x20, 0x68, 0x7b, 0x72, 0x61, 0x6e, 0x68, 0x6e,
    0x74, 0x68, 0x75, 0xb8, 0x04, 0x00, 0x00, 0x00, 0xbb, 0x01, 0x00, 0x00,
    0x00, 0x89, 0xe1, 0xba, 0x15, 0x00, 0x00, 0x00, 0xcd, 0x80, 0xb8, 0x01,
    0x00, 0x00, 0x00, 0xcd, 0x80
};
int main(int argc, char *argv[])
{
    srand(time(NULL));
    int x,y;
    while(1){
        y=rand();
        printf("guess number:");
        if(scanf("%d",&x)!=1){
            exit(1);
        }
        if(x==y){
            int (*func)();
            func = (int (*)()) flag;
            (int)(*func)();
        }
        else{
            printf("answer=%d\n",y);
        }
    }
    return 0;
}

```

---

#Q & A

--

#END

