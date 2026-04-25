# 🧠 DeepSeek Anti-recall

[![Version](https://img.shields.io/badge/version-2026.04.25-orange.svg)](https://greasyfork.org/ru/scripts/)
[![Platform](https://img.shields.io/badge/platform-Tampermonkey-black.svg)](https://www.tampermonkey.net/)
[![Tested On](https://img.shields.io/badge/tested--on-Chrome-blue.svg)](https://www.google.com/chrome/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](https://opensource.org/licenses/MIT)

> [!TIP]
> **Russian description is available below.** > [Прокрутить к описанию на русском языке](#-deepseek-anti-recall-защита-от-цензуры-и-сохранение-контекста)

---

> [!IMPORTANT]
> This script requires a userscript manager such as **Tampermonkey** or **Violentmonkey**. 
> It has been tested exclusively on **Google Chrome** and is provided **"as is"** without any warranties.

## 📖 Overview

**DeepSeek Anti-recall** is a robust anti-censorship tool designed for the DeepSeek web interface. It prevents the loss of information when the AI triggers a content filter, allowing you to maintain a seamless conversation flow even when parts of it are "recalled" by the platform.

### ⚠️ The Problem
When DeepSeek generates a response that fails internal safety filters (`CONTENT_FILTER` or `TEMPLATE_RESPONSE`), the platform forcibly hides or deletes it. This breaks the context, making the AI "forget" the previous exchange.

---

## ✨ Key Features

* **⚡ Instant Interception:** Uses robust SSE (Server-Sent Events) parsing to capture text fragments in real-time before the platform's deletion script can trigger.
* **🔄 Shadow Context (Re-injection):** Rescued responses are saved and automatically appended to your subsequent queries. The AI "remembers" what was censored.
* **🧠 Thinking Storage:** Accurately extracts and stores the AI's reasoning process (`<thinking>` blocks) separately.
* **🖥️ Custom UI & Notifications:**
    * **Inline Banners:** Replaces censored messages with informative yellow tips.
    * **Management Widget:** A floating control panel to view or clear the saved shadow context.
* **🛠️ Developer Controls:** Access internal states and cache via `window.__dsAR` in the console.
* **🛡️ Privacy First:** All data is stored locally in your browser's `localStorage`. No external servers involved.

---

## ⚙️ How It Works

1.  **Intercept:** The script hooks into `fetch` and `XMLHttpRequest` to monitor the data stream.
2.  **Capture:** It accumulates message fragments in a local buffer.
3.  **Detect:** If a `CONTENT_FILTER` flag is detected, the script prevents the UI from clearing the message and saves the buffer.
4.  **Inject:** Upon your next message, the script prepends a `<recalled_exchange>` block to your prompt, restoring the AI's memory.

---

## 🚀 Installation

1.  Install a userscript manager (e.g., [Tampermonkey](https://www.tampermonkey.net/)).
2.  Create a new script and paste the code from `script.js` (or install via GreasyFork).
3.  Refresh your DeepSeek chat page.
4.  Check the Tampermonkey menu for configuration options.

---

## 📝 Important Notes

* **Token Consumption:** Re-injecting context increases prompt length. Use the **"Clear"** button in the banner when the old context is no longer relevant.
* **Compatibility:** Optimized for the latest web version of DeepSeek.
* **I18n:** Automatically switches between English and Russian based on browser settings.

---
---

## 🧠 DeepSeek Anti-recall (Защита от цензуры и сохранение контекста)

### 📖 Описание
Мощный скрипт для обхода цензуры в веб-версии DeepSeek. Перехватывает удаленные сообщения, сохраняет их локально и автоматически подмешивает в контекст ваших следующих запросов, чтобы нейросеть «помнила» заблокированные ответы.

### 🛠 Главные функции
* **🚀 Мгновенный перехват:** Надежный парсинг SSE-потока в реальном времени. Спасает текст до того, как сработает скрипт удаления.
* **🔄 Теневой контекст:** Сохраненные ответы незаметно добавляются к вашим следующим сообщениям. DeepSeek продолжает диалог, опираясь на заблокированный текст.
* **🧠 Сохранение мыслей:** Корректно извлекает процесс рассуждений нейросети (`<thinking>`). Можно настроить их повторную отправку в контекст.
* **🖥️ Интерфейс и уведомления:**
    * **Желтые баннеры:** Наглядные уведомления на месте заблокированных сообщений.
    * **Виджет управления:** Плавающая панель для просмотра (👁) и очистки (🗑) теневого контекста.
* **🛡️ Приватность:** Работает полностью локально. Данные хранятся только в `localStorage` вашего браузера.

### ⚙️ Как это работает
1.  Скрипт перехватывает пакеты данных в момент генерации.
2.  При фиксации события цензуры блокируется команда на удаление сообщения.
3.  Локальная копия текста сохраняется в кэш сессии.
4.  При отправке нового сообщения скрипт формирует блок `<recalled_exchange>` и внедряет его перед вашим текстом.

### 📝 Примечания
* **Лимиты токенов:** Теневой контекст увеличивает размер промпта. Не забывайте нажимать «Очистить», когда старый контекст больше не нужен.
* **История:** Полная поддержка восстановления истории (`/history_messages`) при перезагрузке страницы.

---

**Author:** [CATLYS]  
**License:** MIT
