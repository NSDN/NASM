# NSASM-C
NyaSama Assembly Script Module - C Ver

C语言重置版 (非单文件版)
## Introduction (zh_CN)

### 操作符不区分大小写

#### 指令助记符设计参考 Intel 8086 汇编

```
r#      # = 0 to (REG_CNT - 1)，通用寄存器
mov     数据传送
push    入栈
pop     出栈
in      输入，0x00为标准输入流，仍在开发中
out     输出，地址0x00为标准输出流，0xFF带有[DEBUG]前缀输出
add     加法
inc     加一
sub     减法
dec     减一
mul     乘法
div     除法
cmp     比较，仅此操作符能改变跳转状态寄存器
jz      零则跳转
jnz     非零则跳转
jg      大于则跳转
jl      小于则跳转
and     与
or      或
xor     异或
not     非
shl     左移
shr     右移
end     程序结束，或子程序结束
run     加载外部子程序文件，带提示，寄存器组隔离，以""包括文件路径
call    加载外部子程序文件，无提示，寄存器组隔离且初值为父寄存器组数据，以""包括文件路径
nop     空指令
rst     复位，PC不可用，暂未实现
rem     注释行前缀，可不带内容，以""包括注释
```

### 基本结构

``` javascript
.conf {
    stack 栈大小
    heap 堆大小
}

.data {
    rem "这是注释"
    rem "var 变量名 = 值"
    var a = 1           整数
    var b = 0x1         整数
    var c = 2h          整数
    var d = 1.0         浮点
    var e = 2F          浮点
    var f = 3.0F        浮点
    var g = 'a'         字符
    var h = "ho"        字符串，此变量为字符串首地址，只读
    var i = "ho" * 2    字符串，此变量为字符串首地址，只读，2代表重复次数
}

.code {
    rem "这是注释"
    ...
    [TAG]
    rem
    rem "标号必须使用中括号[]包括起来"
    ...
    jmp [TAG]
    ...
    cmp r0, r1
    jz [TAG]
    rem "寄存器为r0~r#，r不区分大小写，# = (REG_CNT - 1)"
    rem "仅cmp指令影响跳转标志"
    rem "'cmp a, b'相当于判断a - b的结果，是0还是大于0还是小于0"
    call "somedir/something.ns"
    rem "无提示加载外部子程序文件，路径用双引号包括"
    end
}
```

### 如何运行

使用 `run/make.bat` 编译后得到可执行文件，比如 `nsasm.exe` ，则：

`nsasm.exe [c/r] [FILE]`

c为交互式执行，r为执行脚本

其中缺省参数为r

#### Copyright © NSDN 2014 - 2019
