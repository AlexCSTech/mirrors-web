## Docker APT/YUM 镜像更新

Docker 官方部署了[新的 docker 源](https://blog.docker.com/2015/07/new-apt-and-yum-repos/), 我们也对
docker 镜像作出相应调整。

现在的镜像地址为:

- APT: http://{{ site.hostname }}/docker/apt/repo
- YUM: http://{{ site.hostname }}/docker/yum/repo

请根据 [docker镜像帮助](/help/docker) 调整至正确的打开方式。
