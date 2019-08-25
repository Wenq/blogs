# 日常开发工作，总有一些不方便的地方、这里就是相关解决方案的集合

# 1.[20190824]家中使用npm很慢？
方案：用taobao的npm镜像代替即可;
具体操作：
修改本地npm获取包的服务端地址
```
npm config set registry https://registry.npm.taobao.org

npm config set disturl https://npm.taobao.org/dist --global
```
参考连接：
https://www.cnblogs.com/jiqing9006/p/8391964.html

# 2.[]