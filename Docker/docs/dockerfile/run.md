# Dockerfile 最佳实践 —— RUN

每一个 RUN 执行的时候都会新建一层 image layer，而需要主要注意的是：`Union FS 最大层数限制的，比如 AUFS，曾经是最大不得超过 42 层，现在是不得超过 127 层。`
所以编写 Dockerfile 时应该注意的是定义每一层应该如何构建，如果是相同的操作，如：yum 则可以简化为一层去处理。

此外，在执行完后，牢记要清理相关的缓存文件，确保只添加了真正实际需要的东西。因为镜像是多层存储的，每一层的东西并不会在下一层进行清理，而是会一直跟着镜像。

## RUN

- 执行命令行的命令，

RUN 有 2 中表达形式：

- RUN <command> 直接在命令行运行一样。

```shell
# 如果执行长语句或者复杂语句，可以使用 \ (反斜杠) 分割，使其更具可读性，可理解性和可维护性
RUN "/bin/bash -c 'source $HOME/.bashrc; \
echo $HOME'"
```

- RUN ["executable <可执行文件>", "param1", "param2"]

```shell
# Exec 表单被解析为 JSON 数组，这意味着必须在单引号(‘)前后使用双引号(“)。
RUN ["/bin/bash", "-c", "echo hello"]
```

## 参考资料

- [dockerfile 最佳实践](https://docs.docker.com/engine/reference/builder/)