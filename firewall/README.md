### [返回目录][main_url]
#### Firewall 防火墙命令
##### 一、[端口转发](#端口转发)

```
firewall-cmd --add-forward-port=port=5556:proto=tcp:toport=5555:toaddr=*.*.*.* --permanent
firewall-cmd --add-forward-port=port=5557:proto=tcp:toport=5555:toaddr=*.*.*.* --permanent
```


[main_url]: https://github.com/jiangwhua15/soft_install
