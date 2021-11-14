# 安装 ingress-nginx

## 使用 helm 安装

- 部署 helm

```bash
wget https://get.helm.sh/helm-v3.7.0-linux-amd64.tar.gz

tar -xvf helm-v3.7.0-linux-amd64.tar.gz -C /data

mv linux-amd64/helm /usr/local/bin/
```

- helm 命令补全

```bash
source <(helm completion bash) >> ~/.bashrc
source ~/.bashrc
```

- 添加 ingress-nginx 仓库

```bash
helm repo add <repo_name> https://kubernetes.github.io/ingress-nginx
helm repo update
```

- 安装 ingress-nginx

```bash
helm install <release_name> ingress-nginx/ingress-nginx --version <ingress_nginx_chart_version> --set controller.service.type=NodePort --set controller.adminssionwebhooks.enabled=false
```

- 修改 hostNetwork

通过 hostNetwork 方式共享主机网络。(实际上就实现了NodeIP:80, 否则的话就需要通过 svc 暴露的端口进行访问)

```bash
kubectl edit deployments ingress-nginx-controller
```

- 访问 nginx

如果访问返回 404 则成功
