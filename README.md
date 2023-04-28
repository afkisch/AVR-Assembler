# AVR-Assembler
## Turning on the built-in LED of an Arduino Uno / Nano

```asm
.org  0x0000 ; When being reset
rjmp  init ; Jump to label 'init'

init:
  sbi 0x04, 5 ; pinMode(13, OUTPUT)
  sbi 0x05, 5 ; digitalWrite(13, HIGH)

loop:
  rjmp loop ; Jump to label 'loop' - infinite cycle
```
