# 🧠 DeepSeek Anti-recall

[![Version](https://img.shields.io/badge/version-2026.04.25-orange.svg)](https://greasyfork.org/scripts/575367-deepseek-anti-recall)
[![Platform](https://img.shields.io/badge/platform-Tampermonkey-black.svg)](https://www.tampermonkey.net/)
[![Tested On](https://img.shields.io/badge/tested--on-Chrome-blue.svg)](https://www.google.com/chrome/)
[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-orange.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

<img width="939" height="549" alt="blocked" src="https://github.com/user-attachments/assets/f08495c5-e7e8-4e51-b419-7c328628983b" />

> [!TIP]
> **Описание на русском доступно ниже.** > [Прокрутить к описанию на русском языке](#-deepseek-anti-recall-защита-от-цензуры-и-сохранение-контекста)

---

> [!IMPORTANT]
> This script requires a userscript manager such as **Tampermonkey** or **Violentmonkey**. 
> It has been tested exclusively on **Google Chrome** and is provided **"as is"** without any warranties. It is beta-version.
> [You can install it from Greasyfork](https://greasyfork.org/scripts/575367-deepseek-anti-recall)

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

## ⚖️ License

This project is licensed under [CC NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

* Attribution Waived: Although the base license is "BY", I officially waive the requirement for attribution. You are not required to give credit to the author.
* Non-Commercial (NC): You may not use this work for commercial purposes or for-profit activities.
* ShareAlike (SA): Any derivative works must be distributed under the same license terms.
* Open & Free: This software is provided for free and must remain open-source and free for everyone, forever.

---

# На русском

## 🧠 DeepSeek Anti-recall (Защита от цензуры и сохранение контекста)

> [!IMPORTANT]
> [Установить этот скрипт можно с Greasyfork](https://greasyfork.org/ru/scripts/575367-deepseek-anti-recall)
> Скрипт был протестирован на Chrome с установленным Tampermonkey и находится в beta-версии.

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

## ⚖️ Лицензия

Этот проект распространяется под лицензией [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).

* **Отказ от указания авторства:** Хотя базовая лицензия — «BY» (с указанием авторства), я официально отказываюсь от этого требования. Указывать автора **необязательно**.
* **Некоммерческое использование (NC):** Вы **не имеете права** использовать этот проект в коммерческих целях или для деятельности, направленной на получение прибыли.
* **Сохранение условий (SA):** Любые производные работы должны распространяться на тех же условиях и под той же лицензией.
* **Свобода и открытость:** Это программное обеспечение предоставляется бесплатно и должно оставаться открытым и бесплатным для всех навсегда.
