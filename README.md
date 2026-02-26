📡 Alfa Monitor Mode Enabler (Linux)
A simple Bash script to detect an Alfa Wi-Fi adapter interface and enable monitor mode automatically (Linux only).

📌 Overview
 - Alfa Monitor Mode Enabler is a lightweight Linux-only Bash utility that:
 - Detects the first available wireless interface (commonly your Alfa adapter)
 - Checks whether it is already in monitor mode
 - If not, toggles the interface down, enables monitor mode, and brings it back up
 - This is useful as a quick “prep step” before doing wireless packet capture or Wi-Fi security testing in a lab environment.

✅ Key Features
🔍 Auto-detects the Wi-Fi interface using iw dev
🧠 Checks current mode via iwconfig
⚡ Enables monitor mode automatically
🛑 Fails cleanly if no interface is detected
🧰 Minimal and easy to modify

🐧 Supported Platforms
✅ Linux only
This script relies on Linux wireless tooling (iw, iwconfig, ifconfig) and will not work on Windows or macOS.

⚙️ Requirements
Install the required tools:
Debian / Ubuntu / Kali
sudo apt update
sudo apt install -y wireless-tools iw net-tools

Fedora
sudo dnf install -y wireless-tools iw net-tools

Arch
sudo pacman -S --needed wireless_tools iw net-tools

You also need:
A compatible Wi-Fi adapter (e.g., Alfa)
Proper drivers installed (depends on chipset)

🚀 Usage
Save the script as alfa_monitor_mode.sh
Make it executable:
chmod +x alfa_monitor_mode.sh

Run it:
./alfa_monitor_mode.sh
You may be prompted for your sudo password, because changing interface mode requires elevated privileges.

🧾 What the Script Does (Step-by-step)
Reads the first detected wireless interface name:
iw dev | awk '$1=="Interface"{print $2}' | head -n 1
If no interface is found → exits with an error
Checks whether it’s already in monitor mode:
iwconfig <iface> | grep -o "Mode:Monitor"
If not → toggles the interface:
brings it down
sets mode to monitor
brings it up
Verifies whether monitor mode was enabled successfully

📌 Example Output
Alfa network card found on interface: wlan0
Enabling monitor mode for the interface wlan0...
Monitor mode successfully enabled on wlan0!
⚠️ Notes / Limitations

This script selects the first wireless interface found.
If you have multiple wireless adapters, it may choose the wrong one.
Some chipsets/drivers require using airmon-ng or iw with different steps.
Modern systems may use NetworkManager, which can interfere with mode switching.


## ⚠ Responsible Use
This tool is intended for laboratory environments, authorized security testing,
and educational research purposes only.

Wireless monitoring and packet capture may be restricted by law in many countries.
Always ensure you have explicit authorization before performing any wireless testing.

The author assumes no liability and is not responsible for misuse or damage
caused by this software.

## 📜 License
This project is licensed under the MIT License – see the LICENSE file for details.
