# 使用image安装gitlab的方式
>通过k8s部署gitlab,首先要设置evn变量来确定一些值，根据官网可以得知，可以设置如下变量:
> 
>       env:
>         - name: TZ # 容器时区
>           value: Asia/Shanghai
>         - name: GITLAB_TIMEZONE # 配置gitlab的时区
>           value: Beijing
>         - name: GITLAB_ROOT_PASSWORD
>           value: kingking
>         - name: GITLAB_OMNIBUS_CONFIG
>           value: "external_url 'http://192.168.80.131:8929'; gitlab_rails['gitlab_shell_ssh_port'] = 2224; gitlab_rails['gitlab_ssh_host'] = '192.168.80.131'; nginx['listen_port'] = 8929"
> "GITLAB_ROOT_PASSWORD"是初始化gitlab的pod的时候，root的登录密码
>
> "GITLAB_OMNIBUS_CONFIG"是对应gitlab.rb这个配置文件的设置，value值必须用双引号去括起来，value值之间用;号隔开，其中"external_url 'http://192.168.80.131:8929'中的8929是官网提供的额端口号，这样写访问的时候也是直接访问http://192.168.80.131:8929

## 在使用git来clone代码的时候，要注意的事项：
>1)如果使用ssh方式来进行clone是暂时按照百度上的做法是没有问题的
> 
>2）使用clone方式选择为http方式的时候，要在git设置如下命令git config --global http.proxy "192.168.80.131:8929"($ip地址:$端口，不带http://这个开头),如果不设置，在使用git clone代码的时候，会等很久的时间，然后会返回错误:"fatal: unable to access 'http://192.168.80.137:8081/quanhong/testapp.git/': The requested URL returned error: 504"