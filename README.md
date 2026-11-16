# FlatJack: firmware

**[English](#english)** | **[Українська](#українська)**

Released firmware of FlatJack, the ESP32 controller that reads JK-PB BMSes over RS485 and drives an Eltek Flatpack2 over CAN. This repository holds the firmware files only. The newest version is **0.7.1**.

Готові прошивки FlatJack, контролера на ESP32, який читає BMS JK-PB через RS485 і керує Eltek Flatpack2 через CAN. Тут лише файли прошивок. Найновіша версія: **0.7.1**.

## Versions / Версії

### 0.7.1

- Charge history over the last 2 hours
- The history's period buttons fit a narrow phone

- Історія заряду за останні 2 години
- Кнопки періоду історії вміщаються на вузькому телефоні

| | Update / Оновлення | First flash over USB / Перше прошивання через USB |
|---|---|---|
| ESP32 DevKit | [flatjack-v0.7.1.bin](v0.7.1/flatjack-v0.7.1.bin) | [flatjack-v0.7.1-full.bin](v0.7.1/flatjack-v0.7.1-full.bin) |
| Waveshare ESP32-S3-Touch-LCD-5B | [flatjack-v0.7.1-waveshare-s3.bin](v0.7.1/flatjack-v0.7.1-waveshare-s3.bin) | [flatjack-v0.7.1-waveshare-s3-full.bin](v0.7.1/flatjack-v0.7.1-waveshare-s3-full.bin) |

### 0.7.0

- New name FlatJack; in Home Assistant it is a new device
- Charge phases in plain words: charging, topping up, full
- How long the battery lasts, from the load history; more numbers

- Нова назва FlatJack; у Home Assistant це новий пристрій
- Фази простими словами: заряджання, дозаряджання, заряджено
- Прогноз, на скільки вистачить батареї; більше даних на головній

| | Update / Оновлення | First flash over USB / Перше прошивання через USB |
|---|---|---|
| ESP32 DevKit | [flatjack-v0.7.0.bin](v0.7.0/flatjack-v0.7.0.bin) | [flatjack-v0.7.0-full.bin](v0.7.0/flatjack-v0.7.0-full.bin) |
| Waveshare ESP32-S3-Touch-LCD-5B | [flatjack-v0.7.0-waveshare-s3.bin](v0.7.0/flatjack-v0.7.0-waveshare-s3.bin) | [flatjack-v0.7.0-waveshare-s3-full.bin](v0.7.0/flatjack-v0.7.0-waveshare-s3-full.bin) |

### 0.6.0

- Waveshare: firmware update from the screen, beside the version
- The board finds the new version itself and shows what is new
- Release files are now in a public repository

- Waveshare: оновлення прошивки з екрана, кнопка біля версії
- Плата сама знаходить нову версію й показує, що в ній нового
- Файли релізів тепер у публічному репозиторії

| | Update / Оновлення | First flash over USB / Перше прошивання через USB |
|---|---|---|
| ESP32 DevKit | [flatjack-v0.6.0.bin](v0.6.0/flatjack-v0.6.0.bin) | [flatjack-v0.6.0-full.bin](v0.6.0/flatjack-v0.6.0-full.bin) |
| Waveshare ESP32-S3-Touch-LCD-5B | [flatjack-v0.6.0-waveshare-s3.bin](v0.6.0/flatjack-v0.6.0-waveshare-s3.bin) | [flatjack-v0.6.0-waveshare-s3-full.bin](v0.6.0/flatjack-v0.6.0-waveshare-s3-full.bin) |

### 0.5.0

- Three languages: Ukrainian, English and Russian
- One language for the whole device: screen, web, Home Assistant

- Три мови: українська, англійська й російська
- Мова одна на весь пристрій: екран, веб, Home Assistant

| | Update / Оновлення | First flash over USB / Перше прошивання через USB |
|---|---|---|
| ESP32 DevKit | [flatjack-v0.5.0.bin](v0.5.0/flatjack-v0.5.0.bin) | [flatjack-v0.5.0-full.bin](v0.5.0/flatjack-v0.5.0-full.bin) |
| Waveshare ESP32-S3-Touch-LCD-5B | [flatjack-v0.5.0-waveshare-s3.bin](v0.5.0/flatjack-v0.5.0-waveshare-s3.bin) | [flatjack-v0.5.0-waveshare-s3-full.bin](v0.5.0/flatjack-v0.5.0-waveshare-s3-full.bin) |

## English

Each version has two files per board. The two boards' files are not interchangeable: the update page refuses a file built for the other board.

1. **First flash:** connect the ESP32 over USB.
   - In Chrome or Edge, open [ESP Tool](https://espressif.github.io/esptool-js/), press Connect, set Flash Address `0x0`, choose the first-flash file (`…-full.bin`) and press Program.
   - Or from a terminal: `esptool.py --chip esp32 write_flash 0x0 flatjack-vX.Y.Z-full.bin` (Waveshare: `--chip esp32s3` and its `-waveshare-s3-full.bin`).
2. **First start:** the ESP32 opens the Wi-Fi access point `FlatJack-XXXXXX` for 180 s. Connect to it and choose your network.
3. **Open the UI:** go to http://flatjack.local/ or the IP your router gave it. Versions up to 0.6.0 were built under the project's old name: their access point is `JK-FP-XXXXXX` and their address http://jk-fp.local/.
4. **Updates:**
   - Waveshare board with firmware newer than 0.6.0, from its screen: Settings → the download button beside the version. It finds the newest version here, shows what is new and installs it.
   - Any board, from the web UI: System tab → Firmware update → choose your board's update file → Update.

Settings, Wi-Fi and history are kept. Every update restarts the ESP32, and the charger then starts again from Bulk.

`latest.json` is what the on-board update reads: the newest version and its notes in three languages.

## Українська

У кожної версії по два файли на плату. Файли двох плат не взаємозамінні: сторінка оновлення відхиляє файл, зібраний для іншої плати.

1. **Перше прошивання:** під'єднайте ESP32 через USB.
   - У Chrome або Edge відкрийте [ESP Tool](https://espressif.github.io/esptool-js/), натисніть Connect, вкажіть Flash Address `0x0`, виберіть файл першого прошивання (`…-full.bin`) і натисніть Program.
   - Або в терміналі: `esptool.py --chip esp32 write_flash 0x0 flatjack-vX.Y.Z-full.bin` (Waveshare: `--chip esp32s3` і файл `-waveshare-s3-full.bin`).
2. **Перший запуск:** ESP32 на 180 с відкриває точку доступу Wi-Fi `FlatJack-XXXXXX`. Під'єднайтеся до неї й виберіть свою мережу.
3. **Інтерфейс:** відкрийте http://flatjack.local/ або IP, який видав роутер. Версії до 0.6.0 включно зібрані під старою назвою проєкту: їхня точка доступу `JK-FP-XXXXXX`, адреса http://jk-fp.local/.
4. **Оновлення:**
   - плата Waveshare з прошивкою, новішою за 0.6.0, з її екрана: «Налаштування» → кнопка завантаження біля версії. Вона знаходить тут найновішу версію, показує, що нового, і встановлює її.
   - будь-яка плата, з веб-інтерфейсу: вкладка «Система» → «Оновлення прошивки» → виберіть файл оновлення для своєї плати → «Оновити».

Налаштування, Wi-Fi та історія зберігаються. Кожне оновлення перезапускає ESP32, і заряджання знову починається з Bulk.

`latest.json` читає оновлення з екрана: найновіша версія та її опис трьома мовами.
