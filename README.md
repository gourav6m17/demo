# Visual Wiring Diagram - Complete Setup 🎨

## Complete System Layout

```
┌─────────────────────────────────────────────────────────────────┐
│                     ARDUINO UNO (Front View)                    │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                                                         │   │
│  │  [RX] [TX] [RESET] [3.3V] [5V] [GND] [GND] [VIN]       │   │
│  │    0    1                              GND              │   │
│  │                       [AREF]  [A0]  [A1]  [A2]  [A3]    │   │
│  │                                         [A4]  [A5]      │   │
│  │  [13][12][11][10] [9] [8] [7] [6] [5] [4] [3] [2] [1] │   │
│  │  LED          10   9   8   7   6   5   4   3   2   1  │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  I2C Bus (A4, A5):                                             │
│    ┌─────────────────┐          ┌─────────────────┐          │
│    │  0.91" OLED     │          │  MPU6050 Sensor │          │
│    │  Display        │          │                 │          │
│    │  ├─ VCC → 5V    │          │  ├─ VCC → 5V    │          │
│    │  ├─ GND → GND   │          │  ├─ GND → GND   │          │
│    │  ├─ SDA → A4 ───┼──────────┼──┤ SDA ← A4     │          │
│    │  └─ SCK → A5 ───┼──────────┼──┤ SCL ← A5     │          │
│    │     (SCK=SCL) ──┼──────────┼──┤ SAME SIGNAL! │          │
│    └─────────────────┘          └─────────────────┘          │
│                                                                 │
│  NOTE: SCK (OLED) = SCL (MPU6050) = I2C Clock                │
│        They are the SAME signal - both connect to A5!         │
│                                                                 │
│  Serial Ports:                                                  │
│    ┌─────────────────┐          ┌─────────────────┐          │
│    │  GPS Module     │          │  GSM Module     │          │
│    │  NEO-6M         │          │  SIM800L        │          │
│    │  ├─ VCC → 5V    │          │  ├─ VCC → 5V    │          │
│    │  ├─ GND → GND   │          │  ├─ GND → GND   │          │
│    │  ├─ TX → Pin 9 ─┼─────────┐│  ├─ TX → Pin 7 ─┼─────────┐│
│    │  └─ RX → Pin 8 ─┼───┐     ││  └─ RX → Pin 6 ─┼───┐     ││
│    └─────────────────┘   │     ││  └─ SIM Card ─┐│   │     ││
│                           │     ││              ││   │     ││
│  Pin 9: GPS TX ←───────┘  │     ││  Pin 7: GSM TX←──┘     ││
│  Pin 8: GPS RX        │   │     ││  Pin 6: GSM RX         ││
│                      │   │     │└──────────────────────┘│
│                      │   │     │                       │
│  Digital Pins:       │   │     └───────────────────────┘│
│                      │   │                              │
│    ┌─────────────┐  │   │                              │
│    │  ONE BUTTON │  │   │                              │
│    │  (4-leg)   │  │   │                              │
│    │             │  │   │                              │
│    │  Top leg1 ──┼──┼───┼──→ Pin 10                   │
│    │  Top leg2 ──┼──┼───┼──→ 10kΩ → 5V                │
│    │  Bot leg3 ──┼──┼───┼──→ GND                      │
│    │  Bot leg4 ──┼──┼───┼──→ GND                      │
│    └─────────────┘  │   │                              │
│                     │   │                              │
│  Pin 10: Button ←──┘   │                              │
│                     │   │                              │
│    ┌─────────────┐  │   │                              │
│    │  BUZZER     │  │   │                              │
│    │  5V Active  │  │   │                              │
│    │  ├─ (+) ────┼──┼───┼──→ Pin 14 (A0)              │
│    │  └─ (-) ────┼──┼───┼──→ GND                      │
│    └─────────────┘  │   │                              │
│                     │   │                              │
│  Pin 14: Buzzer ←───┘   │                              │
│  Pin 13: LED (built-in) │                              │
│                         │                              │
│  Power Bus:             │                              │
│  ┌─────────────────────┼───────────────────────────────┼─────┐
│  │ 5V ──────────────────┴─────────────┬─────────────────┴───┤
│  │ All VCC pins connect here          │                     │
│  └──────────────────────────────────────────────────────────┘
│  ┌──────────────────────────────────────────────────────────┐
│  │ GND ─────────────────────────────────────────────────────┤
│  │ All GND pins connect here                                 │
│  └──────────────────────────────────────────────────────────┘
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## Side View - Component Layout

```
                    HELMET SHELL
    ╔═══════════════════════════════════════════════════╗
    ║                                                   ║
    ║  ┌────────────────────────────────────────┐      ║
    ║  │        Arduino Uno (Inside)            │      ║
    ║  └────────────────────────────────────────┘      ║
    ║         │                                          ║
    ║         ├── OLED Display (Front)                  ║
    ║         │                                          ║
    ║  ┌──────┼──────────────┐                        ║
    ║  │ MPU6050 (Top)       │ ← Sensor on top         ║
    ║  └──────┼──────────────┘                        ║
    ║         │                                          ║
    ║         ├── GPS (Exterior)                       ║
    ║         │   with antenna                          ║
    ║         │                                          ║
    ║         ├── GSM Module (Inside)                   ║
    ║         │   with SIM card                         ║
    ║         │                                          ║
    ║         ├── Button (Side)                          ║
    ║         │   Easy access                           ║
    ║         │                                          ║
    ║         └── Buzzer (Inside)                        ║
    ║              Audio alarm                           ║
    ║                                                   ║
    ╚═══════════════════════════════════════════════════╝
