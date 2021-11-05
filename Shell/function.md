# Shell 函数

函数可以使你的脚本总体功能分解为更小的逻辑子部分，然后在不同的地方进行调用。实现代码的复用。

## 函数的定义形式

```bash
function_name () {
    list of commands
}

# 或者

function function_name () {
    list of commands
}

```

### 向函数传递参数

当定义一个调用函数时接受参数的函数，可以使用 `$1`、`$2` …… `$n` 来进行传递。

#### 参数变量

```bash
#!/bin/bash

# 定义 Hello 函数
Hello () {
   echo "Hello $1 $2"
}

# 执行函数
Hello None Zh
```

- `$1` ~ `$9`：函数的第一个到第 9 个的参数。
- `$0`：函数所在的脚本名。
- `$#`：函数的参数总数。
- `$@`：函数的全部参数，参数之间使用空格分隔。
- `$*`：函数的全部参数，参数之间使用变量 `$IFS` 值的第一个字符分隔，默认为空格，但是可以自定义。
- `$?`: 上个命令的退出状态，或函数的返回值。
- `$$`: 当前 Shell 进程 ID。对于 Shell 脚本，就是这些脚本所在的进程 ID。

> **\$\* 与 \$\@ 的区别：** 未加引号，二者相同；加了引号，\$\* 返回的是字符串的整体，\$\@ 则把每个参数作为一个字符串返回。

### 查看定义的函数

`declare` 可以查看已经定义的所有函数，后接函数名可以查看单个函数的定义

```bash
# 会展开所有的函数的详细信息，输出可能比较多内容，可以传递至 more 或者 less 查看
declare -f 

# 查看单个函数
declare -f function_name

# 仅查看函数名
declare -F
```

## 函数返回值 return

如果从函数内部执行 exit 命令，其不仅是终止函数的执行，而且是调用函数的 shell 程序的执行。

如果想终止函数的执行，那么可以从自定义的函数中产生，使用 `return` 返回任何值。

```bash
#!/bin/bash
# 后面也可以不接 code，直接 return

function_name () {
    list of commands
    return code
}
```

## 函数嵌套

函数的相互调用，调用自身的函数称为 `递归函数`。

```bash
#!/bin/bash

function_name1 () {
    list of commands
    function_name2
}

function_name2 () {
    list of commands
}
```

## 全局变量、局部变量

函数的局部变量可以用局部内建立声明。这些变量只对函数及其调用的命令可见。全局变量整个脚本均可读取。

```bash
#!/bin/bash

# global_variable 全局变量
global_variable=value


function_name () {
    # local 定义局部变量
    local part_variable=value1

    # 改变全局变量的值
    local global_variable=value2
    list of commands
}
```

## 删除函数定义

若要从 shell 中删除函数的定义，可以使用 unset 命令

```bash
unset -f function_name
```

## 参考资料

- [Linux-Shell Function](https://www.tutorialspoint.com/unix/unix-shell-functions.htm)
- [Shell Function](https://www.gnu.org/software/bash/manual/html_node/Shell-Functions.html)
