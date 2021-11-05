# Dockerfile 最佳实践 —— ENV、ARG

## ENV

表达形式：

```shell
# 允许一次设置多个变量
ENV <key>=<value> ...
```

该 `ENV` 指令将环境变量 <key> 设置为 value <value>，此值将在构建阶段中所有后续指令的环境中使用。并且在许多情况下也可以内联替换。
该值将为其他环境变量解释，因此如果不对引号字符进行转义，则将其删除。像命令行解析一样，引号和反斜杠可用于在值中包含空格。

```shell
ENV MY_NAME="ascmcs Zh"
ENV MY_cat=Rex\ The\ cat
```

## ARG

ARG 指令也是设置环境变量，有所不同的是，ARG 是设置构建环境的环境变量。在以后容器运行时都不会出现这些环境变量。使用 ENV 指令定义的环境变量 始终会覆盖 ARG 同名指令。

>不建议使用构建时变量来传递诸如 github 密钥，用户凭据等机密。构建时变量值对于使用该 `docker history` 命令的图像的任何用户都是可见的。
>请参阅使用 [BuildKit 生成映像](https://docs.docker.com/develop/develop-images/build_enhancements/#new-docker-build-secret-information) 部分，以了解有关在生成映像时使用机密的安全方法。

ARG 指令是有生效范围的，例如在 FROM 指令之前进行指定，那么只能用于 FROM 指令中：

```shell
ARG NAME="ascmcs"
FROM ${NAME}/centos

# 这里则不会生效，如果需要生效，需要重新设置 ARG 变量
RUN echo ${NAME}
```

## 参考资料

- [dockerfile 最佳实践](https://docs.docker.com/engine/reference/builder/)