```

---

## Pin Connection Diagram

```
                    ARDUINO UNO
          
  Pin Layout:                    I2C Bus:
┌────────────────┐             ┌──────────────┐
│                │             │              │
│ 0  : (RX)      │             │  A4 (SDA) ───┤───── OLED SDA
│ 1  : (TX)      │             │              │      MPU6050 SDA
│ 2  :           │             │              │
│ 3  :           │             │  A5 (SCL) ───┤───── OLED SCK (same as SCL!)
│ 4  :           │             │              │      MPU6050 SCL
│ 5  :           │             │              │
│ 6  : GSM RX ←──┼─── GSM      │              │
│ 7  : GSM TX ←──┼─── GSM      │              │
│ 8  : GPS RX ←──┼─── GPS      │              │
│ 9  : GPS TX ←──┼─── GPS      │              │
│ 10 : BUTTON ←──┼─── Button   │              │
│ 11 :           │             │              │
│ 12 :           │             │              │
│ 13 : LED       │             │              │
│                │             │              │
│ A0 : BUZZER ←──┼─── Buzzer   │  Power:      │
│ A1 :           │             │  5V ──────────┘─── All VCC
│ A2 :           │             │  GND ─────────── All GND
│ A3 :           │             │              │
│ A4 : (SDA) ────┘             │              │
│ A5 : (SCL) ────┘             │              │
└────────────────┘             └──────────────┘
```

---

## Power Distribution

```
             9V ADAPTER
                │
                ├── VIN
                │   │
         ┌──────┼───┴──────┐
         │      │          │
      Arduino   5V         GND
       Uno      │           │
                │           │
    ┌───────────┴──────┐    │
    │   5V BUS         │    │
    │                  │    │
    ├─ OLED VCC        │    │
    ├─ MPU6050 VCC     │    │
    ├─ GPS VCC         │    │
    ├─ GSM VCC         │    │
    ├─ Buzzer (+)      │    │
    ├─ Button pull-up  │    │
    └──────────────────┘    │
                             │
                ┌────────────┴──────────┐
                │      GND BUS          │
                │                       │
                ├─ OLED GND             │
                ├─ MPU6050 GND          │
                ├─ GPS GND              │
                ├─ GSM GND              │
                ├─ Buzzer (-)           │
                └─ Button GND           │
```

---

## Button Detail (4-Leg Micro)

```
              BUTTON CONNECTIONS
                  
            ┌─────────────┐
            │             │
         ┌──┤   BUTTON    ├──┐
         │  │    (4-leg)  │  │
         │  │             │  │
    Pin 10│  │             │  │GND
    ────  │  │             │  ───
    │     │  │             │  │
    │     └──┤             ├──┘
    │        │   LEG 1 & 2  │
    │        │   (top)     │
    │        │             │
    10kΩ     │   LEG 3 & 4  │
     │       │   (bottom)  │
     └───────┘             └─── GND
              
           ┌───┐
           │5V │──────────┬── 5V
           └───┘          │
                          │
                    [10kΩ Resistor]
                          │
                  ┌───────┴───────┐
                  │    BUTTON     │
                  │   Pin 10      │
                  └───────────────┘
```

---

## IMPORTANT: SCK and SCL are the SAME!

**Your OLED has:** SCK (some OLEDs label it this way)
**MPU6050 has:** SCL
**They both connect to:** Arduino A5

**Why?** Both are I2C Clock signals:
- SCK = Serial Clock (I2C terminology)
- SCL = Serial Clock Line (I2C terminology)
- **They are THE SAME signal!**

**So your wiring:**
```
OLED SCK → A5 ← MPU6050 SCL
```
**Both connect to the same pin - NO CONFLICT!** ✅

---

## Complete Connection Map

```
Component        Wire Color    Arduino    Function
─────────────────────────────────────────────────────
OLED Display     Red          5V         Power
                 Black        GND        Ground
                 Yellow       A4         SDA (data)
                 Green        A5         SCK (clock, same as SCL!)

MPU6050          Red          5V         Power
                 Black        GND        Ground
                 Yellow       A4         SDA (shared with OLED)
                 Green        A5         SCL (shared with OLED SCK)

GPS Module       Red          5V         Power
                 Black        GND        Ground
                 Blue         Pin 9      TX (sends)
                 Yellow       Pin 8      RX (receives)

GSM Module       Red          5V         Power
                 Black        GND        Ground
                 Green        Pin 7      TX (sends)
                 Orange       Pin 6      RX (receives)

Button           Brown        Pin 10     Signal
                 Brown        10kΩ→5V    Pull-up
                 Black        GND        Ground
                 Black        GND        Ground

