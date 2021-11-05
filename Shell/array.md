# 数组

数组（array）是一个包含多个值的变量。成员的编号从 0 开始，数量没有上限，也没有要求成员被连续索引。

## 数组的类型

`declare` 关键字声明数组， `-A` 声明关联数组， `-a` 声明索引数组。

### 索引数组

### 声明数组

```bash
declare -a indexed_array
indexed_array[0]=value
```

#### 采用逐个赋值的方法创建

ARRAY 是数组的名字，可以是任意合法的变量名。INDEX 是一个大于或等于零的整数，也可以是算术表达式。注意数组第一个元素的下标是 0， 而不是 1。

```bash
ARRAY[INDEX]=value

array[0]=value
array[1]=value1
array[2]=value2
```

#### 指定数组元素的位置

```bash
# 默认顺序赋值位置
array=(a b c)

# 指定值的位置
array=([2]=c [0]=a [1]=b)
```

#### 指定部分元素的位置

`a` 是 0 号位置，`b` 是 4 号位置， `c` 是 5 号位置。

```bash
arrays=(a [4]=b c)
```

### 读取数组

>注意: `{}` 不能省略，否则的话会 `读取该数组的首个元素值`，然后将 `[i]` 原样输出。如果读取数组时，没有指定对应的索引的元素，那么默认读取该数组的首个元素。

#### 读取单个元素
  
```bash
# i 为元素的索引位置
echo ${array[i]}
```

#### 读取所有元素

```bash
echo ${array[@]}
```

另外，可以是配合 `for` 循环遍历数组中的所有元素。

```bash
for i in ${array[@]}
do
    echo $i
done
```

> 注意：`@`、`*` 是否放在 `""` 双引号中，是有一定差别的。

```bash

# 不加上 "" ，可以看出，遍历出来的元素是 6 个，但实际该数组中只有 4 个。
array=(a "b c" d "e f" )
for i in ${array[@]}
do
    echo $i
done

# 加上 ""，遍历出来的是正确的。
for i in "${array[@]}"
do
    echo $i
done

```

#### 获取数组的长度

```bash
array=(a "b c" d "e f" )

# 获取该数组有多少元素
echo ${#array[@]}
echo ${#array[*]}

# 需要注意的是，如果把 @、* 换成是对应的索引位置，则获取的是该索引对应元素值的长度
echo ${#array[1]}
```

#### 获取数组的索引位置

```bash
array=([5]=c [1]=a [7]=b)
echo ${!array[@]}
echo ${!array[*]}

# 也可以利用遍历所有索引，从而遍历数组
for i in ${!array[@]}
do
    echo ${array[i]}
done
```

#### 追加/删除数组元素

```bash
# 追加数组元素。
array+=(value1 value ……)

# 删除数组元素。注意，如果数组后面没有接对应的索引，直接是 unset array 则会删除数组所有的元素。
unset array[2]
```

### 关联数组

```bash
declare -A assoc_array
assoc_array[key]=value
```

#### 定义关联数组

```bash
declare -A array=(
    ["a"]=1
    ["b"]=2
    ["c"]=3
    ["e"]=4
)

```

#### 遍历关联数组的所有值

```bash
for i in ${array[@]}
do
    echo $i
done
```

#### 获取元素的值

```bash
echo ${array[a]}
```
