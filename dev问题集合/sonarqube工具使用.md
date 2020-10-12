<!--
 * @Descripttion: 
 * @version: 
 * @Author: wenq
 * @Date: 2020-10-12 23:39:12
 * @LastEditors: wenq
 * @LastEditTime: 2020-10-12 23:46:53
-->
# sonarqube源代码质量检测工具使用

### `2020/10/12`
### sonarqube工具运作原理：

参考[链接](https://www.imooc.com/article/279446?block_id=tuijian_wz)

sonarqube使用:
1. sonarqube主程序 --需要配置myslq链接信息、
2. sonarqube-scanner扫描程序 --需要配置myslq链接信息 + window系统高级变量、
3. Mysql数据库、

运作方式：
1. 主程序用于扫描相关信息管理，比如用户登录，扫描内容，扫描结果呈现等，是一套web程序，相关数据存储在mysql数据库、
2. scanner扫描程序用于扫描特定目录源代码（各种开发语言源代码）