# Dockerfile 最佳实践 —— COPY、ADD

## COPY

2 种表达形式：

COPY 指令从以下位置复制新文件或目录 <src> ，并将它们添加到容器的文件系统中 <dest>。
<src>可以指定多个资源，但是文件和目录的路径将被解释为相对于构建上下文的源。
每个都<src>可能包含通配符，并且匹配将使用 Go 的 [filepath.Match](http://golang.org/pkg/path/filepath#Match) 规则完成

- COPY <src> <dest>

```shell
# 如果 mydir 是一个 相对路径，那么是相对于 WORKDOR ，到其中的源将在容器内进行复制。
COPY hom* /mydir/
```

## ADD

ADD 是更高级的复制指令。只是在 COPY 的基础上新增了一些功能。添加远程文件/目录，建议使用 curl 或者 wget。

例如：

- 如果源文件是 URL，那么则会尝试下载该链接文件放到目标路径下，下载后的权限默认为 `600`，如果权限不满足，则需要自行设置；
如果 URL 下载的是压缩包，那么是不会自动解压的，还是需要通过 RUN 命令来进行操作。

- 如果源文件是压缩包，那么则会解压复制到目标路径下。

```shell
ADD test.tar.gz /opt
```

大部分情况下， COPY 要优于 ADD， ADD 除了有 CPOY 的功能外还有额外的解压功能。

## 参考资料

- [dockerfile 最佳实践](https://docs.docker.com/engine/reference/builder/)
