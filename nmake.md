### nmake参数

```
# debug makefile，有的宏变量也没显示结果
nmake /D /P -f a.mak
```

source: [Running NMAKE | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/build/reference/running-nmake?view=msvc-170)

---

### 打印变量

```
# 在makefile末尾添加变量打印target, target下命令前是`tab`缩进
echoval:
	echo WINVER=[$(WINVER)]
	echo MSVCVER=[$(MSVCVER)]
	echo CC=[$(CC)]
	echo CFLAGS=[$(CFLAGS)]
	echo MAKE=[$(MAKE)]
	echo LINK=[$(LINK)]

# nmake执行打印变量target, 默认命令会输出两行，第一行是命令，第二行是运行结果
nmake -f a.mak echoval

# 简化输出，只显示运行结果
nmake /NOLOGO /S -f a.mak echoval
```

---

### nmake内置的特殊macro

source: [Special NMAKE macros | Microsoft Learn](https://learn.microsoft.com/en-us/cpp/build/reference/special-nmake-macros?view=msvc-170)

