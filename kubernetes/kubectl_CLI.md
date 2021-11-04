# Kubectl

- [Kubectl](#kubectl)
  - [Kubectl get](#kubectl-get)
    - [获取类型为 Pod 的资源列表](#获取类型为-pod-的资源列表)
    - [获取类型为 Node 的资源列表](#获取类型为-node-的资源列表)
    - [获取类型为 Deployment 的资源列表](#获取类型为-deployment-的资源列表)
    - [查看命名空间](#查看命名空间)
    - [查看所有标签](#查看所有标签)
  - [Kubectl describe](#kubectl-describe)
    - [显示有关资源的详细信息](#显示有关资源的详细信息)
  - [Kubectl log](#kubectl-log)
    - [查看日志信息](#查看日志信息)
  - [Kubectl exec](#kubectl-exec)
    - [在 pod 中的容器环境内执行命令](#在-pod-中的容器环境内执行命令)
    - [添加标签](#添加标签)
    - [修改指定 pod 标签并覆盖原有的值](#修改指定-pod-标签并覆盖原有的值)
  - [扩容](#扩容)
  - [更新镜像](#更新镜像)
  - [回滚](#回滚)
  - [更多详情](#更多详情)

## Kubectl get

### 获取类型为 Pod 的资源列表

```bash
# 不加 <pod_name> 默认显示全部 pod
kubectl get pods <pod_name>
```

### 获取类型为 Node 的资源列表

```bash
# 不加 <node_name> 默认显示全部 node
kubectl get nodes <node_name>
```

### 获取类型为 Deployment 的资源列表

```bash
kubectl get deployments

# 查看所有名称空间的 Deployment
kubectl get deployments -A
kubectl get deployments --all-namespaces

# 查看 kube-system 名称空间的 Deployment
kubectl get deployments -n kube-system
```

### 查看命名空间

```bash
kubectl get namespaces
```

### 查看所有标签

```bash
kubectl get nodes/pod/deployments --show-labels
```

## Kubectl describe

### 显示有关资源的详细信息

```bash
kubectl describe pod <pod_name>

#查看名称为 nginx 的Deployment的信息
kubectl describe deployment <deploy_name>
```

## Kubectl log

### 查看日志信息

```bas
# -f 实时查看 --tail 查看末尾日志
kubectl logs -f <pod_name> --tail=<num>
```

## Kubectl exec

### 在 pod 中的容器环境内执行命令

```bash
kubectl exec -it <pod_name> -- /bin/bash
```

### 添加标签

给指定的 pod 添加标签

```bash
kubectl label pods <pod_name> <label_key>=<label_value>
```

### 修改指定 pod 标签并覆盖原有的值

```bash
kubectl label --overwrite pods  <pod_name> <label_key>=<label_value>
```

## 扩容

```bash
kubectl scale deployment <deployment_namr> --replica=10
```

或者如果支持 Horizontal pod autoscaling，可以设置 deployment 为自动扩展

```bash
kubectl autoscale deployment <deployment_namr> --min=1 --max=10 --cpu-percent=80
```

## 更新镜像

```bash
kubectl set image deployment/<deployment_namr> <container_name>=<image_name>:<tag>
```

## 回滚

```bash
# 回滚操作
kubectl rollout undo deployment/<deployment_namr>

# 回滚到指定版本
kubectl rollout undo deployment/<deployment_namr> --to-revision=<历史版本>

# 查看回滚状态
kubectl rollout status deployment/<deployment_namr>

# 查看历史回滚，注意只有在创建时添加了 --record 参数，执行的命令才会被记录。
kubectl rollout history deployment/<deployment_namr>

# 暂停 deploy 的更新
kubectl rollout pause  deployment/<deployment_namr>
```

## 更多详情

[kubectl-commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)