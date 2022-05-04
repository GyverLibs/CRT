This is an automatic translation, may be incorrect in some places. See sources and examples!

# CRT
Library with a set of functions for CRT correction of LEDs
- Table CRT 8 bit (heavy, fast and beautiful)
- Quadratic CRT 8 and 10 bits (easier but slower)
- Cubic CRT 8 and 10 bits (better than square, but even slower)

### Compatibility
Compatible with all Arduino platforms (using Arduino functions)

## Content
- [Install](#install)
- [Initialization](#init)
- [Usage](#usage)
- [Example](#example)
- [Versions](#versions)
- [Bugs and feedback](#feedback)

<a id="install"></a>
## Installation
- The library can be found by the name **CRT** and installed through the library manager in:
    - Arduino IDE
    - Arduino IDE v2
    - PlatformIO
- [Download library](https://github.com/GyverLibs/CRT/archive/refs/heads/main.zip) .zip archive for manual installation:
    - Unzip and put in *C:\Program Files (x86)\Arduino\libraries* (Windows x64)
    - Unzip and put in *C:\Program Files\Arduino\libraries* (Windows x32)
    - Unpack and put in *Documents/Arduino/libraries/*
    - (Arduino IDE) automatic installation from .zip: *Sketch/Include library/Add .ZIP library…* and specify the downloaded archive
- Read more detailed instructions for installing libraries [here] (https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE% D0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA)

<a id="init"></a>
## Initialization
Not

<a id="usage"></a>
## Usage
```cpp
uint8_t CRT8_table(uint8_t val); // 8 bit CRT from table
uint8_t CRT8_square(uint8_t val); // 8 bit CRT quadratic
int CRT10_square(int val); // 10 bit CRT quadratic
uint8_t CRT8_cubic(uint8_t val); // 8 bit CRT cubic
int CRT10_cubic(int val); // 10 bit CRT cubic
```

<a id="example"></a>
## Example
```cpp
// example with a smooth blinking LED

#include <CRT.h>

void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  static int val = 0;
  // PWM on pin 13 for testing
  //softPWM(13, val); // bare value
  softPWM(13, CRT8_table(val)); // via CRT

  // smooth blinking algorithm
  static uint32_t tmr;
  if (millis() - tmr >= 5) {
    tmr = millis();
    static int8_t dir = 1;
    val += dir;
    if (val == 255 || val == 0) dir = -dir; // expand
  }
}

// soft shim
void softPWM(byte pin, byte val) {
  static byte count;
  count++;
  if (count == 0) digitalWrite(pin, 1);
  if (count == val) digitalWrite(pin, 0);
}

```

<a id="versions"></a>
## Versions
- v1.0

<a id="feedback"></a>
## Bugs and feedback
When you find bugs, create an **Issue**, or better, immediately write to the mail [alex@alexgyver.ru](mailto:alex@alexgyver.ru)
The library is open for revision and your **Pull Request**'s!