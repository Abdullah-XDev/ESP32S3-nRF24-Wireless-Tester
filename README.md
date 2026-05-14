# ESP32-S3 & nRF24L01 Multi-Functional Wireless Penetration & Testing Tool

A comprehensive, hardware-based wireless security auditing and penetration testing tool built for the **ESP32-S3** microcontroller and the **nRF24L01+** transceiver module. This project combines localized RF signal analysis, 2.4GHz spectrum sniffing, hardware-based HID injection, and advanced Wi-Fi security auditing mechanisms (including a physical-hardware backed Evil Twin attack) into a single standalone device operated via a physical BOOT button and an OLED screen.

## 👤 Author
* **Developer:** Abdullah Eshtayeh
* **GitHub Profile:** [Abdullah-XDev](https://github.com/Abdullah-XDev)

---

## 🛠️ Hardware Requirements
* **Microcontroller:** ESP32-S3 (e.g., ESP32-S3-WROOM-1)
* **Display:** 128x64 OLED Display (SH1106 Driver via I2C)
  * `SDA Pin:` GPIO 8
  * `SCL Pin:` GPIO 9
* **RF Module:** nRF24L01+ (SPI Connection)
  * `CE Pin:` GPIO 4
  * `CSN Pin:` GPIO 5
* **Control Input:** Standard Boot Button (`GPIO 0`)

---

## 🚀 Features & Operational Modes

The device features an adaptive scrolling menu UI supporting **10 distinct operation suites**:

1. **Carrier Scanner:** Sequential evaluation of all 125 raw channels on the nRF24 transceiver to verify carrier wave activity.
2. **Spectrum Analyzer:** Real-time visual waterfall graph drawing signal amplitude against 2.4GHz channels natively on the OLED screen.
3. **nRF Packet Sniffer:** Scans localized channels dynamically to intercept, capture, and count raw over-the-air nRF24 data frames.
4. **MouseJack HID Injector:** Wireless keyboard keystroke injection attack utilizing the `0xA6` unencrypted protocol layout. Injects payload sequences (`GUI + R` -> `CMD`) directly into vulnerable 2.4GHz targets.
5. **WLAN Jammer (1-11):** Generates high-velocity noise arrays sweeping across channels 12 to 65 to effectively flood and saturate standard 2.4GHz Wi-Fi bands (Channels 1-11).
6. **Proto Kill (CC):** Forces the nRF24L01 module into a maximum-power Continuous Carrier Wave Output (`startConstCarrier`) sweeping across all frequencies to jam unhardened industrial wireless protocols.
7. **EvilTwin Matrix:** A full-stack captive portal web ecosystem. It launches a fake access point clone of a target network, hosts a localized Arabic/English phishing administrative portal, forces the target's physical disconnect via synchronized RF jamming, and validates user-submitted passwords directly against the genuine uplink.
8. **Beacon Spammer:** Simulates a localized wireless flood by continuously broadcasting over 25 unique, distinct fake network SSIDs concurrently through rapid background softAP swapping.
9. **WiFi Deauther:** Integrates a localized physical OLED network radar. Allows the operator to scan, scroll through discovered access points, lock onto a target, and launch a surgical nRF24 channel-pulse disconnect attack straight from the screen.
10. **Auth Flood (AP):** Identifies a specific target network via the OLED display interface and bombards its operational channel frequencies with rapid burst frame structures to simulate MAC table authentication exhaustion.

---

## 🕹️ UI Navigation & Button Layout
The standalone firmware uses the **OneButton** library to control the interface using a single input pin (`GPIO 0`):
* **Single Click:** Scroll downwards through menu suites or target access point lists.
* **Long Press (Hold):** 
  * From Main Menu: Confirm and launch the selected application mode.
  * Inside Target Radar: Locks onto the highlighted network.
  * Inside Attacks (Jammer/Deauther/etc.): Toggle the attack state between `ACTIVE` and `READY/IDLE`.
* **Double Click:** Global reset and escape mechanism. Instantly halts all active transmissions, teardowns active captive web/DNS components, restores default standalone `XDev` AP state, and returns to the main menu screen.

---

## ⚙️ Installation & Firmware Deployment

### 1. Library Dependencies
Ensure you have the following libraries installed inside your Arduino IDE or PlatformIO project configuration:
* `U8g2` (by oliver)
* `RF24` (by TMRh20)
* `OneButton` (by Matthias Hertel)

### 2. Compilation Settings
1. Open the source code across its 3 segments inside your environment.
2. Select your board configuration as **ESP32S3 Dev Module**.
3. Verify that your pin mappings align correctly with your specific PCB layout.
4. Flash the compiled binary onto your microcontroller.

---

## 📜 Disclaimer
This software and hardware implementation is designed strictly for **educational purposes, defensive analysis, and authorized security auditing (Penetration Testing)**. Running these scripts against target infrastructures without prior explicit, written authorization is completely illegal and punishable by law. The author assumes no liability or responsibility for any misuse, structural downtime, or legal damages caused by utilizing this framework.
