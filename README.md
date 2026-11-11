# SonghubRemoteESP32C3
ESP32-C3 Firmware for Songhub Remote.

---

## 🔑 License & Activation
This firmware requires an activation key to unlock its full functionality.

**How Activation Works:**
1. Upon first boot, the ESP32-C3 will create a Wi-Fi hotspot.
2. Open the web interface by typing the IP address into your browser: `192.168.4.1`
3. The screen will display a **Hardware ID (HWID)** or a specific code. (Or click the "Activate" button).
4. You must provide this HWID to the developer to generate a unique activation key.
5. Enter the activation key into the web interface. Once verified, the device will unlock, and the Bluetooth keypad functions will become active.

**Getting an Activation Key:**
To purchase or request an activation key, please contact me directly on Facebook:
*   **Developer:** AldenM
*   **Facebook Page:** [Click here to message me on Facebook](https://www.facebook.com/profile.php?id=61596062224543)

---

## 🔌 Hardware Wiring Guide (ESP32-C3 to 4x4 Keypad)
To use this firmware, connect your standard 4x4 Matrix Keypad to the **ESP32-C3** as shown below. 

> ⚠️ **Important:** The ESP32-C3 has fewer pins than the standard ESP32. **Do not use the old 38-pin wiring!** Use the mapping below to avoid crashing the board. Do not use GPIO 8 or 9 (Boot pins).

| Keypad Pin | ESP32-C3 Pin | Keypad Row/Column |
| :--- | :--- | :--- |
| **R1** (Row 1) | **GPIO 2** | 1, 2, 3, A |
| **R2** (Row 2) | **GPIO 3** | 4, 5, 6, B |
| **R3** (Row 3) | **GPIO 4** | 7, 8, 9, C |
| **R4** (Row 4) | **GPIO 5** | *, 0, #, D |
| **C1** (Col 1) | **GPIO 6** | 1, 4, 7, * |
| **C2** (Col 2) | **GPIO 7** | 2, 5, 8, 0 |
| **C3** (Col 3) | **GPIO 10** | 3, 6, 9, # |
| **C4** (Col 4) | **GPIO 1** | A, B, C, D |

**💡 Important Wiring Tips:**
*   **Do Not Connect Power:** The keypad has 8 pins (R1-R4, C1-C4). **Do not** connect any of these wires to `3.3V` or `GND`.
*   **Pin Orientation:** Looking at the front of the keypad, the leftmost pin on the header is usually `R1`, and the rightmost is `C4`.
*   **Testing:** Once flashed, connect to the Wi-Fi and open the web interface. Press a physical button on the keypad. If the web interface displays the wrong number (e.g., pressing '5' shows '8'), it means your Row or Column wires are swapped. Simply swap the wires to fix it.

---

## 🚀 How to Flash the Firmware (Installation)

The ESP32-C3 uses **native USB**, which means you usually **do not need to install a CP2102 driver**. It also requires flashing **three separate files** to specific memory addresses.

### Requirements:
*   **Espressif Flash Download Tool** (Download from the official Espressif website).
*   A USB-C cable (Make sure it is a **data cable**, not just a charging cable).

### Step-by-Step Flashing:
1. Open the Flash Download Tool.
2. Select **ESP32-C3** for ChipType, **Develop** for WorkMode, and **UART** for LoadMode. Click OK.
3. Load the three `.bin` files provided in the **Releases** tab and fill in the exact addresses below:

| File Name | Flash Address |
| :--- | :--- |
| `SonghubRemoteEsp32C3.ino.bootloader.bin` | **`0x0`** |
| `SonghubRemoteEsp32C3.ino.partitions.bin` | **`0x8000`** |
| `SonghubRemoteEsp32C3.ino.bin` | **`0x10000`** |

4. Select the correct **COM Port**.
5. Set the **BAUD** rate to `921600` (or `115200` if it fails).
6. Click **START**.
7. **If it gets stuck on "Waiting for download":** Press and hold the **BOOT** button on your ESP32-C3, plug in the USB cable, and then release the BOOT button. Click START again.

---

## 📖 How to Use the Songhub Remote
This remote acts as a Bluetooth keyboard for your TV, PC, or Smartphone, and is controlled via the built-in Wi-Fi Web Interface.

### 1. How to Connect (TV, PC, or Mobile)
1. **Power the ESP32:** Plug the ESP32-C3 into a power source (like a phone charger or TV USB port).
2. **Connect to Wi-Fi:** On your phone or PC, go to Wi-Fi settings and connect to the network named **"Videoke Remote"** (or "Videoke Remote (Unactivated)").
3. **Open the Remote:** Open a web browser (Chrome, Safari, etc.) and type `192.168.4.1` in the address bar. You will see the Remote UI.
4. **Pair via Bluetooth:**
   * Turn on Bluetooth on your Smart TV, PC, or Phone.
   * Search for new devices and pair with **"Videoke Remote"**.
   * Once connected, the status dot on the web interface will turn **Green** (Bluetooth Connected).

### 2. Button Functions (Web UI & Physical Keypad)
Here is what each button does when connected to your device:

*   **🔢 Number Keys (0 - 9):** Types the numbers directly into your TV/PC. Use this to input the Song Code on your Videoke system. The web screen will display the 6-digit code you are typing.
*   **🅰️ 'A' Button (Melody):** Used to toggle the Melody/Vocal Guide on/off in most Videoke software.
*   **🅱️ 'B' Button (Reserve/Enter):** Used to Reserve a song after typing the code, or to confirm a selection.
*   **©️ 'C' Button (Clear All):** Use this if you typed the wrong song code and want to start over.
*   **🇩 'D' Button (Background):** Used to toggle the Background Video (BGV) on or off.
*   **⭐ '*' Button (Stop):** Stops the current song playing.
*   **#️⃣ '#' Button (Play/Pause):** Pauses or plays the current song.

---

## ⚠️ Disclaimer
*   **No Unauthorized Distribution:** The compiled `.bin` files provided in this repository are for personal use only. Do not sell, redistribute, or claim this firmware as your own.
*   **Hardware Risk:** Flash this firmware at your own risk. Ensure you are using an **ESP32-C3** board and wiring the keypad correctly. The developer is not responsible for bricked devices or damaged hardware.
*   **Reverse Engineering:** Attempting to bypass the activation system, extract the source code, or modify the compiled binary is strictly prohibited.
