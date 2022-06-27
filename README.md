[![Foo](https://img.shields.io/badge/Version-1.0-brightgreen.svg?style=flat-square)](#versions)
[![Foo](https://img.shields.io/badge/Website-AlexGyver.ru-blue.svg?style=flat-square)](https://alexgyver.ru/)
[![Foo](https://img.shields.io/badge/%E2%82%BD$%E2%82%AC%20%D0%9D%D0%B0%20%D0%BF%D0%B8%D0%B2%D0%BE-%D1%81%20%D1%80%D1%8B%D0%B1%D0%BA%D0%BE%D0%B9-orange.svg?style=flat-square)](https://alexgyver.ru/support_alex/)
[![Foo](https://img.shields.io/badge/README-ENGLISH-blueviolet.svg?style=flat-square)](https://github-com.translate.goog/GyverLibs/CRT?_x_tr_sl=ru&_x_tr_tl=en) 
[![Foo](https://img.shields.io/badge/ПОДПИСАТЬСЯ-НА%20ОБНОВЛЕНИЯ-brightgreen.svg?style=social&logo=telegram&color=blue)](https://t.me/GyverLibs)


# CRT
Библиотека с набором функций для CRT коррекции светодиодов
- Табличный CRT 8 бит (тяжёлый, быстрый и красивый)
- Квадратичный CRT 8 и 10 бит (легче, но медленнее)
- Кубический CRT 8 и 10 бит (лучше квадратного, но ещё медленнее)

### Совместимость
Совместима со всеми Arduino платформами (используются Arduino-функции)

## Содержание
- [Установка](#install)
- [Инициализация](#init)
- [Использование](#usage)
- [Пример](#example)
- [Версии](#versions)
- [Баги и обратная связь](#feedback)

<a id="install"></a>
## Установка
- Библиотеку можно найти по названию **CRT** и установить через менеджер библиотек в:
    - Arduino IDE
    - Arduino IDE v2
    - PlatformIO
- [Скачать библиотеку](https://github.com/GyverLibs/CRT/archive/refs/heads/main.zip) .zip архивом для ручной установки:
    - Распаковать и положить в *C:\Program Files (x86)\Arduino\libraries* (Windows x64)
    - Распаковать и положить в *C:\Program Files\Arduino\libraries* (Windows x32)
    - Распаковать и положить в *Документы/Arduino/libraries/*
    - (Arduino IDE) автоматическая установка из .zip: *Скетч/Подключить библиотеку/Добавить .ZIP библиотеку…* и указать скачанный архив
- Читай более подробную инструкцию по установке библиотек [здесь](https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA)
### Обновление
- Рекомендую всегда обновлять библиотеку: в новых версиях исправляются ошибки и баги, а также проводится оптимизация и добавляются новые фичи
- Через менеджер библиотек IDE: найти библиотеку как при установке и нажать "Обновить"
- Вручную: **удалить папку со старой версией**, а затем положить на её место новую. "Замену" делать нельзя: иногда в новых версиях удаляются файлы, которые останутся при замене и могут привести к ошибкам!


<a id="init"></a>
## Инициализация
Нет

<a id="usage"></a>
## Использование
```cpp
uint8_t CRT8_table(uint8_t val);    // 8 бит CRT из таблицы
uint8_t CRT8_square(uint8_t val);   // 8 бит CRT квадратичный
int CRT10_square(int val);          // 10 бит CRT квадратичный
uint8_t CRT8_cubic(uint8_t val);    // 8 бит CRT кубический
int CRT10_cubic(int val);           // 10 бит CRT кубический
```

<a id="example"></a>
## Пример
```cpp
// пример с плавным миганием светодиода

#include <CRT.h>

void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  static int val = 0;
  // шим на 13 пине для теста
  //softPWM(13, val);               // голое значение
  softPWM(13, CRT8_table(val));     // через CRT

  // алгоритм плавного мигания
  static uint32_t tmr;
  if (millis() - tmr >= 5) {
    tmr = millis();    
    static int8_t dir = 1;
    val += dir;    
    if (val == 255 || val == 0) dir = -dir;   // разворачиваем
  }  
}

// софт шим
void softPWM(byte pin, byte val) {
  static byte count;
  count++;
  if (count == 0) digitalWrite(pin, 1);
  if (count == val) digitalWrite(pin, 0);
}

```

<a id="versions"></a>
## Версии
- v1.0

<a id="feedback"></a>
## Баги и обратная связь
При нахождении багов создавайте **Issue**, а лучше сразу пишите на почту [alex@alexgyver.ru](mailto:alex@alexgyver.ru)  
Библиотека открыта для доработки и ваших **Pull Request**'ов!


При сообщении о багах или некорректной работе библиотеки нужно обязательно указывать:
- Версия библиотеки
- Какой используется МК
- Версия SDK (для ESP)
- Версия Arduino IDE
- Корректно ли работают ли встроенные примеры, в которых используются функции и конструкции, приводящие к багу в вашем коде
- Какой код загружался, какая работа от него ожидалась и как он работает в реальности
- В идеале приложить минимальный код, в котором наблюдается баг. Не полотно из тысячи строк, а минимальный код
