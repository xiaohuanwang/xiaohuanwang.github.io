git clone https://github.com/xiaohuanwang/xiaohuanwang.github.io.git ./huanBlog

cd huanBlog

npm install

hexo new xxxx

hexo clean

hexo g

hexo d

git pull

git add .

git commit -m 'xxxx'

git push

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

