# 🤖 Arduino Line Follower Robot

A simple, reliable **line following robot** built on an Arduino-based EDVON kit. It uses three analog IR sensors to track a black line on a white surface and two DC motors to steer, with a smart "line lost" recovery mode.

> Built by **Hamza Khan**, Computer Engineering student at Usman Institute of Technology (UIT).

---

## ✨ Features

- **3 IR sensors** (left, centre, right) read with `analogRead()` and a tunable threshold
- **Gentle corrections** for small drifts and **sharp turns** for 90° corners
- **Crossing handling** – goes straight when all three sensors see black
- **Line recovery** – if the line is lost, the robot spins toward the side where it last saw the line
- **Safety timeout** – motors stop automatically if the line is not found within 2 seconds
- **2-second start delay** so you can place the robot on the track
- Clean, commented code with all speeds and pins easy to change at the top

---

## 🧰 Hardware

| Part | Quantity |
|------|----------|
| Arduino-based EDVON robot kit / board | 1 |
| IR line sensors (analog output) | 3 |
| DC gear motors | 2 |
| Motor driver (on the EDVON board) | 1 |
| Battery pack | 1 |
| Black line track on a white surface | – |

---

## 🔌 Pin Connections

| Component | Pin | Function |
|-----------|-----|----------|
| Left motor | D2 | Direction 1 |
| Left motor | D3 | PWM (speed) |
| Left motor | D4 | Direction 2 |
| Right motor | D5 | Direction 1 |
| Right motor | D6 | PWM (speed) |
| Right motor | D7 | Direction 2 |
| Left IR sensor | A4 (IR-L) | Analog input |
| Centre IR sensor | A3 (IR-M) | Analog input |
| Right IR sensor | A2 (IR-R) | Analog input |

---

## 🧠 How It Works

Each sensor reports a number between 0 and 1023. A value **below 525** means the sensor is over the **black line**; above 525 means white floor.

Think of it like walking on a path in the dark with a torch on each shoulder: if the left side lights up the path edge, you step left to correct; if you lose the path completely, you turn back toward the side where you last saw it.

| Left | Centre | Right | Action |
|:----:|:------:|:-----:|--------|
| ⬛ | ⬛ | ⬛ | Go forward (crossing) |
| ⬜ | ⬛ | ⬜ | Go forward (on the line) |
| ⬛ | ⬛ | ⬜ | Gentle left |
| ⬜ | ⬛ | ⬛ | Gentle right |
| ⬛ | ⬜ | ⬜ | Sharp left |
| ⬜ | ⬜ | ⬛ | Sharp right |
| ⬛ | ⬜ | ⬛ | Go forward |
| ⬜ | ⬜ | ⬜ | Line lost → spin toward last known side, stop after 2 s |

---

## 🚀 Getting Started

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/arduino-line-follower-robot.git
   ```
2. Open `LineFollower/LineFollower.ino` in the **Arduino IDE**.
3. Select your board and COM port from the **Tools** menu.
4. Click **Upload**.
5. Place the robot on the black line. After a 2-second delay it starts moving.

---

## ⚙️ Tuning

All settings are at the top of `LineFollower.ino`:

| Setting | Default | What it does |
|---------|---------|--------------|
| `IR_THRESHOLD` | 525 | Black/white cut-off. Adjust if your track or lighting is different |
| `SPD_FWD` | 180 | Normal forward speed |
| `SPD_FAST` | 220 | Outer wheel speed in sharp turns |
| `SPD_SLOW` | 80 | Inner wheel speed in gentle turns |
| `SPD_SEARCH` | 150 | Spin speed when searching for the line |
| `SEARCH_TIMEOUT` | 2000 ms | How long to search before stopping |

**Tips**
- Robot wobbles too much? Lower `SPD_FWD` or raise `SPD_SLOW`.
- Robot misses sharp corners? Lower `SPD_FWD` a little.
- Sensors misreading? Print `analogRead()` values on the Serial Monitor over black and white and set the threshold halfway between them.

---

## 📁 Project Structure

```
arduino-line-follower-robot/
├── LineFollower/
│   └── LineFollower.ino   # Main Arduino sketch
├── README.md
└── LICENSE
```

---

## 🔮 Future Improvements

- PID control for smoother, faster tracking
- Auto-calibration of the sensor threshold at startup
- Support for 5-sensor arrays
- Bluetooth start/stop control

---

## 📜 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## 👤 Author

**Hamza Khan**
Computer Engineering, Usman Institute of Technology (UIT)

Feel free to fork the project, open an issue, or send a pull request. ⭐ Star the repo if it helped you!
