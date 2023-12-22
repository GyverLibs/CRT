This is an automatic translation, may be incorrect in some places. See sources and examples!

# CRT
Library with a set of functions for CRT Correction of LEDs
- tabular CRT 8 bits (heavy, fast and beautiful)
- square CRT 8 and 10 bits (lighter, but slower)
- cubic CRT 8 and 10 bits (better square, but even slower)

## compatibility
Compatible with all arduino platforms (used arduino functions)

## Content
- [installation] (# Install)
- [initialization] (#init)
- [use] (#usage)
- [Example] (# Example)
- [versions] (#varsions)
- [bugs and feedback] (#fedback)

<a id="install"> </a>
## Installation
- The library can be found by the name ** CRT ** and installed through the library manager in:
    - Arduino ide
    - Arduino ide v2
    - Platformio
- [download library] (https://github.com/gyverlibs/crt/archive/refs/heads/main.zip). Zip archive for manual installation:
    - unpack and put in * C: \ Program Files (X86) \ Arduino \ Libraries * (Windows X64)
    - unpack and put in * C: \ Program Files \ Arduino \ Libraries * (Windows X32)
    - unpack and put in *documents/arduino/libraries/ *
    - (Arduino id) Automatic installation from. Zip: * sketch/connect the library/add .Zip library ... * and specify downloaded archive
- Read more detailed instructions for installing libraries [here] (https://alexgyver.ru/arduino-first/#%D0%A3%D1%81%D1%82%D0%B0%BD%D0%BE%BE%BE%BED0%B2%D0%BA%D0%B0_%D0%B1%D0%B8%D0%B1%D0%BB%D0%B8%D0%BE%D1%82%D0%B5%D0%BA)
### Update
- I recommend always updating the library: errors and bugs are corrected in the new versions, as well as optimization and new features are added
- through the IDE library manager: find the library how to install and click "update"
- Manually: ** remove the folder with the old version **, and then put a new one in its place.“Replacement” cannot be done: sometimes in new versions, files that remain when replacing are deleted and can lead to errors!


<a id="init"> </a>
## initialization
No

<a id="usage"> </a>
## Usage
`` `CPP
Uint8_t CRT8_Table (Uint8_T VAL);// 8 bit CRT from the table
Uint8_t CRT8_SQUARE (UINT8_T VAL);// 8 bit CRT square
Int10_SQUARE (Int Val);// 10 bit CRT square
uint8_t CRT8_cubic (Uint8_t Val);// 8 bit CRT cubic
Int10_cubic (Int Val);// 10 bit CRT cubic
`` `

<a id="EXAMPLE"> </a>
## Example
`` `CPP
// An example with a smooth flashing LED

#incLude <CRT.H>

VOID setup () {
  Pinmode (13, output);
}

VOID loop () {
  static int vel = 0;
  // Shim on 13 pin for dough
  // SoftPWM (13, Val);// naked meaning
  SoftPWM (13, CRT8_Table (VAL));// through CRT

  // algorithm of smooth blinking
  Static uint32_t tmr;
  if (millis () - tmr> = 5) {
    TMR = Millis ();
    static int8_t dir = 1;
    val += dir;
    if (val == 255 || val == 0) die = -Dir;// unfold
  }
}

// Soft Shim
VOID SoftPWM (Byte PIN, Byte Val) {
  Static Byte Count;
  Count ++;
  if (Count == 0) digitalWrite (PIN, 1);
  if (Count == val) digitalWrite (PIN, 0);
}

`` `

<a id="versions"> </a>
## versions
- V1.0

<a id="feedback"> </a>
## bugs and feedback
Create ** Issue ** when you find the bugs, and better immediately write to the mail [alex@alexgyver.ru] (mailto: alex@alexgyver.ru)
The library is open for refinement and your ** pull Request ** 'ow!


When reporting about bugx or incorrect work of the library must be indicated:
- The version of the library
- What is MK used
- SDK version (for ESP)
- version of Arduino ide
- whether the built -in examples work correctly, in which the functions and designs are used, leading to a bug in your code
- what code has been loaded, what work was expected from it and how it works in reality
- Ideally, attach the minimum code in which the bug is observed.Not a canvas of a thousand lines, but a minimum code