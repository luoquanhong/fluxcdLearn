#Flux的初始化注意事项
## 不必按照官网的命令去初始化flux
>export GITLAB_TOKEN=<your-token>
> 
> 使用flux-cli命令去创建连接:
> flux bootstrap gitlab \
--owner=my-gitlab-username \
--repository=my-repository \
--branch=master \
--path=clusters/my-cluster \
--token-auth \
--personal

如果是按照这种方式，会变得不太灵活，首先必须要让你的gitlab是能够通过域名和正式的证书来访问，才可以正式初始化

##可以通过定义GitRepository和Kustomization这个两个api来触发flux的功能产生