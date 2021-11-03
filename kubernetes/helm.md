# Helm

## Helm 与 Kubernetes 的关系

Helm 是 Kubernetes 生态系统中的一个软件包管理工具，类似 Linux 下的包管理工具 (yum)。
Helm 还提供了 Kubernetes 上的软件部署，删除，升级，回滚应用的强大功能.

>在 helm 提到的 release 和日常提到的版本有所不同这里的 release 可以理解为 Helm 使用 Chart 包部署的一个应用实例。

## Helm 使用

### 查看 repo 库

```bash
helm repo list
```

### 添加 repo 库

```bash
helm repo add <repo_name> <repo_url>
```

### 查找对应的 Chart

```bash
helm search repo <repo_name>/<chart_name>

# 查看以往历史版本chart
helm search repo <repo_name>/<chart_name> -l
```

### 部署 Chart

```bash
helm install <repo_name>/<chart_name> --name <chart_name>
```

### 查看已部署 release

```bash
helm ls
```

### 升级

升级前，可以使用该命令查看该 chart 的历史版本 `helm search repo <repo_name>/<chart_name> -l`

```bash
# 如果不指定版本号，默认使用最新版本
helm upgrade <chart_name> <repo_name>/<chart_name>  --version <chart_version>
```

### 查看 release 变更历史

```bash
helm history <chart_name>
```

### 回滚

```bash
# revision_num 是变更历史中的变更 REVISION
helm rollback <chart_name> <revision_num>
```
