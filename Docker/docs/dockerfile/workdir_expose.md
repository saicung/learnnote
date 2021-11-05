# Dockerfile 最佳实践 —— WORKDIR、EXPOSE

## WORKDIR

WORKDIR 类似于 `cd`，如果 WORKDIR 不存在，那么即使后面的 Dockerfile 任何指令中都没有使用它，也将创建它。如多次使用时，只提供了相对路径，那么它将相对于上一条 WORKDIR 指令的路径。

使用 WORKDIR，而不要使用 `cd`，尽量使用 `绝对路径`，不要使用相对路径（易出错）。

```shell
WORKDIR /aa
WORKDIR bb

RUN pwd   
# 那么实际的输出应该是 /aa/bb
```

## EXPOSE

> EXPOSE 指令通知 Docker 容器在运行时监听指定的网络端口。您可以指定端口是侦听 TCP 还是 UDP，如果未指定协议，则默认值为 TCP。

**注意：** 这只是一个声明，在容器运行时并不会因为这个声明应用就会开启这个端口的服务。

主要格式为：

```shell
EXPOSE <port1> <port2>

# 例如
EXPOSE 80/tcp
EXPORT 80/udp
```

EXPOSE 需要与 `docker run -P` <-p <宿主端口>:<容器端口>> 区分，也就说，将容器的对应端口服务公开给外界访问，而 EXPOSE 仅仅是声明容器打算使用什么端口而已，并不会自动在宿主进行端口映射。

## 参考资料

- [dockerfile 最佳实践](https://docs.docker.com/engine/reference/builder/)