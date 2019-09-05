# 查看端口信息
netstat -tnupl | grep 端口

``` 
-t (tcp) 仅显示tcp相关选项
-u (udp)仅显示udp相关选项
-n 拒绝显示别名，能显示数字的全部转化为数字
-l 仅列出在Listen(监听)的服务状态
-p 显示建立相关链接的程序名
```

# 解压文件

## zip

`unzip 压缩包 -d 指定文件夹`
