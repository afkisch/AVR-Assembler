# AVR-Assembler
## Turning on the built-in LED of an Arduino Uno / Nano
### Set data direction
In order to set a pin as output, you have to set the corresponding **D**ata **D**irection **R**egister to 1.

| Pin | Port |
| --- | ---- |
| D0 | PD0 |
| D1 | PD1 |
| D2 | PD2 |
| D3 | PD3 |
| D4 | PD4 |
| D5 | PD5 |
| D6 | PD6 |
| D7 | PD7 |
| D8 | PB0 |
| D9 | PB1 |
| D10 | PB2 |
| D11 | PB3 |
| D12 | PB4 |
| D13 | PB5 |

<img src="https://user-images.githubusercontent.com/104489999/235291810-aaa8cb3b-6068-4e17-9a9f-f8b78f9b096a.png" width="600">

<img src="https://user-images.githubusercontent.com/104489999/235291737-7467ea2d-c61a-4b67-9c6f-5dc2c35a629e.PNG" width="600">

```asm
.org  0x0000 ; When being reset
rjmp  init ; Jump to label 'init'

init:
  sbi 0x04, 5 ; pinMode(13, OUTPUT)
  sbi 0x05, 5 ; digitalWrite(13, HIGH)

loop:
  rjmp loop ; Jump to label 'loop' - infinite cycle
```
