# 1.push了代码到github，为什么在个人首页可视化统计图表里看不到？
答：因为你提交代码的邮箱地址与你自己账号对应的邮箱地址不一致？（暂不确定）

# 2.怎样查看全局git提交账号信息配置？
答：`git config --list` 或者 `git config --global user.name / git config --global user.email`

## 更多信息参考帖子：  [git命令：全局设置用户名邮箱配置](https://www.cnblogs.com/vae860514/p/8203455.html)
```
1、查看git配置信息
git config --list

2、查看git用户名
git config user.name

3、查看邮箱配置
git config user.email

4、配置全局用户名
git config --global user.name "你的用户名"

5、配置全局邮箱
git config --global user.email "你的邮箱地址"
```