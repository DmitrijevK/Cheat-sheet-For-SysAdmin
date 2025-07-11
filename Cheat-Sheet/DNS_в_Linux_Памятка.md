Полезные команды и настройки для работы с DNS: диагностика, конфигурация и проверка.

---

## 📌 Что такое DNS?

DNS (Domain Name System) — это система, которая преобразует доменные имена (например, `google.com`) в IP-адреса (например, `142.250.190.14`), необходимые для маршрутизации трафика в интернете.

---

## 🧪 Проверка и диагностика DNS

### 🔍 Базовая информация

```bash
hostname         # имя хоста
hostname -I      # IP-адреса системы
```

🌍 Получение DNS-записей
```
dig google.com              # полный DNS-запрос
dig +short google.com       # только IP-ответ
dig MX gmail.com            # MX-записи
dig @8.8.8.8 google.com     # через определённый DNS-сервер
dig +trace google.com       # трассировка от корня
nslookup google.com         # альтернатива dig
host google.com             # простой и быстрый способ IP

```

## ⚙️ Настройка DNS-клиента

### 📁 /etc/resolv.conf
```
nameserver 8.8.8.8
nameserver 1.1.1.1
```

### 🧭 systemd-resolved (современный способ)

- Проверить активные DNS:
```
resolvectl status
```

Назначить DNS для интерфейса:
```
sudo resolvectl dns eth0 8.8.8.8 1.1.1.1
```


Установить домен поиска:
```
sudo resolvectl domain eth0 example.com

```

🧼 Очистка DNS-кеша
```
sudo systemd-resolve --flush-caches    # для systemd-resolved
sudo killall -HUP dnsmasq              # для dnsmasq
sudo service nscd restart              # для nscd

```

📦 Установка утилит
```
sudo apt install dnsutils      # dig, nslookup, host
sudo apt install bind9-utils   # дополнительные инструменты

```

🔐 Проверка фильтрации
```
dig version.bind txt chaos @dns-сервер

```


## 🧠 Полезные советы

- **`dig +trace`** — незаменим при отладке DNS-цепочки.
    
- **`resolvectl`** — актуальный инструмент для systemd-систем.
    
- **`/etc/resolv.conf`** — вручную редактируй только при отключённом NetworkManager/systemd-resolved.
    
- Если DNS работает, а `ping` по имени не проходит — проблема часто в конфигурации `/etc/resolv.conf`.
