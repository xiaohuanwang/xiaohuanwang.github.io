## CentOS7 部署 hexo 

### 购买并备案域名

- 在阿里云、腾讯云等平台购买域名。
- 进行域名备案，因为在中国，使用域名访问网站前必须进行备案。

### 准备服务器

- 确保你有一台运行CentOS 7的服务器。
- 服务器需要连接到互联网，并且具有稳定的网络连接。

### 安装必要的软件

#### 安装Node.js

打开终端，执行以下命令来安装Node.js

```
sudo yum install epel-release  
sudo yum install nodejs
sudo yum install npm 
```

安装完成后，可以通过`node -v`和`npm -v`命令检查Node.js和npm是否安装成功。

> 查看当前的npm镜像设置：`npm config list`
>
> 清空缓存：`npm cache clean --force`
>
> 修改镜像即可：`npm config set registry https://registry.npmjs.org/`
>
> 推荐淘宝镜像，执行：`npm config set registry https://registry.npmmirror.com`

#### 安装Git

```
sudo yum install git
```

#### 安装Hexo

Hexo是一个快速、简洁且高效的博客框架，支持Markdown功能，并拥有强大的插件系统。

```
sudo npm install -g hexo-cli

git clone https://github.com/xiaohuanwang/xiaohuanwang.github.io.git ./huanBlog

cd huanBlog

npm install

```

> ### 1. 初始化网站
>
> - **命令**：`hexo init [folder]`
> - **说明**：用于初始化本地文件夹为Hexo网站的根目录。`[folder]`是可选参数，用以指定初始化目录的路径，若无指定则默认为当前目录。
>
> ### 2. 新建文章
>
> - **命令**：`hexo new [layout] <title>`
> - **简写**：`hexo n [layout] <title>`
> - **说明**：用于新建文章。`[layout]`是可选参数，用以指定文章类型，若无指定则默认由配置文件中的`default_layout`选项决定。`<title>`是必填参数，用以指定文章标题，如果标题中含有空格，则需要使用双引号包围。
>
> ### 3. 生成静态文件
>
> - **命令**：`hexo generate`
> - **简写**：`hexo g`
> - **说明**：用于生成静态文件。生成的静态文件默认存放在`public`目录中。可以使用`-d`选项指定生成后部署，与`hexo d -g`等价。
>
> ### 4. 启动本地服务器
>
> - **命令**：`hexo server`
> - **简写**：`hexo s`
> - **说明**：用于启动本地服务器，预览网站效果。默认情况下，服务器地址为`http://localhost:4000/`。可以使用`-p`选项指定服务器端口，默认为4000；使用`-i`选项指定服务器IP地址，默认为`0.0.0.0`；使用`-s`选项启用静态模式，仅提供`public`文件夹中的文件并禁用文件监视。
>
> ### 5. 部署网站
>
> - **命令**：`hexo deploy`
> - **简写**：`hexo d`
> - **说明**：用于将生成的静态文件部署到远程仓库。部署前需要修改`_config.yml`配置文件中的部署设置。例如，使用Git进行部署时，需要设置`type`为`git`，并指定`repo`（仓库URL）、`branch`（分支名）等参数。可以使用`-g`选项指定生成后部署，与`hexo g -d`等价。
>
> ### 6. 清理缓存
>
> - **命令**：`hexo clean`
> - **说明**：用于清理缓存文件（如`db.json`）和已生成的静态文件（`public`目录中的文件）。当网站显示异常或修改不生效时，可以尝试执行此命令。
>
> ### 7. 其他常用选项
>
> - **安全模式**：`hexo --safe`，用于禁用加载插件和脚本，安装新插件时遇到问题可尝试此操作。
> - **调试模式**：`hexo --debug`，用于将消息详细记录到终端和`debug.log`文件，便于调试。
> - **静默模式**：`hexo --silent`，用于静默输出到终端，减少不必要的输出信息。
>
> ### 注意事项
>
> - 在执行Hexo命令时，请确保当前目录是Hexo网站的根目录。
> - 修改`_config.yml`配置文件后，通常需要重启本地服务器才能预览效果。
> - 新建、删除或修改文章后，不需要重启Hexo服务器，刷新浏览器即可预览效果。

#### 安装Nginx

Nginx是一个高性能的HTTP和反向代理服务器

```
##安装Nginx
sudo yum install nginx
##启动Nginx服务
systemctl start nginx.service
##查看Nginx服务状态
systemctl status nginx.service
##重启Nginx服务
systemctl restart nginx.service
##停止Nginx服务
systemctl stop nginx.service
##设置其开机自启
sudo systemctl enable nginx
```

> [!CAUTION]
>
> ### 注意事项
>
> - 确保在执行重启操作前，Nginx服务正在运行。
> - 如果在尝试重启Nginx时遇到任何问题，首先检查Nginx的错误日志文件（通常位于`/usr/local/nginx/logs/error.log`或`/var/log/nginx/error.log`），以获取更多关于错误的信息。
> - 如果Nginx没有安装为systemd服务，或者你想将其添加到systemd管理，可以参考相关文档创建`nginx.service`文件，并将其放置在`/etc/systemd/system/`目录下，然后重新加载systemd的配置并启动服务。



#### 配置Nginx

编辑Nginx的配置文件（通常位于`/etc/nginx/nginx.conf`或`/etc/nginx/conf.d/`目录下的某个文件中）。

添加一个server块来配置你的域名和Hexo博客的静态文件目录。

```
server {  
    listen 80;  
    server_name 你的域名.com www.你的域名.com;  
 
    location / {  
        root /usr/local/hexo/public;   ##安装博客目录下的public文件夹
        index index.html index.htm;  
    }  
}
```

保存配置文件，并重新加载Nginx以使更改生效

```
sudo nginx -s reload
```

### 配置域名解析

1. **登录到你的域名注册商网站**。
2. **找到域名解析（DNS）设置部分**。
3. **添加一条A记录**，将你的域名指向你的服务器IP地址。
4. **（可选）添加一条CNAME记录**，如果你使用的是子域名，可以将其指向你的主域名。

#### Linux后台运行hexo

#### 首先安装pm2

```crystal
$ npm  install -g pm2
```

#### 写一个运行脚本，在博客根目录下面创建一个run.js

    //run
    const { exec } = require('child_process')
    exec('hexo server',(error, stdout, stderr) => {
            if(error){
                    console.log('exec error: ${error}')
                    return
            }
            console.log('stdout: ${stdout}');
            console.log('stderr: ${stderr}');
    })

#### cd到博客根目录下运行脚本

```crystal
# pm2 start run.js

pm2 start run.js	#启动
pm2 list	#查看pm2管理的所有服务

pm2 stop all	#停止pm2列表的所有服务
pm2 stop 0 #停止进程为0的进程

pm2 reload all #重新载入列表所有进程
pm2 reload 0 #重载列表中进程为0的进程

pm2 restart all	#重启列表中所有的进程
pm2 restart 0	#重启列表中进程为0的进程

pm2 delete 0	#删除列表中进程为0的进程
pm2 delete all	#删除列表中所有的进程
```

