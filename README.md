# Automated Cocoa Mucilage Processor (Rev. 2)
**Operating Instructions & User Manual**

## 1. System Overview
This system is designed to process cocoa beans for a specific duration while monitoring weight in real-time. It features a precise Load Cell for mass monitoring, a Timer-Based Control System for the wash cycle, and a Servo-Controlled Valve for manual discharge.

### Control Interface Map
| Key | Function | Description |
| :--- | :--- | :--- |
| **0-9** | Numeric Input | Used to enter Time (Hours, Minutes, Seconds) and Calibration weights. |
| **A** | ENTER / CONFIRM | Confirms inputs, starts processes, tares the scale, or toggles the Valve. |
| **B** | VALVE CONTROL | Opens the Servo Valve Menu to toggle Open/Close. |
| **D** | CANCEL/STOP | Returns to the previous menu or triggers Emergency Stop. |
| **1** | Option Select | Selects the top option in a menu. |
| **2** | Option Select | Selects the bottom option in a menu. |

### Status Indicators
* **Green LED (Pin A1):** STANDBY - System is idle and ready for input.
* **Red LED (Pin A0):** ACTIVE - Process is running; Relay is ON (Motor Active).
* **Buzzer:** Provides audio feedback on key presses and alarms.

---

## 2. Start-Up Procedure
1.  **Preparation:** Ensure the scale platform/bucket is empty before powering on.
2.  **Power On:** Connect the system to the power source.
3.  **Initialization:**
    * The LCD will display `System starting!`.
    * The Green LED will light up.
    * **Auto-Tare:** The system automatically sets the current weight to 0.0g.
    * **Servo Reset:** The valve automatically moves to the CLOSED (0°) position.
4.  **Ready:** After approx. 3 seconds, the Main Menu will appear.

---

## 3. Operation Modes

### Mode A: Timer Operation (Set Time)
Use this mode to run the motor/pump for a specific duration.

1.  **Select Mode:** From the Main Menu, press **1** (`[1]Set Time`).
2.  **Set Hours:** Screen shows `Set Hours:` — Type the hours (e.g., 1) and press **A**.
3.  **Set Minutes:** Screen shows `Set Mins:` — Type the minutes (e.g., 30) and press **A**.
4.  **Set Seconds:** Screen shows `Set Secs:` — Type the seconds (e.g., 0) and press **A**.
5.  **Confirm Start:**
    * The screen shows a preview: `Begin process? / 01h 30m 00s`.
    * Press **A** to START (or press **D** to cancel).
6.  **Running Process:**
    * **Countdown:** System counts 3... 2... 1....
    * **Action:** Relay turns ON (Motor Starts), Red LED turns ON.
    * **Display:** Line 1 shows Time (counting down); Line 2 shows Mass (live weight monitoring).
7.  **Completion:**
    * When the timer hits `00:00:00`, the Relay and Motor cut off instantly.
    * Screen displays `Time Reached! / Done..`.
    * After 2 seconds, the system returns to the Main Menu.

### Mode B: Manual Valve Control (Servo)
Use this feature to manually open or close the discharge valve.

1.  **Access:** From the Main Menu, press **B**.
2.  **Prompt:** Screen displays `Toggle Valve? / A:Yes D:Back`.
3.  **Action:** Press **A** to toggle the valve position.
    * If Closed (0°) -> It moves to OPEN (180°).
    * If Open (180°) -> It moves to CLOSED (0°).
4.  **Feedback:** Screen confirms `Valve OPENED!` or `Valve CLOSED!`.

### Mode C: Scale Maintenance (Check Scale)
Use this mode to calibrate or zero the scale.

1.  **Select Mode:** From the Main Menu, press **2** (`[2] Check scale`).
2.  **Select Option:**
    * Press **1** for `[Calibrate]`: Recalibrate the sensor using a known weight.
    * Press **2** for `[Set zero]`: Quickly reset the scale to 0.0g (Tare).

---

## 4. Safety & Troubleshooting

### Emergency Stop
If you need to stop the motor/pump immediately while a process is running:
* **Action:** Press the **D** key.
* **Result:** The Relay cuts power immediately, Red LED turns off, and the LCD displays `Process Canceled!`.

### Common Error Messages
| Message | Meaning | Action |
| :--- | :--- | :--- |
| **HX711 Error!** | Load cell not detected. | Check wiring on Pins D4 and D5. Restart system. |
| **Timeout** | Sensor not responding. | Ensure the HX711 module is powered correctly. |

---

## Technical Specifications
*(For Engineering Reference)*

* **Processor:** Arduino Uno / ATmega328P
* **Motor Control:** Relay on Pin D2 (Active HIGH)
* **Valve Control:** Servo Motor on Pin A3 (PWM Signal)
* **Load Cell:** HX711 Interface on Pins D4 (DT) & D5 (SCK)
* **Calibration Memory:** EEPROM Address 0
* **Safety Feature:** Hard-coded "Instant Cutoff" logic ensures the motor stops exactly at T=0
