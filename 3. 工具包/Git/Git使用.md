### Git 代码合并

dev1.0 合并到 dev

~~~shell
git checkout dev
git merge dev1.0
~~~



Q: 代码合并失败，报错：`refusing to merge unrelated histories`

~~~shell
git merge develop --allow-unrelated-histories
~~~

