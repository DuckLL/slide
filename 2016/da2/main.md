#Dynamic Analysis

廖子慶  
2016/12/06 <!-- .element: align="right" -->

---

# Tool

1. Immunity Debugger
1. Qira

---

# Immunity Debugger
[Download_backup](https://drive.google.com/open?id=0B5w3KuqR3zoBVjhOaDQ5Z1JfSk0)

--

## Just like GDB in GUI
Find and Patch

[Can't Pass](https://drive.google.com/open?id=0B5w3KuqR3zoBZ3BWYlBhQnFSQUk)

```c
#include <stdio.h>
int main(int argc, char *argv[])
{
    int a=0;
    if(a){
    	puts("{{flag}}");
    }
    else{
    	puts("can't pass");
    }
    return 0;
}
```

--

# Practice
[Random](https://drive.google.com/open?id=0B5w3KuqR3zoBS20wN2dPS1U5UXc)

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
int main(int argc, char *argv[])
{
    srand(time(NULL));
    int x,y;
    while(1){
        y=rand()%10000;
        printf("guess number:");
        if(scanf("%d",&x)!=1){
            exit(1);
        }
        if(x==y){
            puts("{{flag}}");
        }
        else{
            printf("answer=%d\n",y);
        }
    }
    return 0;
}
```

---

# Qira
powerful tracer

--

## Command
| command | function |
| --- | --- |
| -s | server |
| -t | ltrace |

web on localhost:3002  
listening on localhost:4000

--

# Demo
[visiable](https://drive.google.com/open?id=0B5w3KuqR3zoBVkN0cG41UE54N2M)

```c
#include <stdio.h>
int main(int argc, char *argv[])
{
    char a[100]="1234";
    gets(a);
    puts(a);
    char* b=malloc(100);
    gets(b);
    puts(b);
    return 0;
}
```


---

#Q & A

--

#END

