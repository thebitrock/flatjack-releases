# Open-source components · Відкриті компоненти

The FlatJack firmware is built with these components. Each is under its own licence.

Прошивка FlatJack зібрана з цих компонентів. Кожен під своєю ліцензією.

| Component | Licence | Where |
|---|---|---|
| Arduino core for ESP32 | LGPL-2.1-or-later | https://github.com/espressif/arduino-esp32 |
| ESP-IDF (including FreeRTOS, lwIP, mbedTLS, NimBLE) | Apache-2.0, MIT, BSD and others, as in ESP-IDF | https://github.com/espressif/esp-idf |
| ESPAsyncWebServer | LGPL-3.0 | https://github.com/ESP32Async/ESPAsyncWebServer |
| AsyncTCP | LGPL-3.0 | https://github.com/ESP32Async/AsyncTCP |
| WiFiManager | MIT | https://github.com/tzapu/WiFiManager |
| ArduinoJson | MIT | https://github.com/bblanchon/ArduinoJson |
| espMqttClient | MIT | https://github.com/bertmelis/espMqttClient |
| LVGL (Waveshare build) | MIT | https://github.com/lvgl/lvgl |
| Montserrat font (Waveshare build) | SIL Open Font License 1.1 | https://github.com/JulietaUla/Montserrat |
| Noto Color Emoji, the language pictures (Waveshare build) | SIL Open Font License 1.1 | https://github.com/googlefonts/noto-emoji |

**LGPL.** Arduino-ESP32 (LGPL-2.1), ESPAsyncWebServer and AsyncTCP (LGPL-3.0) are linked statically. Each release has `flatjack-vX.Y.Z-relink.zip`: FlatJack's compiled object files and a PlatformIO project that builds the same firmware, so you can build it with your own modified version of these libraries. Their source: the versions named in that project, from the links above. Licence texts: [licenses/](licenses/).

**LGPL.** Arduino-ESP32 (LGPL-2.1), ESPAsyncWebServer і AsyncTCP (LGPL-3.0) скомпоновані статично. У кожному релізі є `flatjack-vX.Y.Z-relink.zip`: скомпільовані об'єктні файли FlatJack і проєкт PlatformIO, який збирає ту саму прошивку, тож її можна зібрати з власною зміненою версією цих бібліотек. Їхній вихідний код: версії, вказані в тому проєкті, за посиланнями вище. Тексти ліцензій: [licenses/](licenses/).
