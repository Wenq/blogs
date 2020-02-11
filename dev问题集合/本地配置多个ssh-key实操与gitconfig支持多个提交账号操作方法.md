<!--
 * @Descripttion: 
 * @version: 
 * @Author: wenq
 * @Date: 2020-02-08 14:41:48
 * @LastEditors  : wenq
 * @LastEditTime : 2020-02-08 16:09:07
 -->
### 问题场景1： git本地怎样配置多个ssh-key？
### 问题场景2： 全局.gitconfig文件支持配置多个git账号用于提交内容吗？

### **背景说明**：
>* 本地环境：window10
>* 远程连接服务器环境：
`1.github.com（git官方服务器）`
`2.git.xxx.com(独立第三方gitlab服务器)`

### 1.[20200207] 本地开发怎样配置多个ssh-key(git链接方式之一)用于不同git服务器通信？ 比如一个github，一个gitlab等？
答：
1.ssh-key是做什么的？
答：ssh与http是git管理源代码的2种方式。
>* ssh方式是密钥加密的方式，本地git客户端持有`密钥`，git服务器持有`公钥(ssh配置项)`，密钥与公钥都是通过git指令(`ssh-gen`)生成。

>* 这里问题中的ssh-key是指代本地开发环境配置的密钥(注:本地密钥生成后要生效，需要将密钥添加到本地`密钥列表?`中去)。

2.本地怎样配置多个ssh-key？
答：
(这里以git.com、git.xxx.com2个git服务器为例)
配置思路：
1.通过ssh-gen指令生成2副ssh-key(key文件名字不一样)、
2.将2副key的私钥加入本地私钥列表、
3.修改本地全局配置目录`xxx/.ssh`中的`config`文件,添加2个key配置，示例如下：
```
var config = key // config文件中配置示例数据？？
```
4.将2副ssh-key的公钥分别配置到各自所在git服务器中ssh项即可

3.整个配置过程具体执行指令如下示例： 
```
var config = key // 整个过程git指令示例数据？？
```
***`关键：`***
通过git指令生成多个ssh-key、
将key相关具体信息配置到本地全局配置文件`xxx/.ssh/config`中。

### 2.[20200207] 本地全局git配置的用户名/邮箱('.gitconfig'文件)怎样支持多个账户配置？ 即不同项目有不同用户名/邮箱
答：
1.全局.gitconfig文件所在文件路径？
答：与全局目录`xxx/.ssh`在同一文件夹下。
即：xxx/.ssh、xxx/.gitconfig
2.全局.gitconfig不支持配置多个用于提交的帐号信息，那不同项目怎样支持？
答：git全局配置文件之一的`.gticonfig`文件不支持同时配置多个提交帐号信息，且只允许配置一个全局帐号信息。
>* 怎样实现不同项目配置不同的提交信息？
在每个项目目录下配置自己的提交帐号信息即可。
>* 全局统一的提交帐号信息配置在全局配置文件.gitconfig中，而单个项目如果提交的帐号信息不同，可以在该项目下单独配置其提交帐号信息。
***配置方式有2种：使用git指令 或者 直接修改项目目录下隐藏的.git文件夹中的config文件***
git指令示例如下：
```
var config = key // git指令示例？？
```
直接修改config文件：
取消.git文件夹隐藏，直接修改config文件，修改数据示例如下：
```
var config = key // config文件中配置示例数据？？
```
***`关键`***
git提交帐号信息，优先从本地项目git配置中获取，没有则再从全局配置中获取
