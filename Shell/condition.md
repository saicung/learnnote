# 条件判断

## if 条件判断

if... else... fi 语句是控制语句，它允许 Shell 以受控的方式执行语句并做出正确的选择。

Shell 按照 if 的表达式进行判断，如果结果值为真，则执行给定的语句。如果表达式为 false，则不执行任何语句。

```bash
# then 可以分行也可以跟 if 同一行，跟 if 同一行需要使用英文分号 ";" 进行分割。

if expression;then
   Statement(s) to be executed if expression is true
else
   Statement(s) to be executed if expression is not true
fi
```

此外，if 结构的判断条件可以有三种形式，这三种形式都是等价的，且第三种支持正则匹配。当使用 `[]` 或者 `[[]]` 时，内部前后需要有空格。

```bash
# 一
if expression

# 二
if [ expression ]

# 三
if [[ expression ]]
```

### 文件判断

>表达式中的 `file` 要放在 `""` 中，防止该值为空，当为空时表达式会判断为 `true`。而放在双引号中，返回总是一个空字符串，此时会判断未 `false`。

- `[ -a "file" ]`：如果 file 存在，则为 `true`。
- `[ -b "file" ]`：如果 file 存在并且是一个块（设备）文件，则为 `true`。
- `[ -c "file" ]`：如果 file 存在并且是一个字符（设备）文件，则为 `true`。
- `[ -d "file" ]`：如果 file 存在并且是一个目录，则为 `true`。
- `[ -e "file" ]`：如果 file 存在，则为 `true`。
- `[ -f "file" ]`：如果 file 存在并且是一个普通文件，则为 `true`。
- `[ -g "file" ]`：如果 file 存在并且设置了组 ID，则为 `true`。
- `[ -G "file" ]`：如果 file 存在并且属于有效的组 ID，则为 `true`。
- `[ -h "file" ]`：如果 file 存在并且是符号链接，则为 `true`。
- `[ -k "file" ]`：如果 file 存在并且设置了它的“sticky bit”，则为 `true`。
- `[ -L "file" ]`：如果 file 存在并且是一个符号链接，则为 `true`。
- `[ -N "file" ]`：如果 file 存在并且自上次读取后已被修改，则为 `true`。
- `[ -O "file" ]`：如果 file 存在并且属于有效的用户 ID，则为 `true`。
- `[ -p "file" ]`：如果 file 存在并且是一个命名管道，则为 `true`。
- `[ -r "file" ]`：如果 file 存在并且可读（当前用户有可读权限），则为 `true`。
- `[ -s "file" ]`：如果 file 存在且其长度大于零，则为 `true`。
- `[ -S "file" ]`：如果 file 存在且是一个网络 socket，则为 `true`。
- `[ -t fd ]`：如果 fd 是一个文件描述符，并且重定向到终端，则为 `true`。 这可以用来判断是否重定向了标准输入／输出／错误。
- `[ -u "file" ]`：如果 file 存在并且设置了 setuid 位，则为 `true`。
- `[ -w "file" ]`：如果 file 存在并且可写（当前用户拥有可写权限），则为 `true`。
- `[ -x "file" ]`：如果 file 存在并且可执行（有效用户有执行／搜索权限），则为 `true`。
- `[ "file1" -nt "file2" ]`：如果 FILE1 比 FILE2 的更新时间最近，或者 FILE1 存在而 FILE2 不存在，则为 `true`。
- `[ "file1" -ot "file2" ]`：如果 FILE1 比 FILE2 的更新时间更旧，或者 FILE2 存在而 FILE1 不存在，则为 `true`。
- `[ "FILE1" -ef "FILE2" ]`：如果 FILE1 和 FILE2 引用相同的设备和 inode 编号，则为 `true`。

### 字符串判断

> - 表达式内的 `>` 和 `<`，必须用引号引起来（或者是用 `反斜杠` 转义）。否则，它们会被 shell 解释为重定向操作符。
> - 字符串判断时，变量要放在双引号之中，比如 `[ -n "$string" ]`，否则变量替换成字符串以后，表达式可能会报错，提示参数过多。另外，如果不放在双引号之中，变量为空时，命令会变成`[ -n ]`，这时会判断为 `true`。如果放在双引号之中，`[ -n "" ]`就判断为 `false`。

- `[ "string" ]`：如果 `string` 不为空（长度大于 0），则判断为真。
- `[ -n "string" ]`：如果字符串 `string` 的长度大于零，则判断为真。
- `[ -z "string" ]`：如果字符串 `string` 的长度为零，则判断为真。
- `[ "string1" = "string2" ]`：如果 `string1` 和 `string2` 相同，则判断为真。
- `[ "string1" == "string2" ]` 等同于 `[ string1 = string2 ]`。
- `[ "string1" != "string2" ]`：如果 `string1` 和 `string2` 不相同，则判断为真。
- `[ "string1" '>' "string2" ]`：如果按照字典顺序 `string1` 排列在 `string2` 之后，则判断为真。
- `[ "string1" '<' "string2" ]`：如果按照字典顺序 `string1` 排列在 `string2` 之前，则判断为真。

