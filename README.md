git clone git@github.com:xiaohuanwang/xiaohuanwang.github.io.git ./huanBlog

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

npm i -g @cloudbase/cli
cloudbase login

cloudbase hosting deploy public -e blog-2gbsc2o321c689df
