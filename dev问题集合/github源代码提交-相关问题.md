# 1.push了代码到github，为什么在个人首页可视化统计图表里看不到？
答：因为你提交代码的邮箱地址与你自己账号对应的邮箱地址不一致？（通过自身github账号+本地macbook客户端多个提交账号验证确认！）

# 2.怎样查看全局git提交账号信息配置？
答：`git config --list` 或者 `git config --global user.name / git config --global user.email`
## 更多信息参考帖子：  [git命令：全局设置用户名邮箱配置](https://www.cnblogs.com/vae860514/p/8203455.html)
```
1、查看git配置信息：git config --list

2、查看git用户名：
    2.1 git config user.name （如果在当前项目目录+项目有单独配合提交账号，则是当前项目的否则是全局的） 
    2.2 全局：git config --global user.name

3、查看邮箱配置：
    3.1 git config user.email（如果在当前项目目录+项目有单独配合提交账号，则是当前项目的否则是全局的） 
    3.2 全局：git config --global user.email

4、配置全局用户名：git config --global user.name "你的用户名"

5、配置全局邮箱：git config --global user.email "你的邮箱地址"
```

# 3.怎样为当前项目单独配置git提交账号信息，而不受全局影响？
答：在项目根目录使用`git config user.name 'xxx' / git config user.email 'xxxx@xx.com'`指令配置即可。
## 更多信息参考帖子： [git账号信息配置](https://www.cnblogs.com/xybxj/articles/5509429.html)

## git账号信息先后顺序说明： 
```
1. git提交账号信息在mac与window上控制规则基本一致，只是基于不同系统账号信息存储形式如目录等有差异

2. 本地安装了git客户端之后，一般都需要配置一个全局账号，后续提交代码都会默认使用这个账号

3. git支持全局统一账号信息A，同时单个项目也支持单个项目配置单独的账号信息B（在该项目根目录使用`git config user.name 'xxx'等即可设置`）

4. git在本地环境的配置不止全局账号A和单个项目账号B的配置级别，还支持更多层级配置（具体可阅读如上`git账号信息配置`链接文章）

5. 单独项目账号信息B优先与全局账号信息A
```