# Amos

Jetson helper board (USB3 + 12V RS-485 Servo + 5V UART Servo)

Input Power: 19V laptop
Output Power: 19V jetson + 12V (10A..20A) servo + 5V (5A..10A) servo + 5V (5A) USB

Upstream USB Hub: USB3-C
Downstream USB Hub: 3x USB3-A + 1x internal to CH344Q

each servo bus either 12V 4-pin RS-485 or 5V 3-pin UART
selectable with DIP

## Schematic Sheets

2: Main Power + Jetson
3: Buck 12V 10A..20A
4: Buck 5V 5A..10A
5: Buck 5V USB
6: Buck 3V3 + 1V1
7: USB HUB
8: CH344Q
9: Servo A
10: Servo B
11: Servo C
12: Servo D
13: USB A
14: USB B
15: USB C
