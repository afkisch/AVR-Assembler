# AVR-Assembler
## Why would you need it?
Of course, the built-in functions of the Arduino IDE are ok for hobby applications. However, even the most basic funcitons such as `digitalWrite()` or `delay()` have some **known issues**. This can be a problem when designing (time-)critical embedded systems. In order to evade these issues we can directly manipulate the registers of the Arduino.

With the following 5 small projects I´d like to give you a small introduction into the AVR Assembly programming.

## 1. Turning on the built-in LED of an Arduino Uno / Nano

### Choose the corresponding port number

According to the datasheet of the Atmega 328P the pin numbers and the corresponding port numbers are the following:

| D0 | D1 | D2 | D3 | D4 | D5 | D6 | D7 | D8 | D9 | D10 | D11 | D12 | D13 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PD0 | PD1 | PD2 | PD3 | PD4 | PD5 | PD6 | PD7 | PB0 | PB1 | PB2 | PB3 | PB4 | **PB5** |

The bulit-in LED of an Uno is connected to **D13** --> **PB5**

### Set data direction
In order to set a pin as output, we have to set the corresponding bit of the **D**ata **D**irection **R**egister to 1.

| Bit || 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DDRB `0x04` || DDB7 | DDB6 | **DDB5** | DDB4 | DDB3 | DDB2 | DDB1 | DDB0 |

Setting the 5th bit of **DDRB** (address `0x04`) using the `sbi` command:

```asm
sbi 0x04, 5
```

| Bit || 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PORTB `0x05` || PORTB7 | PORTB6 | PORTB5 | PORTB4 | PORTB3 | PORTB2 | PORTB1 | PORTB0 |


```asm
.org  0x0000 ; When being reset
rjmp  init ; Jump to label 'init'

init:
  sbi 0x04, 5 ; pinMode(13, OUTPUT)
  sbi 0x05, 5 ; digitalWrite(13, HIGH)

loop:
  rjmp loop ; Jump to label 'loop' - infinite cycle
```
