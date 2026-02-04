---
title: 隐藏目录与cd命令
---

# 隐藏目录与cd命令

我们都知道在Linux系统中有一种特殊的文件或目录——以"."开头的隐藏文件或目录。

我们还知道cd命令有种用法是`cd ..`来快速回到上级目录。

我们可以发现它们都与"."有关，其实它们有着巧妙的关系。



我们新建一个空白目录，cd进入后用`ll -a`可以发现有两个隐藏目录：

```shell
[root@kf-zgttslyypt-tyszr-xzzs test]# ll -a
total 8
drwxr-xr-x 2 root root 4096 Sep 23 09:52 .
drwxr-xr-x 3 root root 4096 Sep 23 09:52 ..
```

`.`：代表**当前目录**，也就是 `unzip-area` 这个目录本身。

`..`：代表**上一级目录**。

所以我们可以通过`cd ..`来方便的回到上级目录。



那我们把`..`目录删除呢？[坏笑]

很遗憾，即使是`rm - rf`也无法删除

```shell
[root@kf-zgttslyypt-tyszr-xzzs test]# rm -rf ..
rm: refusing to remove ‘.’ or ‘..’ directory: skipping ‘..’
```

