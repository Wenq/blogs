# git操作：将一个分支完全覆盖另外一个分支？

## 如：用master分支代码完全覆盖baseline分支

### 当前分支是baseline分支，想要将master分支上的代码完全覆盖baseline分支，步骤如下：

步骤1.首先切换到baseline分支。

`git checkout baseline` //如果当前已经是baseline分支，可以跳过该步骤

步骤2.使用master分支代码内容覆盖baseline分支

`git reset --hard origin/master` //此操作会将你本地的代码完全替换为master分支代码（## 类似先清空本地baseline代码，然后把master代码拷贝过来 ##）

步骤3.执行上面的命令后，baseline分支上的代码就完全被master分支上的代码覆盖了（本地分支），然后将本地分支强行推到远程分支。

`git push -f`

（ 参考链接：https://www.cnblogs.com/wangshuazi/p/10243005.html ）

# 其他收获：
1. 依据代码分支A创建的tag：tag_A_01，在代码分支A被删除后，该tag依然存在。tag不依赖代码分支而存在，tag生成了就类似于单独拉了一个代码分支出来。


# git操作：git为什么会产生冲突？