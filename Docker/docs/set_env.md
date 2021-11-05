# 配置 Docker 环境

下述操作均相对于 /etc/docker/daemon.json 阐述。

## 修改目录

```shell
{
    "data-root": "/data/docker",
}
# 修改后，需要将默认目录下的数据同步至新目录下
rsync -avgz /var/lib/docker /data/docker
```

## 限制日志大小以及数量

```shell
"log-opts": {
        "max-size": "500m",
        "max-file":"5"
    }
```

## 配置加速器

```shell
{
  "registry-mirrors": [
    "https://hub-mirror.c.163.com"
  ]
}
```

- 设置代理可参考 [https://docs.docker.com/config/daemon/systemd/#httphttps-proxy](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy)
