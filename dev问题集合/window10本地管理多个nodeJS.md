<!--
 * @Descripttion: 
 * @version: 
 * @Author: wenq
 * @Date: 2020-02-12 14:23:38
 * @LastEditors  : wenq
 * @LastEditTime : 2020-02-14 09:30:08
 -->
### 本机环境：window10 64bit

### `问题场景`：根据不同文件或项目编译需要，本地会动态切换nodeJS版本
### `解决方法`：
>* 1.使用`gnvm`工具包在本地做不同nodeJS版本管理与动态切换。
>* 2.还有个`nvmw`工具包可以实现，暂时没有接触。

### gnvm使用方法如下：
网上有个帖子已经介绍非常详细，gnvm工具包使用方法 [传送门](https://www.cnblogs.com/zycb/p/10912736.html)

### 其他问题
>* 1.使用`npm install xxx`指令安装包速度慢？ 
答：使用taobao的npm镜像（`cnpm`指令工具可以不是必须的，只是修改获取包的路径）
>* 2.使用gnvm工具包指令`gnvm install xx.xx.x`安装nodeJS包速度慢？
答：gvnm启用内置的淘宝`TAOBAO`安装路径即可(具体启用指令见gnvm使用介绍)
`gnvm.exe内建了 DEFAULT and TAOBAO 两个库。`
```
注：'gnvm install xx1 xx2 xx3'指令是可以同时安装多个nodejs包的，包版本之间用空格分开
```
>* 3.使用gnvm工具切换了本地nodeJS版本，对应的npm工具也需要手动去更新为node对应版本，怎么安装或更新？
答：使用gnvm指令：`gnvm npm global`,即可自动安装与本地node版本最佳匹配的npm包
