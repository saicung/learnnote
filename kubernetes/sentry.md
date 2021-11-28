# 部署 Sentry

## 添加 sentry repo

```bash
helm repo add stable http://mirror.azure.cn/kubernetes/charts
helm repo add incubator http://mirror.azure.cn/kubernetes/charts-incubator
helm repo update
helm search repo sentry
```

## 创建 sentry 命名空间

```bash
kubectl create namespace sentry
```

## helm 安装 sentry

```bash
helm  install sentry stable/sentry \
-n sentry \
--set persistence.enabled=true,user.email=sc4242@163.com,user.password=sc747200 \
--set ingress.enabled=true,ingress.hostname=www.scsentry.com,service.type=ClusterIP \
--set email.host=smtp.163.com,email.port=465 \
--set email.user=sc4242@163.com,email.password=13226762206..,email.use_tls=false \
--set redis.primary.persistence.storageClass=local-path \
--set postgresql.persistence.storageClass=local-path \
--wait
```

## 初始化 DB

```bash
# 进入容器
kubectl exec -it -n sentry sentry-web-xxxx /bin/bash

# 执行upgrade 操作
sentry upgrade
```

## 端口转发

```bash
kubectl get svc -n sentry

kubectl port-forward -n sentry svc/sentry --address=0.0.0.0  9000:9000
```