### 整数判断

> 缩写说明，便于记忆理解
>
> - eq：equals，等于
> - ne：no equals，不等于
> - le：less equals，小于等于
> - ge：greater equal，大于等于
> - lt：less than，小于
> - gt：greater than，大于

- `[ int1 -eq int2 ]`：如果 `int1` 等于 `int2`，则为 `true`。
- `[ int1 -ne int2 ]`：如果 `int1` 不等于 `int2`，则为 `true`。
- `[ int1 -le int2 ]`：如果 `int1` 小于或等于 `int2`，则为 `true`。
- `[ int1 -lt int2 ]`：如果 `int1` 小于 `int2`，则为 `true`。
- `[ int1 -ge int2 ]`：如果 `int1` 大于或等于 `int2`，则为 `true`。
- `[ int1 -gt int2 ]`：如果 `int1` 大于 `int2`，则为 `true`。

### 正则判断

前面的时候，已经说过 `[[]]` 是支持正则表达式判断的。

```bash
# =~ 正则匹配运算符， rex 正则表达式。
[[ string =~ rex ]]
```

### 逻辑判断

逻辑判断与其他判断表达式组合，可以实现更加复杂的判断。

- 且：`AND`，符号表达 `&&`，参数表达 `-a`。<记忆方式：该单词的首字母>
- 或：`OR`，符号表达 `||`，参数表达 `-o`。<记忆方式：该单词的首字母>
- 非：`NOT`，符号表达 `!`。

### 算术判断

在 Bash 中，提供了 `(( ))` 作为算术运算的条件判断，且会自动忽略内部的空格。
如果 (( )) 中的数值或者算术结果为 `0` 时，则判断返回的为 `false`，否则为 `true`。

> (( )) 只支持整数运算，不支持小数，否则会报语法错误。

- `+`：加法
- `-`：减法
- `*`：乘法
- `/`：除法（整除）
- `%`：余数
- `**`：指数
- `++`：自增运算（前缀或后缀）
- `--`：自减运算（前缀或后缀）

> 当 `++`、 `--` 运算符作为前缀或者后缀时是有区别的：
>
> 前缀：先进行计算，然后再返回值
>
> 后缀：先返回变量的值，然后再进行计算

#### 算术逻辑运算

- `<`：小于
- `>`：大于
- `<=`：小于或相等
- `>=`：大于或相等
- `==`：相等
- `!=`：不相等
- `&&`：逻辑与
- `||`：逻辑或
- `!`：逻辑否
- `expr1?expr2:expr3`：三元条件运算符。若表达式 `expr1` 的计算结果为非零值（算术真），则执行表达式`expr2`，否则执行表达式 `expr3`。

如果逻辑表达式为真，返回 `1`，否则返回 `0`。

#### 算术位运算（较少使用）

- `<<`：位左移运算，把一个数字的所有位向左移动指定的位。
- `>>`：位右移运算，把一个数字的所有位向右移动指定的位。
- `&`：位的 “与” 运算，对两个数字的所有位执行一个 `AND` 操作。
- `|`：位的 “或” 运算，对两个数字的所有位执行一个 `OR` 操作。
- `~`：位的 “否” 运算，对一个数字的所有位取反。
- `^`：位的异或运算（exclusive or），对两个数字的所有位执行一个异或操作。

```bash
echo $((16>>2))
4
echo $((16<<2))
64
```

#### let 命令

`let` 命令用于将算术运算的结果，赋予一个变量。

```bash
# x=2+3 这个式子里面不能有空格，否则会报错。
let x=2+3
echo $x
5
```

## case 条件判断

case 语句的基本语法是给出一个表达式，根据表达式的值计算并执行几个不同的语句。没有最大数量的模式，但最小的是一个。当语句部分执行时，命令 ;; 指示程序流应跳转到整个 case 语句的末尾。

> 如果想 case 结构匹配多个条件，可以在 `;;` 后加上 `&`<;;&> 实现匹配多个条件。

```bash
case word in
   pattern1)
      Statement(s) to be executed if pattern1 matches
      ;;
   pattern2)
      Statement(s) to be executed if pattern2 matches
      ;;
   pattern3)
      Statement(s) to be executed if pattern3 matches
      ;;
   *)
     Default condition to be executed
     ;;
esac
```

此外，case 条件判断还支持通配符匹配。详细可见 [Regex cheatsheet](https://remram44.github.io/regex-cheatsheet/regex.html)

- `a)`：匹配 `a`。
- `a|b)`：匹配 `a` 或 `b`。
- `[[:alpha:]])`：匹配单个字母。
- `???)`：匹配 3 个字符的单词。
- `*.txt)`：匹配 `.txt` 结尾。
- `*)`：匹配任意输入，通过作为 `case` 结构的最后一个模式。
