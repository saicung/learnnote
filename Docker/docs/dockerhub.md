# Docker Hub

将自定义的 image 上传至 Docker Hub 进行存储。

## 登录

```shell
docker login -i <docker id>

# 退出
docker logout
```

## 推送镜像

推送之前，需要确保镜像已生成，并 `REPOSITORY` 的格式为：`<user_name>/<imags_name>`

```shell
docker push <user-name>/<image_name>

# 例如，docker hub 的用户名为：seichung，而我需要推送的镜像是 centos
# 如果未指定标签，则 Docker将使用名为的标签latest

docker tag centos:7.6 seichung/centos 
docker push seichung/centos
```

## 如何自动构建

### 关联源代码的代码存储库服务

目前仅支持 GitHub 和 Bitbucket 两种方式，为了简便，这边就以 GitHub 为例：

#### GitHub 侧

- 确保存在需要关联的存储库，如不存在，请新建。

#### Docker Hub 侧

- 登陆 Docker Hub 后，点击头像，选择 【Account Settings】->【Linked Accounts】-【选择 GitHub 处的 Connect】
- Docker Hub 中选择需要配置的存储库，选择 【Build】->【Configure Automated Builds】
- 选择需要关联的代码存储库
- 执行 Dockerfile 的位置即可

## 参考资料

- [Share the application](https://docs.docker.com/get-started/04_sharing_app/)
- [Set up automated builds](https://docs.docker.com/docker-hub/builds/)
