# Dockerfile 最佳实践 —— FROM、LABEL

Dockerfile 是一个文本文件，其中包含了用户可以在命令行上调用的已组装images的所有 「指令」。一条指令就是一层。

## FROM

- 指定基础镜像且有效的 Dockerfile 文件必须以 `FROM` 开始。后续所有的指令操作都会指定的基础镜像上进行定制操作。

**特殊镜像：** scratch。这个镜像是虚拟的概念，实际不存在，一般用它来表示空白的镜像。如果以 scratch 为基础镜像的话，意味着不以任何镜像为基础，所写的指令将作为镜像第一层开始存在。

```shell
ARG  VERSION=latest
FROM [--platform] <image>[:tag] [AS <name>]
# 或者
FROM [--platform] <image>[@<digest>] [AS <name>]
```

- \-\-platform：在 FROM 引用多平台图像的情况下，可选标志可用于指定图像的平台。例如，`linux/amd64`， `linux/arm64`，或 `windows/amd64`。默认情况下，使用构建请求的目标平台。

- `tag` 和 `digest` 是可选的，如果忽略其中任何一个，那么构建器 latest 默认情况下都将使用标签。

- FROM 指令支持由 `ARG` 第一指令之前的任何指令声明的变量 FROM。

## LABEL

LABEL 指令将元数据添加到 iamge。ALABE 是键值对。要在 LABEL 值中包含空格，请像在命令行分析中一样使用引号和反斜杠。例如：

```shell
LABEL <key>=<value> <key>=<value> <key>=<value> ...
```

比如：可以添加构建镜像的作者、构建的日期、镜像的版本等。

```shell
LABEL org.opencontainers.image.create="2021-04-19"
LABEL org.opencontainers.image.authors="ascmcs"
LABEL org.opencontainers.image.version="1.0.0"
```

更多 LABEL 格式请参考 [image-spec](https://github.com/opencontainers/image-spec/blob/master/annotations.md)。

## 参考资料

- [dockerfile 最佳实践](https://docs.docker.com/engine/reference/builder/)
- 参考 [docker-library](https://github.com/docker-library) 的 dockerfile 的写法技巧
