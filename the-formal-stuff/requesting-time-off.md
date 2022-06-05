---
cover: >-
  https://images.unsplash.com/photo-1511497584788-876760111969?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=3432&q=80
coverY: 0
---

# APC-UPS

APC UPS 软件包apcupsd 对大部分 APC的Smart-APC都支持。

{% hint style="info" %}
**Good to know:** you can embed public links, like this Typeform, to make data capture a breeze!
{% endhint %}

apt install apcupsd&#x20;

apt install apcupsd-cgi 支持Http服务，可用浏览器查看UPS状态。



/etc/apcupsd/apcupsd.conf

```
UPSNAME Power
UPSCABLE usb
UPSTYPE apcsmart 
DEVICE /dev/apc-usb
LOCKFILE /var/lock
# 等待6秒才开始真正的ONBATTERY操作：如果电源只是短暂地发生瞬断则不做反应
ONBATTERYDELAY 6
# 当停电导致电池剩余容量低于8%时，立即执行关机操作
BATTERYLEVEL 5
# 当停电导致剩余容量低于3分钟时，立即执行关机操作
MINUTES 3
# 禁止按掉电时间为关机判断条件,缺省值是0
TIMEOUT 90
# 每5分钟（300s）警告一次登录的用户系统发生掉电
ANNOY 300
# 首次掉电后1分钟（60s）告知登录的用户发生掉电
ANNOYDELAY 60
# 禁止apcupsd关闭电源
KILLDELAY 0
# UPS在供电恢复后等待60秒再恢复对设备的供电
#WAKEUP 60
```

/etc/default/apcupsd

&#x20;`ISCONFIGURED` 的 `no` no 选项改为 `yes`

apcaccess `#`查看设备的状态

绑定USB串口

[https://blog.csdn.net/walleva96/article/details/78347612](https://blog.csdn.net/walleva96/article/details/78347612)

```
lsusb 查看
ls /dev 查看
```



/etc/udev/rules.d/local.rules

```
#Bus 002 Device 003: ID 0403:6001 Future Technology Devices International, Ltd FT232 Serial (UART) IC
ENV{ID_BUS}=="usb", ENV{ID_VENDOR_ID}=="0403", ENV{ID_MODEL_ID}=="6001", SYMLINK+="apc-usb"
```



{% embed url="https://2w3pnm4iy73.typeform.com/to/P228Ngvj" %}
