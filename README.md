# AVR-Assembler
## Turning on the built-in LED of an Arduino Uno / Nano
### Set data direction
In order to set a pin as output, you have to set the corresponding **D**ata **D**irection **R**egister to 1.


| D0 | D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | D9 | D10 | D11 | D12 | D13 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PD0 | PD1 | PD2 | PD3 | PD4 | PD5 | PD6 | PD7 | PB0 | PB1 | PB2 | PB3 | PB4 | PB5 |

| DDRB 0x04 || DDB7 | DDB6 | DDB5 | DDB4 | DDB3 | DDB2 | DDB1 | DDB0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

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
