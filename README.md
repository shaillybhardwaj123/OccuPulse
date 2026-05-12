<div align="center">

<br/>

```
 ██████╗  ██████╗ ██████╗██╗   ██╗██████╗ ██╗   ██╗██╗     ███████╗███████╗
██╔═══██╗██╔════╝██╔════╝██║   ██║██╔══██╗██║   ██║██║     ██╔════╝██╔════╝
██║   ██║██║     ██║     ██║   ██║██████╔╝██║   ██║██║     ███████╗█████╗  
██║   ██║██║     ██║     ██║   ██║██╔═══╝ ██║   ██║██║     ╚════██║██╔══╝  
╚██████╔╝╚██████╗╚██████╗╚██████╔╝██║     ╚██████╔╝███████╗███████║███████╗
 ╚═════╝  ╚═════╝ ╚═════╝ ╚═════╝ ╚═╝      ╚═════╝ ╚══════╝╚══════╝╚══════╝
```

# OccuPulse 🟢
### _Real-Time Exam Hall Occupancy Intelligence_

<br/>

[![Arduino](https://img.shields.io/badge/Arduino-UNO-00979D?style=for-the-badge&logo=arduino&logoColor=white)](https://www.arduino.cc/)
[![Flask](https://img.shields.io/badge/Flask-Backend-000000?style=for-the-badge&logo=flask&logoColor=white)](https://flask.palletsprojects.com/)
[![Firebase](https://img.shields.io/badge/Firebase-Realtime_DB-FFCA28?style=for-the-badge&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org/)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)]()

<br/>

> **One sensor. One hall. Zero guesswork.**
> OccuPulse turns a single HC-SR04 ultrasonic sensor into a full-featured live occupancy monitoring system — complete with a dark-mode dashboard, Firebase cloud sync, and tri-color LED feedback.

<br/>

---

</div>

## 📡 What Is OccuPulse?

OccuPulse is an **IoT-powered exam hall occupancy monitor** that uses a single ultrasonic sensor on an Arduino UNO to intelligently detect entries and exits — no second sensor needed. The live count streams over USB serial to a **Flask web backend**, syncs to **Firebase Realtime Database**, and renders on a stunning **dark-mode web dashboard** with charts, stats, and alerts.

Whether you're managing a 30-seat exam room, a library pod, or a lab — OccuPulse gives you full situational awareness with minimal hardware.

<br/>

---

## ✨ Feature Highlights

| Feature | Description |
|---|---|
| 🔵 **Single-Sensor Entry/Exit Detection** | One HC-SR04 determines direction using a timed two-trigger algorithm |
| 📊 **Live Web Dashboard** | Dark-mode UI with big counter, progress bars, trend chart & event log |
| ☁️ **Firebase Cloud Sync** | Every entry/exit is logged to Realtime Database in real-time |
| 🚦 **Tri-Color LED Feedback** | Green (available) → Yellow (warning at 80%) → Red + Buzzer (full) |
| 📈 **Session Statistics** | Peak count, total entries, total exits, fill rate |
| 💾 **CSV Export** | Download the session log with one click |
| 🔄 **Auto-Refresh** | Dashboard polls every 2 seconds — no page reload needed |
| 🔌 **Arduino Connection Indicator** | Live badge shows if serial link is healthy |
| ♻️ **Reset Button** | Clear the session instantly, both locally and in Firebase |

<br/>

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        OCCUPULSE SYSTEM                             │
│                                                                     │
│  ┌──────────────┐     USB Serial      ┌────────────────────────┐   │
│  │  ARDUINO UNO │ ─────────────────▶  │   Flask Backend        │   │
│  │              │   "EVENT:Entry,     │   (app.py)             │   │
│  │ HC-SR04      │    COUNT:12,        │                        │   │
│  │ ┌──────────┐ │    STATUS:AVAILABLE"│   • Serial reader      │   │
│  │ │ TRIG  3  │ │                     │     (daemon thread)    │   │
│  │ │ ECHO  4  │ │                     │   • State management   │   │
│  │ └──────────┘ │                     │   • REST API /data     │   │
│  │              │                     │         /logs          │   │
│  │ LEDs: 9,10,11│                     │         /reset         │   │
│  │ Buzzer: 8    │                     └──────────┬─────────────┘   │
│  └──────────────┘                               │                   │
│                                      ┌──────────┴────────┐          │
│                                      │                   │          │
│                              ┌───────▼──────┐  ┌─────────▼──────┐  │
│                              │  Firebase    │  │  Dashboard     │  │
│                              │  Realtime DB │  │  (HTML/JS/CSS) │  │
│                              │              │  │                │  │
│                              │  /occupancy  │  │  • Live count  │  │
│                              │  /logs       │  │  • Chart.js    │  │
│                              └──────────────┘  │  • CSV export  │  │
│                                                └────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

<br/>

---

## 🔧 Hardware Required

| Component | Qty | Purpose |
|---|---|---|
| Arduino UNO | 1 | Microcontroller |
| HC-SR04 Ultrasonic Sensor | 1 | Distance / person detection |
| Red LED | 1 | Full alert |
| Yellow LED | 1 | Warning (≥80% capacity) |
| Green LED | 1 | Available status |
| Active Buzzer | 1 | Audible full alert |
| 220Ω Resistors | 3 | LED current limiting |
| Breadboard | 1 | Prototyping |
| Jumper Wires | ~10 | Connections |
| USB-A to USB-B Cable | 1 | Arduino ↔ PC |

<br/>

---

## 🔌 Wiring Diagram

```
Arduino UNO                     Components
──────────────                  ──────────────────────────────
Pin 3  (TRIG) ────────────────▶ HC-SR04 TRIG
Pin 4  (ECHO) ◀──────────────── HC-SR04 ECHO
5V            ────────────────▶ HC-SR04 VCC
GND           ────────────────▶ HC-SR04 GND

Pin 9  (PWM)  ──[220Ω]───────▶ Red LED     (+) → GND
Pin 10 (PWM)  ──[220Ω]───────▶ Yellow LED  (+) → GND
Pin 11 (PWM)  ──[220Ω]───────▶ Green LED   (+) → GND
Pin 8         ────────────────▶ Buzzer (+)  (–) → GND
```

| Arduino Pin | Connected To |
|---|---|
| `3` | HC-SR04 TRIG |
| `4` | HC-SR04 ECHO |
| `8` | Active Buzzer |
| `9` | Red LED |
| `10` | Yellow LED |
| `11` | Green LED |
| `5V` | HC-SR04 VCC |
| `GND` | All GND rails |

<br/>

---

## 🧠 How the Single-Sensor Algorithm Works

> OccuPulse uses a **timed dual-trigger** method to detect both entries AND exits with just one sensor:

```
  Person approaches doorway
           │
           ▼
  Distance < 20 cm?
           │
    ┌──────┴──────┐
   YES            NO
    │              │
    ▼              ▼
First trigger?   Reset state
    │
 ┌──┴──┐
YES    NO (within 3s window)
 │      │
 ▼      ▼
ENTRY  EXIT
count++ count--
```

**In plain English:**

- 🚶 **1st detection** — someone crosses the threshold → **Entry** (count +1)
- 🚶 **2nd detection within 3 seconds** — same person steps back → **Exit** (count −1)
- ⏱️ **After 3 seconds** — state resets; next detection starts fresh

This makes a single sensor surprisingly robust for low-to-medium traffic doorways like exam hall entrances.

<br/>

---

## 🚦 LED & Buzzer Status Codes

| Occupancy Level | Indicator | Meaning |
|---|---|---|
| 0% – 79% | 🟢 Green LED | Hall is **AVAILABLE** |
| 80% – 99% | 🟡 Yellow LED | **WARNING** — nearly full |
| 100% | 🔴 Red LED + 🔔 Buzzer | **FULL** — no entry |

<br/>

---

## 📁 Project Structure

```
occupulse/
│
├── arduino/
│   └── occupancy.ino          ← Flash this to your Arduino UNO
│
├── templates/
│   └── dashboard.html         ← Full-featured web dashboard
│
├── app.py                     ← Flask server + serial reader thread
├── firebase_config.py         ← Firebase Admin SDK integration
├── requirements.txt           ← Python dependencies
├── .gitignore                 ← Keeps secrets out of version control
└── serviceAccountKey.json     ← 🔒 NOT included — you generate this locally (see Setup)
```

<br/>

---

## 🚀 Setup & Installation

### Step 1 — Flash the Arduino

1. Open `arduino/occupancy.ino` in [Arduino IDE](https://www.arduino.cc/en/software)
2. Select **Board:** Arduino UNO
3. Select your port (e.g. `COM3` on Windows, `/dev/ttyUSB0` on Linux)
4. Click **Upload ▶**

---

### Step 2 — Set Up Firebase

1. Go to [Firebase Console](https://console.firebase.google.com)
2. Create a new project
3. Enable **Realtime Database** → Start in **test mode**
4. Go to **Project Settings → Service Accounts → Generate new private key**
5. Save the downloaded file as `serviceAccountKey.json` in the project root

> ⚠️ **Security Warning:** `serviceAccountKey.json` contains your private Firebase credentials.
> **Never commit it to Git.** Add it to `.gitignore` immediately:
> ```
> echo "serviceAccountKey.json" >> .gitignore
> ```

6. Open `firebase_config.py` and update:

```python
'databaseURL': 'https://YOUR-PROJECT-ID.firebaseio.com'
```

---

### Step 3 — Install Python Dependencies

```bash
pip install -r requirements.txt
```

`requirements.txt` includes:
```
flask
flask-cors
pyserial
firebase-admin
```

---

### Step 4 — Configure Serial Port

Open `app.py` and set the correct port for your OS:

```python
# Windows
SERIAL_PORT = 'COM3'

# Linux / Raspberry Pi
SERIAL_PORT = '/dev/ttyUSB0'

# macOS
SERIAL_PORT = '/dev/cu.usbmodem14101'
```

---

### Step 5 — Run OccuPulse

```bash
python app.py
```

---

### Step 6 — Open the Dashboard

```
http://localhost:5000
```

<br/>

---

## 🖥️ Dashboard Preview

The dashboard is built with a dark-mode aesthetic and renders:

```
┌─────────────────────────────────────────────────────┐
│  🟢 OccuPulse  [● LIVE]  [12:34:05]  [● CONNECTED] │
├──────────────┬──────────────┬──────────┬────────────┤
│  OCCUPIED    │  AVAILABLE   │  ENTRIES │  EXITS     │
│    12        │    18        │    15    │    3       │
├──────┬───────┴──────────────┴──────────┴────────────┤
│ BIG  │  ████████████░░░░░░░░  40%       [AVAILABLE] │
│  12  │                                              │
│ /30  │  Hall A ████████░░░  12/30   [AVAILABLE]     │
├──────┴──────────────────────────────────────────────┤
│  TREND (last 10 readings)                           │
│  ▁▂▃▄▅▆▆▇▇█                                       │
├─────────────────────────────────────────────────────┤
│  EVENT LOG                [Export CSV]  [Reset]     │
│  12:34:02  Entry  count=12  AVAILABLE               │
│  12:33:59  Exit   count=11  AVAILABLE               │
└─────────────────────────────────────────────────────┘
```

**Dashboard Widgets:**

- 📦 **4-metric top bar** — Occupied, Available, Total Entries, Total Exits
- 🔢 **Big live counter** — Dominant number display with status badge
- 📊 **Animated progress bar** — Color shifts green → amber → red dynamically
- 📉 **Hall occupancy bars** — Per-hall visual fill indicators
- 📈 **Trend chart** — Last 10 readings, powered by Chart.js
- 🗒️ **Firebase event log** — Real-time entry/exit feed
- 💾 **CSV export** — One-click session data download
- ♻️ **Reset button** — Clears session state + Firebase
- 🔌 **Connection badge** — Arduino serial health indicator

<br/>

---

## 🌐 API Reference

The Flask backend exposes these REST endpoints:

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/` | Serves the dashboard HTML |
| `GET` | `/data` | Returns live occupancy JSON |
| `GET` | `/logs` | Returns last 20 Firebase events |
| `POST` | `/reset` | Resets all counts to zero |
| `GET` | `/health` | Server + serial connection status |

**Sample `/data` response:**

```json
{
  "count": 12,
  "max": 30,
  "status": "AVAILABLE",
  "percentage": 40.0,
  "total_entries": 15,
  "total_exits": 3,
  "available": 18,
  "connected": true,
  "last_event": "Entry"
}
```

<br/>

---

## 📦 Firebase Data Structure

```json
{
  "occupancy": {
    "hall_a": {
      "count": 12,
      "status": "AVAILABLE",
      "last_updated": "2026-05-12T18:49:00.000Z"
    }
  },
  "logs": {
    "-Nxyz123": {
      "timestamp": "2026-05-12T18:49:00.000Z",
      "hall": "Hall A",
      "event": "Entry",
      "count": 12,
      "status": "AVAILABLE"
    }
  }
}
```

<br/>

---

## ⚙️ Configuration Reference

All tunable parameters live at the top of their respective files:

**`app.py`**
```python
MAX_CAPACITY = 30        # Maximum allowed occupants
SERIAL_PORT  = 'COM3'   # Arduino serial port
BAUD_RATE    = 9600      # Must match Arduino sketch
```

**`arduino/occupancy.ino`**
```cpp
int MAX_CAPACITY   = 30;    // Max occupants (mirrored in app.py)
int ENTRY_TIMEOUT  = 3000;  // ms window for exit detection
// Sensor threshold: distance < 20 cm triggers detection
```

<br/>

---

## 🛠️ Troubleshooting

| Problem | Solution |
|---|---|
| `SerialException: could not open port` | Check `SERIAL_PORT` in `app.py`, ensure Arduino is plugged in |
| Dashboard shows `● DISCONNECTED` | Serial thread retries every 5s automatically; check cable |
| Count never increments | Ensure sensor is within ~50cm of doorway; check TRIG/ECHO wiring |
| Firebase errors on startup | Verify `serviceAccountKey.json` is present **locally** (never commit it) and `databaseURL` in `firebase_config.py` is correct |
| Count goes negative | Normal edge case; the reset button restores to zero |
| Buzzer won't stop | Hall reached max capacity; reduce count or press Reset |

<br/>

---

## 🔮 Future Roadmap

- [ ] **Dual-sensor mode** — directional entry/exit with two HC-SR04s
- [ ] **Multi-hall support** — monitor multiple rooms from one dashboard
- [ ] **SMS/Email alerts** — notify admins when hall reaches capacity
- [ ] **Raspberry Pi deployment** — headless server with no laptop required
- [ ] **Mobile PWA** — installable dashboard for phones
- [ ] **Historical analytics** — daily/weekly occupancy heatmaps
- [ ] **QR code display** — students check capacity on their phones

<br/>

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/dual-sensor`
3. Commit your changes: `git commit -m 'Add dual-sensor mode'`
4. Push to the branch: `git push origin feature/dual-sensor`
5. Open a Pull Request

<br/>

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

<br/>

---

<div align="center">

**Built with ❤️ using Arduino + Flask + Firebase**

_If OccuPulse helped your project, please ⭐ star the repo!_

</div>
