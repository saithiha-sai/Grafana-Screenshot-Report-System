# Grafana Automation Script – README

## Overview

This Python automation script is designed to **open Grafana dashboards, capture screenshots, intelligently crop specific monitoring panels using OCR, and send the results directly to Telegram**. It is mainly used for **daily infrastructure monitoring reports** such as storage, backup, and vCenter utilization.

The script uses **Firefox browser automation**, **OCR-based text detection**, and **Telegram Bot API integration** to fully automate the monitoring workflow.

---

## Key Features

* Automatically opens Grafana dashboards in Firefox
* Captures full-page screenshots
* Uses **EasyOCR** to locate specific panel titles
* Crops only required sections from dashboards
* Sends cropped images to a Telegram chat
* Supports scrolling for long dashboards

---

## Technologies Used

* **Python**
* **PyAutoGUI** – UI automation and screenshots
* **OpenCV (cv2)** – Image processing
* **EasyOCR** – Text detection for smart cropping
* **Firefox Browser** – Dashboard rendering
* **Telegram Bot API** – Alert and report delivery

---

## Prerequisites

Before running the script, ensure the following are installed:

```bash
pip install pyautogui opencv-python easyocr requests
```

Additional requirements:

* Mozilla Firefox installed
* Active Grafana access (URL reachable)
* Telegram Bot Token and Chat ID

---

## Configuration

### 1. Telegram Configuration

```python
BOT_TOKEN = "<YOUR_BOT_TOKEN>"
CHAT_ID = "<YOUR_CHAT_ID>"
```

Used to send captured images to Telegram.

---

### 2. Screenshot Save Directory

```python
save_dir = r"C:\Users\Sai Thiha\Desktop\Grafana_Shots"
```

All screenshots and cropped images are stored here.

---

### 3. Firefox Browser Path

```python
firefox_path = r"C:\Program Files\Mozilla Firefox\firefox.exe"
```

Ensures the script launches Firefox explicitly.

---

## Script Workflow

### Step 1: Open Grafana Dashboard

The script opens a Grafana dashboard URL using Firefox and waits for it to fully load.

### Step 2: Capture Screenshot

A full-screen screenshot of the dashboard is taken using PyAutoGUI.

### Step 3: OCR-Based Cropping

EasyOCR scans the screenshot to locate **start and end panel titles**, then crops only the required section.

### Step 4: Close Browser

Firefox is automatically closed after capturing the screenshot.

### Step 5: Send to Telegram

Cropped images are sent to the configured Telegram chat.

---

## Dashboards Captured

### 1. AYA-RV Data Domain Storage

* URL: System Team Daily Overview
* Cropped panel: **Backup Storage Usage**
* Output: `BackupStorage.png`

---

### 2. Dell PowerStore Utilization

* URL: Dell PowerStore Dashboard
* Cropped panel: **Storage Utilization**
* Output: `Dell.png`

---

### 3. vCenter Overview Utilization

* Scroll-enabled capture
* Cropped panel: **vCenter Utilization Overview**
* Output: `vCenterOverviewUtilization.png`

---

## Helper Functions Explanation

### `capture_grafana()`

* Opens Grafana URL
* Waits for dashboard to load
* Scrolls page if required
* Takes screenshot
* Closes Firefox

---

### `crop_section()`

* Uses OCR to detect start and end text
* Dynamically calculates crop area
* Saves cropped image

---

### `send_photo()`

* Sends image file to Telegram
* Includes filename as caption

---

## Use Case

* Daily infrastructure monitoring
* Automated NOC reporting
* Storage & virtualization health reporting
* Core banking infrastructure monitoring support

---

## Notes & Limitations

* Screen resolution should remain consistent
* Grafana panel titles must match OCR text
* Firefox window should stay in foreground

---

## Future Enhancements

* Headless browser support (Selenium)
* Error alerting via Telegram
* Scheduling via Task Scheduler / Cron
* Grafana API-based capture (no UI automation)

---

## Author

**Sai Thiha**
IT System & Automation Engineer

---
This script significantly reduces manual monitoring effort and improves operational visibility through automated reporting.
