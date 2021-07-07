# git将一个分支完全覆盖另外一个分支如：stable分支代码完全覆盖brush分支

当前分支是maser分支，我想将stable分支上的代码完全覆盖brush分支，首先切换到brush分支。

`git reset --hard origin/stable`

执行上面的命令后brush分支上的代码就完全被stable分支上的代码覆盖了（本地分支），然后将本地分支强行推到远程分支。

`git push -f`

出处：https://www.cnblogs.com/wangshuazi/p/10243005.html