# 🦍 Gobuster — Памятка

Gobuster — это CLI-инструмент на Go для быстрого brute-force анализа веб-ресурсов с использованием словарей.

---

## 📦 Установка

### Debian / Ubuntu

```bash
sudo apt update
sudo apt install gobuster
```

| Флаг         | Описание                          |
| ------------ | --------------------------------- |
| `-u`         | URL цели                          |
| `-w`         | Путь к словарю                    |
| `-x`         | Расширения файлов (через запятую) |
| `-t`         | Кол-во потоков (по умолч. 10)     |
| `-o`         | Сохранить вывод в файл            |
| `--no-error` | Отключить вывод ошибок            |

## Примеры:
gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt
gobuster dir -u http://example.com -w wordlist.txt -x php,html -t 50 -o result.txt

## 🌐 Режим 2: Поиск поддоменов (dns)
gobuster dns -d target.com -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt

| Флаг         | Описание                 |
| ------------ | ------------------------ |
| `-d`         | Домен                    |
| `-w`         | Словарь с поддоменами    |
| `-t`         | Кол-во потоков           |
| `--wildcard` | Обнаружение wildcard DNS |

 gobuster s3 -w wordlist.txt



## 📚 Словари (wordlists)
Стандартные пути:

    `/usr/share/wordlists/dirb/common.txt`

    `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

    `/usr/share/wordlists/rockyou.txt.gz (разархивировать)`

    `/usr/share/seclists/ (если установлен)`

## 💡 Советы
```
    Используй -x для указания расширений файлов: -x php,html,txt

    Используй --wildcard при сканировании поддоменов

    Начни с малого словаря (common.txt), потом переходи к большому (SecLists)

    Увеличивай потоки (-t) для ускорения, но следи за rate-limit’ами
```
