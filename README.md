#概述
##Docker版CUPS 打印服务器和打印驱动程序。

##运行 Cups 服务器
使用默认的cupsd.conf配置文件：

docker run -d \
  --name cupsd \
  --restart unless-stopped \
  -dp 631:631 \
  --privileged \
  -v /var/run/dbus:/var/run/dbus \
  -v /dev/bus/usb:/dev/bus/usb \
  greedcrow/cupsd:2.3.3op

使用自定义 cupsd.conf 配置文件：
  --name cupsd \
  --restart unless-stopped \
  -dp 631:631 \
  --privileged \
  -v 自定义配置cupsd.conf文件位置:/etc/cups/cupsd.conf
  -v /var/run/dbus:/var/run/dbus \
  -v /dev/bus/usb:/dev/bus/usb \
  greedcrow/cupsd:2.3.3op

##将打印机添加到 Cups 服务器

通过http://ip:631连接到 Cups 服务器
添加打印机：管理 > 打印机 > 添加打印机
注意：Cups 服务器的管理员用户/密码是print/print
