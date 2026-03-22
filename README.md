# 🐕 Meshtastic Dog Tracker

A GPS tracker for your dog based on **Heltec T114 V2** and **Meshtastic**.  
Communicates via LoRa radio — no cellular network or internet required.

---

## 📦 What You Need

| Component | Purpose |
|-----------|---------|
| **Heltec T114 V2** (with 1.14" display) | Tracker worn by the dog |
| **Heltec V3** | Base station at home |
| GPS module (L76K, included with T114) | Provides accurate location |
| LiPo battery (2000mAh recommended) | Power for the tracker |
| 3D printed case | Enclosure for electronics |
| Meshtastic app | For monitoring on your phone |

---

## 🖨️ 3D Printed Case

STL files are available in the `/stl` folder.

**Printing recommendations:**
- Material: **PETG** or **ASA** (weather resistant, UV resistant)
- Layer height: 0.2 mm
- Infill: 30%

The case is designed with integrated slots for zip ties to securely attach the tracker to your dog's harness.

---

## ⚙️ Setup Instructions

### 1. Flash the Firmware

Use the official [Meshtastic Web Flasher](https://flasher.meshtastic.org) with **Chrome or Edge**:

| Device | Model to Select |
|--------|-----------------|
| Tracker (Heltec T114 V2) | `Heltec T114` |
| Base (Heltec V3) | `Heltec V3` |

- Choose the latest stable firmware
- Select **"Full Erase and Install"**
- After flashing, set **Region → EU_868** (mandatory for Italy and Europe)

---

### 2. Configure the Tracker (Dog Unit)

Connect to the T114 via Bluetooth in the Meshtastic app.

| Setting | Value |
|---------|-------|
| **Role** | `TRACKER` |
| **Position update interval** | `60 seconds` (adjust as needed) |
| **GPS** | `ENABLED` |
| **Region** | `EU_868` |

---

### 3. Configure the Base Station (Home Unit)

Connect to the V3 via Bluetooth.

| Setting | Value |
|---------|-------|
| **Role** | `CLIENT` |
| **Region** | `EU_868` |

---

### 4. Create a Private Channel

This ensures that only your devices can see each other.

**On the tracker (T114):**
1. Go to **Settings → Channels**
2. Click **+** to create a new channel
3. Set:
   - **Name**: `DogTracker` (or any name you prefer)
   - **PSK**: generate a random key
   - **Precise Location**: `ON` (this is critical for accurate tracking)
4. Save and set it as **Primary**

**On the base (V3):**
1. Go to **Settings → Channels**
2. Click **+** to add a new channel
3. Enter the **exact same name and PSK** as on the tracker
4. Save and set it as **Primary**

> 💡 **Why a private channel?**  
> The default public channel (`LongFast`) enables "Approximate Location" by default, which rounds positions to ~2.9 km for privacy. A private channel allows you to disable this and get precise GPS coordinates.

---

### 5. Test the Connection

Place both devices close to each other and send a test message from the base:

- If you see a **checkmark ✅**, the devices are communicating.
- If you see a **cloud ☁️**, the message was sent but not received by another node.

You can also enable **Range Test Module** to monitor signal strength and packet success rate.

---

## 📱 Daily Usage

1. **Turn on both devices** (tracker on the dog, base station at home)
2. **Open the Meshtastic app** on your phone and connect to the **base station**
3. **Go to the Map tab** — you'll see your dog's location in real time
4. The tracker sends position updates every 60 seconds (or as configured)

No internet, no cellular coverage needed. The devices communicate directly via LoRa radio.

---

## ⚠️ Important Notes

| Note | Details |
|------|---------|
| **Antenna first!** | Always attach the antenna **before** powering on the device. Running without an antenna can permanently damage the LoRa chip. |
| **Region setting** | Must be `EU_868` for Italy and most of Europe. Using the wrong frequency may violate local regulations. |
| **Battery life** | With a 2000mAh battery and updates every 60 seconds, expect 2–4 days of operation. Reduce update frequency for longer runtime. |
| **Range** | Depends on terrain: 2–5 km in open areas, less in dense urban environments or forests. |

---

## 🛠️ Troubleshooting

| Issue | Solution |
|-------|----------|
| Devices not communicating | Check that both have the **same channel name and PSK**, and **same region (EU_868)**. |
| Position is inaccurate or shows a large circle | You're likely using the public channel. Switch to a **private channel** with **Precise Location enabled**. |
| GPS not fixing | Place the tracker near a window or outdoors. First fix may take a few minutes. |
| Flashing fails | Make sure you're using Chrome/Edge, a data-capable USB cable, and that the device is in bootloader mode (hold BOOT while plugging in). |

---

## 🙏 Credits & License

### 3D Case Design
The 3D printable case for the Heltec T114 is based on the **H2T Case** by [muzi.works](https://www.printables.com/@muziworks).

- Original model: [H2T - Case for Heltec T114 with GPS running Meshtastic](https://www.printables.com/model/982046-h2t-case-for-heltec-t114-with-gps-running-meshtast)
- Original license: [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

### This Repository
All content in this repository — including documentation, configuration examples, and modified STL files — is shared under the same license:  
**Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)**.

This means:
- ✅ You may share and adapt this work
- ✅ You must give appropriate credit (to muzi.works for the original case, and to this repository for modifications and documentation)
- ❌ Commercial use is **not permitted**
- ✅ Derivative works must use the same license

For the full license text, see the [LICENSE](LICENSE) file.

### Meshtastic
[Meshtastic](https://meshtastic.org) is an open-source project. Meshtastic® is a registered trademark of Meshtastic LLC.

