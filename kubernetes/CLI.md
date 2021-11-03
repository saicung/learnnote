# CLI

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

