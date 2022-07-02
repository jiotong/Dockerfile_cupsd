＃＃ 概述
##Docker版CUPS 打印服务器和打印驱动程序。

## 运行 Cups 服务器
使用默认的cupsd.conf配置文件：
```bash
docker run -d \
  --name cupsd \
  --restart unless-stopped \
  -dp 631:631 \
  --privileged \
  -v /var/run/dbus:/var/run/dbus \
  -v /dev/bus/usb:/dev/bus/usb \
  greedcrow/cupsd:2.3.3op
```

使用自定义 cupsd.conf 配置文件：
```bash
--name cupsd \
  --restart unless-stopped \
  -dp 631:631 \
  --privileged \
  -v 自定义配置cupsd.conf文件位置:/etc/cups/cupsd.conf
  -v /var/run/dbus:/var/run/dbus \
  -v /dev/bus/usb:/dev/bus/usb \
  greedcrow/cupsd:2.3.3op
```


## 将打印机添加到 Cups 服务器
1. 在 [http://ip:631](http://ip:631) 连接到 Cups 服务器
2. 添加打印机：管理 > 打印机 > 添加打印机

__注意__：Cups 服务器的管理员用户/密码是`print`/`print`

## 在你的机器上配置 Cups 客户端
1. 安装`cups-client`包
2. 编辑`/etc/cups/client.conf`，设置`ServerName`为`ip:631`
3. 使用 `lpstat -r` 测试与 Cups 服务器的连接性
4. 使用 `lpstat -v` 测试是否检测到打印机
5. 您机器上的应用程序现在应该可以检测到打印机了！
