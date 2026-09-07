<h1 align="center">TG WS Proxy iOS (Workflow Fix Fork)</h1>

<h4 align="center">Локальный MTProto-прокси для Telegram на iOS с Rust-ядром, WidgetKit, Live Activity и опциональным Packet Tunnel. Сборка через GitHub Actions.</h4>

<p align="center">
  <a href="docs/README.md">English</a>
</p>

<p align="center">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-GPLv3-blue?style=for-the-badge&logo=gnu&logoColor=white" alt="GPLv3"></a>
  <img src="https://img.shields.io/badge/iOS-17%2B-black?style=for-the-badge&logo=apple&logoColor=white" alt="iOS 17+">
  <img src="https://img.shields.io/badge/Swift-SwiftUI-F05138?style=for-the-badge&logo=swift&logoColor=white" alt="SwiftUI">
  <img src="https://img.shields.io/badge/Core-Rust-000000?style=for-the-badge&logo=rust&logoColor=white" alt="Rust">
</p>


---

**TG WS Proxy iOS** запускает Rust-версию TG WS Proxy на iPhone и предоставляет Telegram локальный MTProto endpoint:

```text
Telegram → 127.0.0.1:1443 → Rust TG WS Proxy → WSS / Cloudflare → Telegram DC
```

> [!CAUTION]
> **Это экспериментальный сетевой инструмент. Он работает, но ошибочная конфигурация Packet Tunnel может полностью «убить» интернет на устройстве до отключения VPN, переустановки приложения или перезагрузки iPhone. Приложение не проходило аудит безопасности. Используйте только на свой риск и не устанавливайте IPA из источников, которым не доверяете.**
---

## 🤖 Отказ от ответственности / AI Disclaimer
> [!NOTE]
> Все исправления сборочных скриптов, патчи компилятора Xcode 16.2+, обходы песочницы iOS и настройка CI/CD автоматизации в этом форке были реализованы в плотном соавторстве с нейросетью **Gemini AI**. Автор делал всё возможное для достижения стабильности, но за любые скрытые ошибки, утечки памяти Rust-ядра или будущие поломки из-за обновлений Apple ответственности не несёт. Используйте на свой страх и риск!

---

## ⚡ Особенности этого форка (Исправления сборки)
В данном репозитории исправлены критические ошибки компиляции оригинального проекта под свежие версии Xcode (16.2+), убран падающий модификатор интерфейса `.glassEffect`, а также добавлены автоматические скрипты для облачной сборки через **GitHub Actions** без наличия компьютера Mac. 

---

## ✨ Возможности

- локальный MTProto-прокси на Rust;
- Cloudflare Workers, пользовательский домен и обновляемый список доменов;
- размеры WebSocket-пула `2`, `4` или `6`;
- статистика трафика, состояние пула, логи и диагностика;
- Liquid Glass с возможностью отключения;
- Live Activity и Dynamic Island одним компонентом `la`;
- интерактивный Home Screen Widget;
- системный toggle для Control Center;
- App Intents и Siri Shortcuts;
- deep links для запуска, остановки и настройки;
- RU/EN интерфейс;
- автоматический fallback на loopback, если Packet Tunnel недоступен.

---

## 📦 Ограничения установки на Бесплатный Apple ID (Важно!)

При попытке использовать приложение на бесплатном аккаунте разработчика (Free Apple ID) через `iloader` или `Sideloadly` вы столкнетесь со следующими системными ограничениями песочницы iOS:

1. **Лимит App ID (Ошибка 0 available):** Полная сборка со всеми расширениями (`-c wd,la,cc,vpn`) требует регистрации множества уникальных идентификаторов в Apple. Из-за лимитов бесплатного аккаунта установка может упасть. **Решение:** используйте абсолютно новый, чистый Apple ID.
2. **Проблема 8 секунд (Падение VPN):** Если собрать полную версию с флагом `vpn`, приложение успешно запустится, но ровно через 8-30 секунд трафик затухнет. Система iOS блокирует инициализацию сетевых настроек (`NetworkExtension`) для бесплатных сертификатов и обрывает сокет. Стабильная работа в режиме VPN на бесплатном аккаунте возможна **только при постоянном ручном перезапуске приложения**.
3. **Рекомендуемый стабильный режим:** Для непрерывной работы без вылетов компилируйте проект с флагом **`-c la`** (только Live Activity) и активированным в коде патчем маскировки под плеер (`audio`). Подключайте Telegram локально через ручной ввод прокси на адрес **`127.0.0.1:1443`**.

---

## 🚀 Облачная сборка (GitHub Actions)

Вам не нужен Mac или установленный Xcode. Всё собирается в облаке:
1. Перейдите во вкладку **Actions** вашего репозитория.
2. Выберите воркфлоу **Build iOS IPA**.
3. Нажмите кнопку **Run workflow**.

Вы можете выбрать флаги сборки внутри `.github/workflows/build.yml`:
- `-c la` — Облегченная стабильная версия с Живой активностью (Рекомендуется).
- `-c wd,la,cc,vpn` — Полная ультимативная версия (Требует платный аккаунт или TrollStore).

Готовый `.ipa` файл будет доступен для скачивания в разделе **Artifacts** после успешного завершения сборки.

---

## 🧬 Происхождение и благодарности

- [Flowseal/tg-ws-proxy](https://github.com/Flowseal/tg-ws-proxy) — оригинальный проект и основная идея;
- [amurcanov/tg-ws-proxy-android](https://github.com/amurcanov/tg-ws-proxy-android) — Rust-ядро и Android-форк, используемые как upstream;
- [IMDelewer/tg-ws-proxy-ios](https://github.com/reekeer/tg-ws-proxy-ios) — оригинальная iOS-оболочка и интеграция Apple frameworks.

---

## 🔗 Deep links
```text
tgwsproxy://home
tgwsproxy://settings
tgwsproxy://?action=start
tgwsproxy://?action=stop
```
*(Полный список deep-links доступен в оригинальной документации проекта).*

---

## ⚖️ Лицензии

- Этот объединённый проект и все модификации распространяются по лицензии [GPLv3](LICENSE).
- Названия Telegram и Apple принадлежат соответствующим правообладателям. Проект не аффилирован с Telegram FZ-LLC или Apple Inc.

<p align="center"><sub>Модификацию и исправление воркфлоу подготовил <a href="https://github.com">Adolfsmikler</a></sub></p>