Buzzer           Red          Pin 14     Positive
                 Black        GND        Ground
```

---

## 3D Layout Visualization

```
                TOP VIEW
                
    ┌──────────────────────────────────┐
    │        HELMET INSIDE             │
    │                                  │
    │  ┌────────────┐   ┌──────────┐  │
    │  │  Arduino   │   │  MPU6050 │  │
    │  │    Uno     │   │ (on top) │  │
    │  └─────┬──────┘   └──────────┘  │
    │        │                         │
    │        │  ┌──────────────────┐  │
    │        │  │  OLED Display    │  │
    │        │  │  (Front facing) │  │
    │        │  └──────────────────┘  │
    │        │                         │
    │        │  ┌──────────┐          │
    │        │  │   GSM    │          │
    │        │  │  Module  │          │
    │        │  └──────────┘          │
    │        │                         │
    │  ┌─────┴─────┐                 │
    │  │  Buzzer   │                 │
    │  └───────────┘                 │
    │                                │
    │  ┌──────────────────────────┐ │
    │  │  GPS Module              │ │
    │  │  (Exterior with antenna) │ │
    │  └──────────────────────────┘ │
    └────────────────────────────────┘
           │
           │  BUTTON (Side)
           └─────────────────────
```

---

## Wire Routing Inside Helmet

```
INSIDE HELMET:

Power Distribution:
━━━━━━━━━━━━━━━━━━━━━━━━━━
│ 5V ───────────────────────┬── OLED
│                        ├── MPU6050
│                        ├── GPS
│                        └── GSM
│
│ GND ────────────────────┬── OLED
│                       ├── MPU6050
│                       ├── GPS
│                       ├── GSM
│                       ├── Buzzer
│                       └── Button

Data Lines:
━━━━━━━━━━━━━━━━━━━━━━━━━━
│ A4 ────┬── OLED SDA
│        └── MPU6050 SDA
│
│ A5 ────┬── OLED SCL
│        └── MPU6050 SCL
│
│ Pin 9 ─── GPS TX
│ Pin 8 ─── GPS RX
│ Pin 7 ─── GSM TX
│ Pin 6 ─── GSM RX
│ Pin 10 ── Button (with 10kΩ)
│ Pin 14 ── Buzzer
```

---

## Quick Connect Chart

```
ARDUINO PIN    COMPONENT      WIRE COLOR (suggestion)
────────────────────────────────────────────────────
Pin 0          (Not used)
Pin 1          (Not used)
Pin 6          GSM RX         Orange
Pin 7          GSM TX         Green
Pin 8          GPS TX         Blue
Pin 9          GPS RX         Yellow
Pin 10         BUTTON         Brown + 10kΩ to 5V
Pin 13         LED            (automatic)
Pin 14 (A0)    Buzzer         Red (+)

A4 (SDA)       OLED + MPU6050 Yellow
A5 (SCL)       OLED + MPU6050 Green

5V             All VCC        Red
GND            All GND        Black
```

---

## Real-World Placement

```
           HELMET (Side View)
        ╔══════════════════════╗
        ║  GPS (Exterior)     ║ ← Antenna
        ║  ┌──────────┐       ║
        ║  │          │       ║
        ║  └──────────┘       ║
        ║                      ║
        ║  ┌──────────┐       ║
        ║  │ OLED     │       ║ ← Display visible
        ║  │ Display  │       ║
        ║  └──────────┘       ║
        ║      │              ║
        ║  ┌───▼──────────┐  ║
        ║  │  Arduino     │  ║
        ║  │  + MPU6050   │  ║ ← Sensors
        ║  └───┬──────────┘  ║
        ║      │              ║
        ║  ┌───▼──────────┐  ║
        ║  │  GSM Module │  ║
        ║  └───┬──────────┘  ║
        ║      │              ║
        ║  ┌───▼──────┐      ║
        ║  │  Buzzer  │      ║
        ║  └──────────┘      ║
        ║                     ║
        ║  ┌────────┐         ║
        ║  │ BUTTON │ ← Easy access
        ║  └────────┘         ║
        ╚══════════════════════╝
```

---

**This visual guide shows all connections clearly!** 🎨✅

---

## Wire Both Devices to Same Pins - Explanation

```
                    A4 (SDA)
                      │
            ┌─────────┴─────────┐
            │                   │
        OLED SDA          MPU6050 SDA
        (data)                (data)
            │                   │
            └─────────┬─────────┘
                      │
                 Arduino A4
                      │
            Both share same pin!
            (No conflict - I2C multi-device)

                    A5 (SCL)
                      │
            ┌─────────┴─────────┐
            │                   │
        OLED SCK          MPU6050 SCL
        (clock)              (clock)
            │                   │
            └─────────┬─────────┘
                      │
                 Arduino A5
                      │
            Both share same pin!
            SCK = SCL (SAME SIGNAL!)
```

**Why this works:**
- I2C protocol supports multiple devices on same bus
- Each device has unique address
- OLED: 0x3C
- MPU6050: 0x68
- Arduino communicates with each separately
- **SCK and SCL are identical signals**
- **Both can connect to A5 - NO PROBLEM!** ✅

