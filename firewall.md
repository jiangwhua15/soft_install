#### 端口转发命令

```
firewall-cmd --add-forward-port=port=5556:proto=tcp:toport=5555:toaddr=8.212.144.66 --permanent
firewall-cmd --add-forward-port=port=5557:proto=tcp:toport=5555:toaddr=8.212.183.110 --permanent
```