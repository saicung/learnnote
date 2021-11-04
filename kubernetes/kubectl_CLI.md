# kubectl

- [kubectl](#kubectl)
  - [应用管理](#应用管理)
    - [kubectl get](#kubectl-get)
    - [kubectl label](#kubectl-label)
    - [kubectl scale](#kubectl-scale)
    - [kubectl autoscale](#kubectl-autoscale)
    - [kubectl set](#kubectl-set)
    - [kubectl rollout](#kubectl-rollout)
    - [kubectl edit](#kubectl-edit)
  - [使用应用](#使用应用)
    - [kubectl exec](#kubectl-exec)
    - [kubectl describe](#kubectl-describe)
    - [kubectl logs](#kubectl-logs)
    - [kubectl top](#kubectl-top)
    - [kubectl cp](#kubectl-cp)
  - [kubectl explain](#kubectl-explain)
  - [更多详情](#更多详情)

## 应用管理

### kubectl get

- 获取类型为 Pod 的资源列表

  ```bash
  # 不加 <pod_name> 默认显示全部 pod
  kubectl get pods <pod_name>
  ```

- 获取类型为 Node 的资源列表

  ```bash
  # 不加 <node_name> 默认显示全部 node
  kubectl get nodes <node_name>
  ```

- 获取类型为 Deployment 的资源列表

  ```bash
  # 查看所有名称空间的 Deployment
  kubectl get deployments -A
  kubectl get deployments --all-namespaces

  # 查看 kube-system 名称空间的 Deployment
  kubectl get deployments -n kube-system
  ```

- 查看命名空间

  ```bash
  kubectl get namespaces
  ```

- 查看 job

  ```bash
  kubectl get job
  ```

- 查看所有标签

  ```bash
  kubectl get nodes/pod/deployments --show-labels
  ```

### kubectl label

- 添加标签。给指定的 pod 添加标签

  ```bash
  kubectl label pods <pod_name> <label_key>=<label_value>
  ```

- 修改指定 pod 标签并覆盖原有的值

  ```bash
  kubectl label --overwrite pods  <pod_name> <label_key>=<label_value>
  ```

### kubectl scale

- 扩容

  ```bash
  kubectl scale deployment <deployment_namr> --replica=10
  ```

  或者如果支持 Horizontal pod autoscaling，可以设置 deployment 为自动扩展

  ```bash
  kubectl autoscale deployment <deployment_namr> --min=1 --max=10 --cpu-percent=80
  ```

### kubectl autoscale

- 自动扩容
  
  创建一个自动缩放器，自动选择和设置在 Kubernetes 集群中运行的 pod 数量

  ```bash
  # 自动扩展部署 pod，pod 数量在 2 到 10 之间，未指定目标 CPU 利用率，因此将使用默认的自动扩展策略 
  kubectl autoscale deployment <pod_name> --min=2 --max=10

  # 自动扩展复制控制器 pod，pod 数量在 1 到 5 之间，目标 CPU 利用率为 80%
  kubectl autoscale rc <pod_name> --max=5 --cpu-percent=80
  ```

### kubectl set

- 更新镜像

  ```bash
  kubectl set image deployment/<deployment_namr> <container_name>=<image_name>:<tag>
  ```

### kubectl rollout

- 回滚

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

### kubectl edit

  修改 configMap

  ```bash
  # KUBE_EDITOR 使用替代编辑器（可选）
  # --save-config：修改后的配置保存在其注释中
  KUBE_EDITOR="vim" kubectl edit cm -n <deployment_namr> <pod_name> --save-config
  ```


## 使用应用

### kubectl exec

- 在 pod 中的容器环境内执行命令

  ```bash
  kubectl exec -it <pod_name> -- /bin/bash
  ```

### kubectl describe

- 显示有关资源的详细信息

  ```bash
  kubectl describe pod <pod_name>

  #查看名称为 nginx 的Deployment的信息
  kubectl describe deployment <deploy_name>
  ```

### kubectl logs

- 查看日志信息

  ```bash
  # -f 实时查看 --tail 查看末尾日志
  kubectl logs -f <pod_name> --tail=<num>

  # 从标签定义的 pod 中的所有容器返回快照日志
  kubectl logs -l <label_key>=<label_value> --all-containers=true

  # 显示过去 1小时内来自 pod 的所有日志
  kubectl logs --since=1h <pod_name>

  # 显示 deployment 的容器的日志
  kubectl logs deployment/<deploy_name> -c <flag_name>
  ```

### kubectl top

  ```bash
  # 显示所有节点的指标
  kubectl top node

  # 显示指定节点的指标
  kubectl top node <node_name>
  ```

### kubectl cp

将文件和
目录复制到容器或从容器复制。

  ```bash
  # 将 /tmp/foo_dir 本地目录复制到默认命名空间中远程 pod 中的 /tmp/bar_dir
  kubectl cp /tmp/foo_dir <pod_name>:/tmp/bar_dir

  # 将 /tmp/foo 本地文件复制到命名空间中远程 pod 中的 /tmp/bar
  kubectl cp /tmp/foo <namespace_name>/<pod_name>:/tmp/bar

  # 将 /tmp/foo 从远程 pod 复制到本地的 /tmp/bar
  kubectl cp <namespace_name>/<pod_name>:/tmp/foo /tmp/bar
  ```

## kubectl explain

列出支持资源的字段

```bash
# 获取资源及其字段的文档
kubectl explain pods

# 获取资源特定字段的文档
kubectl explain pods.spec.containers
```

## 更多详情

[kubectl-commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
