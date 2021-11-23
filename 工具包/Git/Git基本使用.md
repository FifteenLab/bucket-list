## Git 基础

### Git 安装&卸载



### Git常用命令

~~~shell
# 克隆项目
git clone <git地址>
# 下载代码
git pull
# 添加
git add .
# 提交
git commit -m "commit message"
# 上传代码
git push
# 切换分支
git checkout <branch-name>
# 代码合并
git merge <branch-name>
~~~

#### git  merge

dev1.0 合并到 dev

~~~shell
git checkout dev
git merge dev1.0
~~~

##### 坑点

1、代码合并失败，报错：`refusing to merge unrelated histories`

~~~shell
git merge develop --allow-unrelated-histories
~~~

