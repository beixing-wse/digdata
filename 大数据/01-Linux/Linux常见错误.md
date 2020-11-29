# Linux常见错误

## 1 修改ip之后，重启network报错，错误信息为`systemctl status network.service" and "journalctl -xe" for details.`

解决：

观察日志发现有个 NetworkManager的网络服务组件，对他进行以下操作就可以了

```
[root@mina0 hadoop]# systemctl stop NetworkManager
[root@mina0 hadoop]# systemctl disable NetworkManager
```

然后：重启网卡

```
[root@mina0 hadoop]# systemctl restart network
[root@mina0 hadoop]# ifconfig
```

![image-20201031202908245](Linux常见错误.assets/image-20201031202908245.png)