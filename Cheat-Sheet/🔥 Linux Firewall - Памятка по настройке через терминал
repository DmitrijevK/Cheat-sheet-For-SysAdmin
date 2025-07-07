Настройка брандмауэра в Linux с использованием `ufw`, `iptables` и `firewalld`.

---

## ✅ UFW (Uncomplicated Firewall) — для Ubuntu/Debian

Простой и удобный фаервол по умолчанию в Ubuntu.

### 🔧 Основные команды

- `sudo ufw status` — проверить статус
- `sudo ufw enable` — включить фаервол
- `sudo ufw disable` — выключить фаервол
- `sudo ufw default deny incoming` — по умолчанию блокировать входящие
- `sudo ufw default allow outgoing` — разрешить исходящие

### ➕ Разрешить соединения

- `sudo ufw allow ssh` — разрешить SSH (порт 22)
- `sudo ufw allow 80/tcp` — HTTP
- `sudo ufw allow 443/tcp` — HTTPS
- `sudo ufw allow 22` — любой протокол, порт 22
- `sudo ufw allow from 192.168.1.0/24 to any port 22` — доступ по SSH из подсети

### ➖ Заблокировать соединения

- `sudo ufw deny 21` — блокировать FTP
- `sudo ufw reject 23` — блокировать Telnet (с ответом)

### ❌ Удалить правило

- `sudo ufw delete allow 22`

---

## 🧱 iptables — классический фаервол (гибкий, но сложнее)

### 📋 Проверка и сброс

- `sudo iptables -L -v` — список правил
- `sudo iptables -F` — удалить все правила

### ➕ Примеры правил

- `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT` — разрешить SSH
- `sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT` — разрешить HTTP
- `sudo iptables -A INPUT -i lo -j ACCEPT` — разрешить loopback
- `sudo iptables -A INPUT -m conntrack --ctstate ESTABLISHED,RELATED -j ACCEPT` — разрешить существующие соединения
- `sudo iptables -P INPUT DROP` — по умолчанию блокировать всё входящее

### 💾 Сохранение правил

Debian/Ubuntu:
```bash
sudo apt install iptables-persistent
sudo netfilter-persistent save

```

## 🔥 firewalld — Red Hat / CentOS / Fedora

Современная замена `iptables`, основанная на зонах.

### ▶️ Управление

- `sudo systemctl start firewalld`
    
- `sudo systemctl enable firewalld`
    
- `sudo firewall-cmd --state` — статус
    

### ➕ Разрешения

- `sudo firewall-cmd --add-service=http --permanent`
    
- `sudo firewall-cmd --add-port=8080/tcp --permanent`
    
- `sudo firewall-cmd --reload`
    

### 🔍 Просмотр

- `sudo firewall-cmd --list-all`
    
- `sudo firewall-cmd --list-ports`

## 📌 Общие советы

- Всегда **разрешай SSH** перед включением фаервола:
```
sudo ufw allow ssh
sudo ufw enable
```

- Для тестов сначала используй временные правила (без `--permanent`).
    
- После изменения конфигурации перезагружай фаервол:
    
    - `sudo ufw reload`
        
    - `sudo firewall-cmd --reload`

