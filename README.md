Here’s your complete and refined `README.md` for the **Blink-AI** project in **Markdown**, combining all your features, architecture, and breakdown into a polished and cool format:

```markdown
# ⚡ Blink-AI

**Blink-AI** is a powerful Android-based remote control system that lets you turn one phone into a wireless **mouse + keyboard** controller for another Android device. Whether you're navigating, typing, or clicking—Blink-AI brings seamless remote interaction to your fingertips.

<p align="center">
  <img src="https://img.shields.io/badge/platform-Android-green" />
  <img src="https://img.shields.io/badge/language-Kotlin-blue" />
  <img src="https://img.shields.io/badge/client--server-TCP%2FJSON-purple" />
  <img src="https://img.shields.io/badge/keyboard%20%2B%20mouse-enabled-orange" />
</p>

---

## 🚀 Features

- 🖱️ Virtual Touchpad for full mouse control (tap, swipe, scroll)
- ⌨️ Keyboard Input for typing on a connected device
- 🔢 Numpad UI for numbers and special keys
- 🌐 TCP-based communication using JSON (GSON)
- 💡 Gesture support: tap, scroll, drag, and multi-touch
- 🧠 Modular and scalable Kotlin codebase

---

## 🧭 Architecture

```
Blink-AI-Final/
├── client/        # Mousedroid app (Controller)
│   ├── src/       # Kotlin logic for UI, touch, keyboard, and networking
│   └── res/       # UI layouts, drawables, themes
├── server/        # Android server that receives and acts on input
│   └── src/       # Logic to decode and process control commands
├── shared/        # Common models and interfaces (e.g., Command.kt)
└── README.md
```

### 📡 Communication Flow

1. **Client (Mousedroid)** starts and connects to a target IP via `TcpClient.kt`
2. Sends touch gestures and key events encoded as JSON using GSON
3. **Server (Blink-AI)** receives and interprets the commands
4. Server performs actions like moving cursor, clicking, or typing

---

## 🧠 Core Modules

| Module / File | Description |
|---------------|-------------|
| `MainActivity.kt` | Launch and permission logic |
| `SelectDeviceActivity.kt` | Lists available devices to connect |
| `InputActivity.kt` | Hosts fragments for touchpad, keyboard, numpad |
| `TouchpadFragment.kt` | Gesture UI and logic for mouse input |
| `GestureHandler.kt` | Converts gestures into command objects |
| `KeyboardInputWatcher.kt` | Captures and sends key inputs |
| `TcpClient.kt` | Maintains socket connection to server |
| `DeviceAdapter.kt` | RecyclerView for device listing |

---

## 🖥️ Server Functionality

- Built as an Android app (server APK)
- Listens on a socket for incoming JSON commands
- Parses commands like:
  - `{"action": "move", "dx": 15, "dy": -5}`
  - `{"action": "tap"}`
  - `{"action": "type", "key": "H"}`

Handles them in real-time using Kotlin's multithreading and event-handling.

---

## 📲 Installation

### ✅ Requirements

- Android 7.0 (API 24) and above
- Kotlin-compatible environment
- Two Android devices on the same network

### 🔧 Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/SarthSatpute/Blink-AI-Final.git
   ```

2. **Open in Android Studio**
   - Open both `client/` and `server/` folders as separate projects or modules.

3. **Build APKs**
   - Use `Build > Build Bundle(s) / APK(s) > Build APK` from Android Studio

4. **Install on Devices**
   - Install the client APK on the controller phone
   - Install the server APK on the target phone

5. **Connect & Control**
   - Launch both apps and connect using device IP
   - Start controlling with touch and keyboard!

---

## 🛠️ Dependencies

- [Kotlin](https://kotlinlang.org/)
- [GSON](https://github.com/google/gson) for JSON parsing
- AndroidX, Material Components
- Custom TCP Socket implementation

---

## 💡 Future Plans

- 🔐 Secure communication via encryption
- 📶 Add Bluetooth & Wi-Fi Direct support
- 🖥️ Screen preview on client side
- 🧩 Plug-in architecture for custom control modules
- 🧪 Robust unit tests and UI automation

---

## 🤝 Contributing

Pull requests are welcome! Fork the repo and submit a PR if you'd like to:
- Fix bugs 🐛
- Add features 🚀
- Improve UI 🎨

---
