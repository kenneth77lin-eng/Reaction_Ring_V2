# Reaction_Ring_V2

An Arduino-powered reflex and agility game inspired by the popular arcade/carnival "stick drop" challenge. The system uses electromagnets (controlled via a relay board) to suspend 8 wooden dowels. Once the game starts, the system randomly drops the dowels one by one at unpredictable intervals. Players must use their fast reflexes to catch them before they hit the ground!

---

## 🕹️ How It Works

The codebase is built around a non-blocking **Finite State Machine (FSM)** with four distinct states:
* **STANDBY:** Magnets are powered `ON` by default. Players can easily attach the metal-tipped dowels to the electromagnets.
* **STARTING:** The main switch is flipped ON. The game initializes a true random drop order using the **Fisher-Yates Shuffle Algorithm** and gives players a 3-second warning.
* **PLAYING:** Dowels are dropped one by one based on dynamic time delays.
* **FINISHED:** Once all 8 dowels drop, the magnets instantly re-engage so you can reload the game without turning off the system.

---

## ⚙️ Features

* **True Randomization:** Uses a `Fisher-Yates Shuffle` combined with an uncorrelated floating analog pin reading (`analogRead(A0)`) to guarantee a completely randomized drop sequence every single game.
* **Dynamic Difficulty Scaling:** As the game progresses past the 4th drop, the interval between drops decreases, creating a fast-paced climax.
* **Two Difficulty Modes (Switch selectable):**
  * **Normal Mode:** Faster base intervals (1000ms - 3000ms), aggressive speed scaling, and a special "lightning-fast" final drop (100ms - 500ms).
  * **Easy Mode:** Slower base intervals (2000ms - 4000ms) and more forgiving speed scaling.
* **Fail-Safe Reset:** Flipping the main toggle switch `OFF` at any point instantly interrupts active gameplay, re-engages all magnets, and resets the system to standby safely.

---

## 🛠️ Hardware Connection Reference

* **Microcontroller:** Arduino Uno, Nano, or Mega.
* **Actuators:** 8x Electromagnets controlled via an 8-Channel Relay Module.
* **Inputs:** * 1x Main Toggle Switch (Start/Stop)
  * 1x Easy Mode Toggle Switch

### Pin Mapping

| Component | Arduino Pin | Notes |
| :--- | :---: | :--- |
| **Main Switch** | Pin 10 | Uses internal `INPUT_PULLUP` (Connect to GND when ON) |
| **Easy Mode Switch** | Pin 11 | Uses internal `INPUT_PULLUP` (Connect to GND when ON) |
| **Magnets / Relays 1-8**| Pins 2 to 9 | Digital Outputs (Active `HIGH` for hold, `LOW` for drop) |
| **Floating Pin** | Pin A0 | Kept unconnected to seed the random number generator |

---

## 💾 Installation & Setup

1. Clone or download this repository.
2. Open the file in the **Arduino IDE**.
3. Connect your Arduino board via USB.
4. Select your correct board type and COM port under `Tools`.
5. Click **Upload**.
6. Open the **Serial Monitor** at `9600` baud to see real-time game logs, current drop order sequence, and exact millisecond delay calculations.

---

## 📜 License

This project is open-source and available under the [MIT License].
