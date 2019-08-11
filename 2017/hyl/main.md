# Hack Your Life

DuckLL  
2017/12/13 <!-- .element: align="right" -->

---

# 生活中用得到的駭客技巧

1. file
1. Cheat Engine
1. Resource Hacker

---

# file

猜測檔案格式

```sh
$file unkonw.xxx
```

--

# 原理

header magic number

- png 0x89504E47
- jpg 0x25504446
- exe 0x4D5A9000
- zip 0x504B0304

--

# DEMO

---

# Cheat Engine

外掛神器

--

# 程式啟動概要

- 程式碼載入記憶體(.text)
- 字串會存在(.rdata)
- global 變數會存在(.data)
- 區域變數會在(stack, heap)

更改記憶體就能?

--

# 幾招技巧

- 追值 改值
- 改程式碼

--

# DEMO

---

# Resource Hacker

拆解 EXE 檔內容

--

# DEMO

---

# 想成為

# 生活駭客?

--

# 直接進入

# 業配主題

--

# 更多文章

# www.duckll.tw

--

# Hacker 2018

# 每週四 19:00

# 台達 632

--

# END

Thank you for listening
