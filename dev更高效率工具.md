<!--
 * @Descripttion: 
 * @version: 
 * @Author: wenq
 * @Date: 2019-08-24 22:56:42
 * @LastEditors  : wenq
 * @LastEditTime : 2020-02-07 10:47:29
 -->
# 日常开发工作，总有一些不方便的地方、这里就是相关解决方案的集合

## 1.[20190824]家中使用npm很慢？
方案：用taobao的npm镜像代替即可;
具体操作：
修改本地npm获取包的服务端地址
```
npm config set registry https://registry.npm.taobao.org

npm config set disturl https://npm.taobao.org/dist --global
```
参考连接：
[传送门](https://www.cnblogs.com/jiqing9006/p/8391964.html)

## 2.[20200207] 本地开发怎样配置多个ssh(git链接方式之一)用于不同git服务器？比如一个github，一个gitlab等？
答：
本机环境：window10
远程服务器环境：github.com、 git.xxx.com(独立第三方gitlab服务器)
配置思路：1.xxx、2.xxx、3.xxxx、4.xxxx
具体执行指令：??

## 3.[20200207] 本地全局git配置的用户名/邮箱('.gitconfig'文件)怎样支持多个账户配置？ 即不同项目有不同用户名/邮箱
答：

