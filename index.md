<div align="center">

<br>

# 🚁 Parrot Drone Simulation

**A full simulation environment for autonomous drone development, no hardware required.**

<br>



[![AirSDK Docs](https://img.shields.io/badge/📦_AirSDK-Drone_SDK-0A84FF?style=for-the-badge&logoColor=white)](https://developer.parrot.com/docs/airsdk/index.html)
[![Sphinx Docs](https://img.shields.io/badge/🌍_Sphinx-UE_Simulator-6C47FF?style=for-the-badge&logoColor=white)](https://developer.parrot.com/docs/sphinx/masterindex.html)
[![Olympe Docs](https://img.shields.io/badge/🐍_Olympe-Python_SDK-22C55E?style=for-the-badge&logoColor=white)](https://developer.parrot.com/docs/olympe/index.html)
[![Demo Mission](https://img.shields.io/badge/🧪_Demo-Hello_Mission-F59E0B?style=for-the-badge&logoColor=white)](https://github.com/Parrot-Developers/airsdk-samples/tree/master/hello)

<br>

![Platform](https://img.shields.io/badge/Platform-Linux%20%2F%20Ubuntu%2020.04-E11D48?style=flat-square&logo=ubuntu&logoColor=white)
![Language](https://img.shields.io/badge/Language-Python-3B82F6?style=flat-square&logo=python&logoColor=white)
![Simulator](https://img.shields.io/badge/Simulator-Unreal%20Engine-9333EA?style=flat-square&logo=unrealengine&logoColor=white)
![Status](https://img.shields.io/badge/Status-Research%20%2F%20Demo-10B981?style=flat-square)

</div>

---
## 📘 Documentation Notice
> This guide provides a simplified setup workflow based on the official Parrot documentation.  
> For detailed instructions, troubleshooting, or updated information,  
> please refer to the official docs linked below, they remain the authoritative source.

---

## ⚠️ Compatibility

> **Parrot software is only supported on Linux (Debian/Ubuntu).**  
> Official testing was performed on **Ubuntu 20.04 LTS**.

---

## 🚀 Quick Start

<details>
<summary><b>1️⃣ &nbsp;Install Parrot AirSDK</b></summary>

<br>

```bash
# Add Parrot repository & GPG key
curl https://debian.parrot.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/debian.parrot.com.gpg
echo "deb [signed-by=/usr/share/keyrings/debian.parrot.com.gpg] https://debian.parrot.com/ $(lsb_release -cs) main generic" \
  | sudo tee /etc/apt/sources.list.d/debian.parrot.com.list > /dev/null
sudo apt update

# Install AirSDK
sudo apt install parrot-airsdk-cli
```

</details>

<details>
<summary><b>2️⃣ &nbsp;Install Parrot Sphinx (Simulator)</b></summary>

<br>

```bash
# Add Parrot repository & GPG key (if not already done in step 1)
curl --fail --silent --show-error --location https://debian.parrot.com/gpg \
  | gpg --dearmor \
  | sudo tee /usr/share/keyrings/debian.parrot.com.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/debian.parrot.com.gpg] https://debian.parrot.com/ $(lsb_release -cs) main generic" \
  | sudo tee /etc/apt/sources.list.d/debian.parrot.com.list
sudo apt update

# Install Sphinx
sudo apt install parrot-sphinx

# (Optional) List all available Unreal worlds
apt-cache search parrot-ue4

# Install the empty world (recommended for testing)
sudo apt install parrot-ue4-empty
```

</details>

<details>
<summary><b>3️⃣ &nbsp;Install Parrot Olympe (Python SDK)</b></summary>

<br>

```bash
pip3 install parrot-olympe
```

</details>



<details>
  
<summary><b>4️⃣ &nbsp;Quickstart Simulation (Run your first flight)</b></summary>

<br>

Open multiple terminals, each component runs separately.

### 🖥️ Terminal 1 — Firmware & Drone Simulation

Start the firmware service:

```bash
sudo systemctl start firmwared.service
```

Launch the drone simulation (Anafi AI PC firmware):
```bash
sphinx "/opt/parrot-sphinx/usr/share/sphinx/drones/anafi_ai.drone"::firmware="https://firmware.parrot.com/Versions/anafi2/pc/%23latest/images/anafi2-pc.ext2.zip"
```
### 🌍 Terminal 2 — Unreal Engine World

Start the world you installed (example: empty world):
```bash
parrot-ue4-empty
```
For better performance add the low quality flag:
```bash
parrot-ue4-empty -quality=low
```
👉 Available worlds are listed in the Sphinx documentation under
“3D Scenes Available”

### 🎮 Optional Terminal 3 — Virtual Controller

If you want to manually control the drone without hardware:

Install QDroneCtrl:
```bash
sudo apt install parrot-tools-qdronectrl
```
Start the drone controller:
```bash
qdronectrl
```
</details>
<details>
<summary><b>5️⃣ &nbsp;Connect ADB for Debugging</b></summary>

<br>

ADB allows you to access the drone firmware shell for debugging and inspection.
For debug it is important that the simulation and firmware is up and running.

### 📦 Install ADB

```bash
sudo apt install adb
```

### 🔗 Connect to the simulated drone

```bash
adb connect 10.202.0.1:9050
```

If the connection is successful, you should see:
connected to 10.202.0.1:9050

### 🐚 Open a remote shell
```bash
adb -s 10.202.0.1:9050 shell
```
You now have terminal access to the drone firmware.

</details>

---

## 📖 Documentation

| Component | Description | Link |
|-----------|-------------|------|
| 📦 **AirSDK** | Core drone SDK for mission programming | [→ Open Docs](https://developer.parrot.com/docs/airsdk/index.html) |
| 🌍 **Sphinx** | Unreal Engine-based flight simulator | [→ Open Docs](https://developer.parrot.com/docs/sphinx/masterindex.html) |
| 🐍 **Olympe** | Python control library for Parrot drones | [→ Open Docs](https://developer.parrot.com/docs/olympe/index.html) |
| 🎮 **QDroneCtrl** | Virtual controller (no hardware needed) | [→ Open Docs](https://developer.parrot.com/docs/sphinx/local_controllers.html#qdronectrl) |
| 🧪 **Hello Mission** | Minimal demo to get started | [→ Open Repo](https://github.com/Parrot-Developers/airsdk-samples/tree/master/hello) |

---

## 💡 Performance Tips

```
⚙️  Use -quality=low when launching the Unreal world to reduce GPU load
🎮  Use QDroneCtrl if you don't have a physical Parrot controller
🐞  Debug via ADB on 10.202.0.1:9050
💻  A dedicated GPU is strongly recommended
```

---

<div align="center">

<br>

<br>

*Built for the Presentation of Paul Gässler · Powered by AirSDK + Sphinx + Olympe*

<br>

</div>
