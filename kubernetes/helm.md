# Helm

- [Helm](#helm)
  - [Helm 与 Kubernetes 的关系](#helm-与-kubernetes-的关系)
  - [Helm 使用](#helm-使用)
    - [查看 repo 库](#查看-repo-库)
    - [添加 repo 库](#添加-repo-库)
    - [查找对应的 Chart](#查找对应的-chart)
    - [部署 Chart](#部署-chart)
    - [查看已部署 release](#查看已部署-release)
    - [查看 release 的发布状态](#查看-release-的发布状态)
    - [查看 release 可配置项](#查看-release-可配置项)
    - [升级 release](#升级-release)
    - [查看 release 变更历史](#查看-release-变更历史)
    - [回滚 release](#回滚-release)
    - [删除 release](#删除-release)
    - [查看 release 的说明信息](#查看-release-的说明信息)
    - [查看 release 在 k8s 中创建出来的资源](#查看-release-在-k8s-中创建出来的资源)
    - [查看 release 的 values 配置](#查看-release-的-values-配置)
    - [查看本地安装好的插件](#查看本地安装好的插件)
    - [安装插件](#安装插件)
    - [更新插件](#更新插件)
    - [卸载插件](#卸载插件)

[Helm 官网](https://helm.sh/zh/docs/)

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

helm 安装的顺序参考 [Helm 使用](https://helm.sh/zh/docs/intro/using_helm/)

```bash
helm install <repo_name>/<chart_name> --name <release_name>
```

### 查看已部署 release

```bash
# 查看发布到 k8s 中的 chart 对应的 release
helm ls
helm list
```

### 查看 release 的发布状态

```bash
helm status <release_name>
```

### 查看 release 可配置项

```bash
# 查看chart包中的 values.yaml 文件内容
helm show values <release_name>
```

### 升级 release

升级前，可以使用该命令查看该 chart 的历史版本 `helm search repo <repo_name>/<chart_name> -l`

```bash
# 如果不指定版本号，默认使用最新版本
helm upgrade <v> <repo_name>/<chart_name>  --version <chart_version>
```

### 查看 release 变更历史

```bash
helm history <release_name>
```

### 回滚 release

```bash
# revision_num 是变更历史中的变更 REVISION
helm rollback <release_name> <revision_num>
```

### 删除 release

```bash
# --keep-history 保留删除记录
helm uninstall <release_name> --keep-history

# 查看删除的记录
helm list --uninstalled

# 如果运行或者删除时，都加了 --keep-history 参数选项，那么可以用下面的命令查看所有的历史 (包括失败，删除的)
helm list --all
```

### 查看 release 的说明信息

```bash
helm get notes <release_name>
```

### 查看 release 在 k8s 中创建出来的资源

```bash
helm get manifest <release_name>
```

### 查看 release 的 values 配置

```bash
# 查看 install 后 自定义的 values 
helm get values <release_name>
```

### 查看本地安装好的插件

```bash
helm plugin list
```

### 安装插件

```bash
helm plugin install <plugin_url>
```

### 更新插件

```bash
helm plugin upgrade <plugin_name>
```

### 卸载插件

```bash
helm plugin uninstall <plugin_name>
```
