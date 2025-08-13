# Battery Monitor for HP Laptops (and others without charging-stop features)

A lightweight Python-based battery monitor for Windows systems (HP, etc.) that don't support manufacturer-provided charge limit tools (unlike Asus "Battery Health Charging" or Lenovo "Charge Threshold"). It auto-starts at login, runs silently in the background, and notifies you when your battery’s charge level crosses configurable thresholds.

---

##  Features

- **Works on HP and other laptops** with no native charging-stop support.
- **Portable, single-file executable** (`batteryMonitor.exe`) built with PyInstaller.
- **Auto-start on login** via Windows Startup (no admin rights required).
- **Background monitoring**, with low CPU & memory footprint.
- **Desktop notifications** when battery drops below or exceeds thresholds.
- **Fully customizable thresholds** (`LOW_BATTERY_THRESHOLD`, `HIGH_BATTERY_THRESHOLD`).
- **Optional Windows Service** variant for truly invisible operation.

---

##  How It Works

1. On first run, the executable copies itself to the user’s Startup folder and deletes the original, ensuring it launches on every login automatically.
2. Runs a simple battery-check loop:
   - Notifies when battery ≤ LOW threshold and not plugged in.
   - Notifies when battery ≥ HIGH threshold and plugged in.
3. Uses **`psutil`** for battery status and **`plyer`** for cross-platform notifications.
4. Compiled as a **console-hidden** `.exe` with **PyInstaller**, embedding your own `.ico` file for icons.

---

##  Getting Started

### Prerequisites
- Python 3.8+
- `psutil`, `plyer`, [`flask`] (optional)
- Windows OS

### Setup & Build

```bash
git clone https://github.com/your-username/battery-monitor-hp.git
cd battery-monitor-hp

# (Optional) create a virtual environment:
python -m venv venv
venv\Scripts\activate

pip install psutil plyer

# Build the executable
pip install pyinstaller
pyinstaller --onefile --noconsole --icon=battery.ico batteryMonitor.py
