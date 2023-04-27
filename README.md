# AVR-Assembler
## Blinking an LED

```assembly
.org  0x0000
rjmp  init

init:
sbi 0x04, 5 ; pinMode(13, OUTPUT)

loop:
ldi  r16, 82
ldi  r17, 43
ldi  r18, 0
sbi 0x05, 5
rcall delay_1000ms
ldi  r16, 82
ldi  r17, 43
ldi  r18, 0
cbi 0x05, 5
rcall delay_1000ms
rjmp loop

delay_1000ms:
dec  r18
brne delay_1000ms
dec  r17
brne delay_1000ms
dec  r16
brne delay_1000ms
ret

```
