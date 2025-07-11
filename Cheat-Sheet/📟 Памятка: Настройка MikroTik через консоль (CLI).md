

> Мини-шпаргалка по базовой настройке MikroTik через командную строку. Удобно использовать при первичной настройке или в экстренной ситуации.

---

## 🔑 Изменение пароля администратора

```bash
/user set admin password=НОВЫЙ_ПАРОЛЬ
```

## 🌐 Назначение IP-адреса на интерфейс

```bash
/ip address add address=192.168.88.1/24 interface=ether1
```

## 🚪 NAT (маскарадинг для выхода в интернет)

```
/ip firewall nat add chain=srcnat action=masquerade out-interface=ether1

```

## 📶 DHCP-сервер
```bash

/ip pool add name=dhcp_pool ranges=192.168.88.10-192.168.88.100

/ip dhcp-server add name=dhcp1 interface=ether2 address-pool=dhcp_pool disabled=no

/ip dhcp-server network add address=192.168.88.0/24 gateway=192.168.88.1

/ip dhcp-server enable dhcp1
```

## ⛓ Firewall: базовые правила безопасности
```bash
/ip firewall filter add chain=input connection-state=established,related action=accept
/ip firewall filter add chain=input protocol=icmp action=accept
/ip firewall filter add chain=input in-interface=ether1 action=drop
```

## 📡 Проверка состояния

```bash
/interface print
/ip address print
/ip route print
```

## 💾 Резервное копирование конфигурации

```bash
/system backup save name=backup_имя
```

## Установка своих DNS серверов и отключение получения их по DHCP

```bash
/ip dns set servers=8.8.8.8,1.1.1.1
/ip dhcp-client set [find ] use-peer-dns=no
```

## Настройка синхронизации времени по NTP и MikroTik Cloud Time

```bash
/system ntp client set enabled=yes server-dns-names=time.google.com,0.pool.ntp.org,1.pool.ntp.org,2.pool.ntp.org,3.pool.ntp.org /system clock set time-zone-autodetect=no 
/system clock set time-zone-name=Europe/Moscow 
/ip cloud set update-time=yes
```

## Заблокировать доступ к WiFi по MAC-адресу
```bash
/interface wireless access-list authentication=no mac-address=8A:EA:B7:2E:38:C1
```

## Включение пробросов портов SSH
```bash
/ip ssh set forwarding-enabled=both
```
