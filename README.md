



# Luxonis OAK-D Pro Cameras: Quick Start Guide and Troubleshooting

This repository provides instructions for setting up, troubleshooting, and customizing Luxonis OAK-D Pro Cameras, along with resources for Android and Python app integration.

---

## 1. Initial Setup

### **Hardware Setup**

1. **Power Connection**
    - Use a PoE (Power over Ethernet) setup. Connect the PoE switch to your laptop (example below).
    - Ensure all cables are securely connected.
    - Avoid connecting this switch to a router or internet-connected switch to prevent IP changes due to DHCP and ensure discoverability.

PoE Setup Example

Switch Image

---

### **Software Requirements**

1. **Visualizing the Camera**
    - Install the DepthAI Viewer:

```bash
python3 -m pip install depthai-viewer
python3 -m depthai_viewer
```

    - Use either the system-wide Python environment or a virtual environment with `conda` or `venv` for compatibility across camera generations.
2. **Install DepthAI Python Library**
    - Follow the installation steps from the [DepthAI Python repository](https://github.com/luxonis/depthai-python).

---

### **IP Configuration**

1. **Factory Reset \& Configure IP**
    - Clone the device manager from [DepthAI Utilities](https://github.com/luxonis/depthai-python/tree/main/utilities).
    - Use:

```bash
python3 device_manager.py
```

    - Recommended settings:
        - IP: `169.254.1.&lt;0-255&gt;` (default: `169.254.1.222`)
        - Subnet Mask: `255.255.0.0`
        - Gateway: `169.254.1.1`
    - To check devices on the network, use tools like Wireshark to scan the IPs on the switch.

---

## 2. Troubleshooting Common Issues

### **Soft-Bricked Device**

- **Symptoms:** Device pings but cannot connect or search for it.
- **Fix:** Factory reset the device using the OAK Programming Board:

1. Connect the programming board to the M8 connector.
2. Press and hold the Recovery button while connecting the board to your host device.
3. Use the "Factory Reset" option in the Device Manager tool.

---

### **Camera Not Detected**

- **Symptoms:** Camera not showing in the device list or "RuntimeError: Failed to find device after booting."
- **Fix:**
    - Ensure the latest DepthAI version is installed.
    - Check USB or PoE connections.
    - Perform a factory reset.

---

### **Flashing or Random Disconnects**

- **Symptoms:** Disconnections caused by `Node.warn` messages interfering with TCP connections.
- **Fix:** Use the script available in the Blindspot Monitoring utilities.

---

### **Calibration Issues**

- **Symptoms:** Depth measurements are inaccurate or calibration fails.
- **Fix:**
    - Run the `calibrate.py` script from the DepthAI repository.
    - Verify left and right cameras aren't swapped during setup.

---

### **Focus and White Balance Problems**

- **Symptoms:** Autofocus varies randomly or images are inconsistent.
- **Fix:**
    - Adjust focus and white balance using RGB camera controls via presets.

---

## 3. Customization Options

### **Pipeline Adjustments**

- Customize the camera’s pipeline based on application needs using compatible models and decoding logic.


### **App Integration**

- Update decoding logic in the app’s Kotlin file if camera data changes.
- Set ports and IP configurations in the Android app's `MainActivity`.

---

## 4. Resources

- [Blindspot Monitoring Utilities](https://github.com/Brunswick-BI-Design-Lab/Blindspot_Monitoring/tree/main)
- [DepthAI Python Repository](https://github.com/luxonis/depthai-python)
- Android App Code Repository: [BlindspotMonitoringV2](https://github.com/Brunswick-BI-Design-Lab/BlindspotMonitoringV2)

---

## 5. Android Quick Start

### **Hello World Application**

This application streams data and video from the camera to an Android display.

- Clone the repository:

```bash
git clone https://github.com/Brunswick-BI-Design-Lab/Blindspot_Monitoring
cd Blindspot_Monitoring/utilities
```

- **Flash the Camera:**

```bash
python oakyolodepth.py --port XXXX
```

Replace `XXXX` with the desired port. Ensure only one camera is connected during flashing for clarity.
- Android Client Code:
Check the `CameraSocket.kt` in the [BlindspotMonitoringV2 Repo](https://github.com/Brunswick-BI-Design-Lab/BlindspotMonitoringV2/blob/master/app/src/main/java/com/example/blindspotmonitoringv2/CameraSocket.kt).
- Open the hackathon branch in Android Studio to set up a simple Android app with video streaming.

---

## 6. Python Client Example

Use the Python client on a local machine to stream camera data:
[Python Tester Script](https://github.com/Brunswick-BI-Design-Lab/Blindspot_Monitoring/blob/main/utilities/tester2.py)




