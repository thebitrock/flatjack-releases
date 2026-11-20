# FlatJack relinking kit · Набір для перезбирання

## English

FlatJack's firmware uses three libraries under the GNU LGPL: Arduino-ESP32 (LGPL-2.1),
ESPAsyncWebServer and AsyncTCP (LGPL-3.0). They are linked statically, so this kit lets you
build the firmware with your own modified version of them. FlatJack's own code comes as
compiled object files (`objects/`); its source is not published.

1. Download `flatjack-vX.Y.Z-relink.zip` of your version from the [version list](README.md#versions--версії) and unzip it.
2. Install PlatformIO (`pip install platformio`).
3. In the unzipped `flatjack-relink` folder: `pio run -e waveshare-s3` (or `-e esp32dev`). Unmodified, it builds the
   same firmware as the release of that version (the same code; a few bytes of layout may differ).
4. To use a modified library, point its line in `platformio.ini` at your copy, e.g.
   `ESP32Async/AsyncTCP@3.6.1` → `symlink:///path/to/your/AsyncTCP`. To change the Arduino core,
   add `platform_packages = framework-arduinoespressif32 @ symlink:///path/to/your/arduino-esp32`
   to the env.
5. Flash `.pio/build/<env>/firmware.bin` from the web page (System → Firmware update), or
   `firmware.factory.bin` at 0x0 over USB.

A modified library must stay compatible with the interface FlatJack was compiled against.
Library sources: the exact versions in `platformio.ini`, from the PlatformIO registry, and
https://github.com/espressif/arduino-esp32. Licence texts: `LICENSES/`.

## Українська

Прошивка FlatJack використовує три бібліотеки під GNU LGPL: Arduino-ESP32 (LGPL-2.1),
ESPAsyncWebServer і AsyncTCP (LGPL-3.0). Вони скомпоновані статично, тож цей набір дає змогу
зібрати прошивку з вашою зміненою версією цих бібліотек. Власний код FlatJack тут у вигляді
скомпільованих об'єктних файлів (`objects/`); його вихідний код не публікується.

1. Завантажте `flatjack-vX.Y.Z-relink.zip` своєї версії зі [списку версій](README.md#versions--версії) і розпакуйте.
2. Встановіть PlatformIO (`pip install platformio`).
3. У розпакованій теці `flatjack-relink`: `pio run -e waveshare-s3` (або `-e esp32dev`). Без змін збирається та сама
   прошивка, що в релізі цієї версії (той самий код; кілька байтів розміщення можуть відрізнятися).
4. Щоб узяти змінену бібліотеку, вкажіть у її рядку в `platformio.ini` свою копію, наприклад
   `ESP32Async/AsyncTCP@3.6.1` → `symlink:///шлях/до/вашого/AsyncTCP`. Щоб змінити ядро Arduino,
   додайте до env рядок `platform_packages = framework-arduinoespressif32 @ symlink:///шлях/до/вашого/arduino-esp32`.
5. Прошийте `.pio/build/<env>/firmware.bin` з вебсторінки (Система → Оновлення прошивки) або
   `firmware.factory.bin` за адресою 0x0 через USB.

Змінена бібліотека має лишатися сумісною з інтерфейсом, з яким скомпільовано FlatJack.
Вихідний код бібліотек: точні версії з `platformio.ini` з реєстру PlatformIO і
https://github.com/espressif/arduino-esp32. Тексти ліцензій: `LICENSES/`.
