<h1 align="center">TG WS Proxy iOS (Workflow Fix Fork)</h1>

<h4 align="center">Локальный MTProto-прокси для Telegram на iOS с Rust-ядром, Live Activity и встроенным Silent Audio обходом песочницы. Сборка через GitHub Actions.</h4>

<p align="center">
  <a href="docs/README.md">English 🌐</a>
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
> **Это экспериментальный сетевой инструмент. Используйте только на свой риск. Приложение не проходило аудит безопасности.**

---

## 🤖 Отказ от ответственности / AI Disclaimer
> [!NOTE]
> Все исправления сборочных скриптов, патчи компилятора Xcode 16.2+, обходы песочницы iOS и настройка CI/CD автоматизации в этом форке были реализованы в плотном соавторстве с нейросетью **Gemini AI**. Автор делал всё возможное для достижения стабильности, но за любые скрытые ошибки, утечки памяти Rust-ядра или будущие поломки ответственности не несёт.

---

## ⚡ Особенности этого форка (Что изменено)
В данном репозитории исправлены критические ошибки компиляции оригинального проекта под свежие версии Xcode (16.2+), убран падающий модификатор интерфейса `.glassEffect`, а также добавлены автоматические скрипты для облачной сборки через **GitHub Actions** без наличия компьютера Mac.

---

## 📦 Решение проблемы фонового режима на Бесплатном Apple ID (Важно!)

В оригинальном проекте фоновая работа на бесплатном аккаунте была невозможна: системный VPN (`NetworkExtension`) отваливался через 8 секунд из-за отсутствия платных энтайтлментов подписи [creative-writing-pad]. 

В данном форке внедрен **Автоматический патч Silent Audio Engine**, который полностью решает эту проблему [travel]! При сборке с флагом **`-c la`** скрипт автоматически вшивает в Swift-код генератор 

бесконечной тишины [travel]. Для iOS приложение выглядит как активный музыкальный плеер, что предотвращает заморозку процесса и позволяет Rust-ядру работать бесконечно [travel]!
### ⚠️ Известные компромиссы и баги (Нюансы хака):
1. **Повышенный жор батареи:** Поскольку звуковой движок и Rust-ядро работают в фоне непрерывно, телефон расходует заряд аккумулятора быстрее обычного [travel].
2. **Конфликт аудиосессий (Звонки и Запись):** Любое действие, задействующее микрофон или системный звук — сотовый звонок, VoIP-вызов, а также **запись голосовых сообщений или "кружков" (видеосообщений) в Telegram** — принудительно глушит наш фейковый аудио-поток [travel].
3. **Ручной перезапуск:** После окончания разговора или отправки голосового/видеосообщения прокси засыпает [travel]. **Необходимо перезапустить прокси вручную (нажать в приложении Stop -> Start)**, чтобы вернуть фоновую работу мессенджера.

---
## 🧬 Происхождение, источники и благодарности

Этот проект является результатом объединения, модификации и исправления цепочки опенсорс-решений:

- [Flowseal/tg-ws-proxy](https://github.com/Flowseal/tg-ws-proxy) — оригинальная концепция, идея обхода ограничений через WebSocket и базовое ядро прокси.
- [amurcanov/tg-ws-proxy-android](https://github.com/amurcanov/tg-ws-proxy-android) — активно развиваемый форк Rust-ядра и Android-версия, используемые в данном проекте как upstream для автоматической синхронизации.
- [reekeer/tg-ws-proxy-ios](https://github.com/reekeer/tg-ws-proxy-ios) — оригинальная графическая оболочка на Swift/SwiftUI и интеграция нативных фреймворков Apple.


## 🚀 Облачная сборка (GitHub Actions)

Вам не нужен Mac. Всё собирается в облаке:
1. Перейдите во вкладку **Actions** вашего репозитория.
2. Выберите воркфлоу **Build iOS IPA** и нажмите **Run workflow**.
3. Скачайте готовый `.ipa` из раздела **Artifacts** и установите через `iloader` или `Sideloadly` на пресете сборки `-p side -c la` [creative-writing-pad].

---

<p align="center"><sub>Модификацию и исправление воркфлоу подготовил <a href="https://github.com">Adolfsmikler</a></sub></p>
