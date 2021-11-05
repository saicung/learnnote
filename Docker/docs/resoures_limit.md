# 资源限制

启动一个容器如果没有对其进行资源限制，默认情况下主机内核是会尽可能的给予程序调度更多的主机资源。为了降低因主机资源带来的风险，需要在启动一个容器 `docker run` 时就对内存、网络、磁盘等进行限制。

## 内存限制

启动时没有对容器进行内存限制，如果主机内核检测到没有足够的内存来维持执行重要的程序，那么将会抛出 OOME 或者 Out Of Memory Exception 的错误，与此同时终止程序进行释放内存，任何进程都将有可能会被 kill，如果 kill 错误的进程，会是整个程序崩溃，从而带来严重的后果。因此，在启动容器时，需要强制的限制内存, `docker run --help` 可以找到 -m 的选项参数，该选项则是对内存的限制。

```shell
docker run --help
……
  -m, --memory bytes                   Memory limit        # 容器可以使用的最大内存量。如果设置此选项，则最小允许值为 4m（4 MB）。
      --memory-reservation bytes       Memory soft limit   # 允许您指定一个小于--memoryDocker在主机上检测到争用或内存不足时激活的软限制。如果使用--memory-reservation，则必须将其设置为低于，--memory以使其具有优先权。因为这是一个软限制，所以不能保证容器不超过该限制。
      --memory-swap bytes              Swap limit equal to memory plus swap: '-1' to enable unlimited swap  # 允许此容器交换到磁盘的内存量
      --memory-swappiness int          Tune container memory swappiness (0 to 100) (default -1)    # 默认情况下，主机内核可以换出一定比例的容器使用的匿名页面。您可以设置--memory-swappiness一个介于0到100之间的值来调整此百分比。
……
```

## CPU 限制

默认情况下，每个容器对主机的 CPU 周期的访问都是不受限制的。

```shell
docker run --help
……
-c,   --cpu-shares int                 CPU shares (relative weight)
      --cpus decimal                   Number of CPUs     # 指定一个容器可以使用多少可用的CPU资源。例如，如果主机有两个CPU，并且您设置了--cpus="1.5"，则可以保证容器最多容纳一半的CPU。
      --cpuset-cpus string             CPUs in which to allow execution (0-3, 0,1)
      --cpuset-mems string             MEMs in which to allow execution (0-3, 0,1)
……
```

如果您有 1 个 CPU，则以下每个命令都会确保容器每秒最多占用 50％ 的 CPU。

```shell
docker run -it --cpus=".5" ubuntu /bin/bash
```

这等效于手动指定 `--cpu-period` 和 `--cpu-quota`

```shell
docker run -it --cpu-period=100000 --cpu-quota=50000 ubuntu /bin/bash
```

## 磁盘 I/O 限制


## 参考资料

- [https://docs.docker.com/config/containers/resource_constraints/](https://docs.docker.com/config/containers/resource_constraints/)
