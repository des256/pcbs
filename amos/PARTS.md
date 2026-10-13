# Parts

## 2. Main Power

- U201 C2653623 LM74700QDBVTQ1: low Iq reverse battery protection ideal diode controller
- CN201..CN202: 2x C431092 XT30PW-M30.G.Y: power connector
- Q201: C882766 CSD18532Q5B: MOSFET
- D201: C908801 SMBJ24A: transient voltage suppressor
- 15A T 2410 (fuse?)
- 4A T 1206 (fuse?)

## 3. 12V Servo Buck

- U301: C485912 LM5145RGYR: 75V synchronous buck DC/DC controller with wide duty cycle range
- Q301..Q302: 2x C882766 CSD18532Q5B: MOSFET
- L301: C2880057 TMPA1265SP-4R7MN-D: 4.7uH 25A inductor

## 4. 5V Servo Buck

- U401: C485912 LM5145RGYR: 75V synchronous buck DC/DC controller with wide duty cycle range
- Q401..Q402: 2x C882766 CSD18532Q5B: MOSFET
- L401: C845075 IHLP4040DZER3R3M01: 3.3uH 18.6A inductor

## 5. 5V USB Buck

- U501: C31966 TPS54560DDAR: 4.5V to 60V input, 5A, step down DC-DC converter with Eco-mode(tm)
- D501: C85100 B560C: Schottky barrier rectifier
- L501: C105681 7447798720: 7.2uH 6A inductor

## 6. 1V1 and 3V3 Buck

- U601..U602: 2x C141836 TLV62569DBVR: 2A high efficiency synchronous buck converter
- L601..L611: 2x C135262 SMNR4020-2.2UH: 2.2uH 3.4A inductor
- FB701: C80165 BLM18PG221SN1D: ferrite bead

## 7. USB Hub

- U701: C544686 TUSB8041IRGCR: 4-port USB 3.0 hub
- U702: C165155 HD3SS3220RNHR: USB-C DRP port controller with SS 2:1 mux
- U703: C138714 TPD4E05U06: 1, 4, 6 channel ESD protection device for SS interface
- USB-C 24P receptacle
- 3x USB-A 3.0 receptacle

## 8. Servo Bus Controller

- U801: C2988084 CH344Q: 4-port USB to UART controller
- U802: C7519 USBLC6-2SC6: protection diodes?

## 9.-12. Servo Bus A, B, C, D

- C10430 SN74LVC2G241DCU: dual buffer and driver with 3-state outputs
- C8963 SP3485EN-L/TR: 3v3 low-power half-duplex RS-485 transceiver 10Mbps
- C2155674 TPS259531DSGR: 2v7-18V 4A 34mOhm eFuse with adjustable current limit, 5v7 output clamp, auto-retry (R_ILM 1.02k = 2A)
- C1849461 TPS16630PWPR: 60V 6A eFuse with adjustable output power limiting
- C32677 PSM712-LF-T7 (diodes?)
- C2857263 SMF5.0A (diode?)
- TTL JST EH 3p
- RS-485 JST EH 4p
- C492401 PZ254V-11-02P: 1x2 2.54mm header (RETRY jumper)
- C2937625 PZ254V-11-03P: 1x3 2.54mm header (RS-485/TTL select jumper)

## 13.-15. USB Port A, B, C

- C138714 TPD4E05U06: 1, 4, 6 channel ESD protection device for SS interface
- C7519 USBLC6-2SC6: protection diodes?
- C55266 TPS2553DBVR: precision adjustable current-limited power distribution switches
- C85840 BLM21PG221SN1D (ferrite?)
