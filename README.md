# FortiGate Bulk Firmware Upgrade Automation Tool

> ⚠️ **CRITICAL WARNING – USE AT YOUR OWN RISK**
>
> This script performs automated operations on FortiGate devices, including **configuration backup and firmware upgrade execution**.
>
> Firmware upgrades can:
>
> * Cause **device reboots**
> * Lead to **network downtime**
> * Break compatibility if upgrade path is incorrect
>
> ❗ **This script has NOT been fully tested in all environments.**
> ❗ Use only after proper validation in a **lab environment**.
> ❗ The author is NOT responsible for any outage, data loss, or damage.

---

## 📌 Overview

This tool automates **bulk FortiGate management via SSH**, with a strong focus on **safe firmware upgrade workflow**.

It follows a **2-phase approach**:

### 🧩 Phase 1: Staging (Safe)

* Ping check (reachability)
* SSH login validation
* Device detection (FortiGate only)
* Firmware version detection
* Configuration backup (mandatory)
* Upgrade eligibility check

### ⚡ Phase 2: Upgrade (Controlled)

* Runs only if explicitly enabled
* Rolling upgrade (one device at a time by default)
* Cooldown between upgrades
* Stops on failure (optional safety)

---

## 🧠 Key Features

* ✅ Multi-device SSH automation
* ✅ Automatic FortiGate detection
* ✅ Firmware version parsing
* ✅ Dual configuration backup (full + running)
* ✅ Upgrade eligibility validation
* ✅ Rolling upgrade control (prevents mass outage)
* ✅ Dry-run mode (default safe mode)
* ✅ Detailed logging

---

## 📁 Project Structure

```id="fgt1"
project/
│── main.py
│── ips.txt
│── output.log
│── backups/
```

---

## ⚙️ Requirements

* Python 3.x
* SSH access enabled on FortiGate devices

Install dependency:

```id="fgt2"
pip install paramiko
```

---

## 🔑 Configuration

Edit the script variables:

```python id="fgt3"
CREDENTIALS = [
    ("username", "password"),
]

TARGET_FORTIOS_VERSION = "7.0.14"  # Optional
DO_UPGRADE = False  # KEEP FALSE FOR DRY RUN
```

---

## 🌐 Device List

Add IPs in `ips.txt`:

```id="fgt4"
192.168.1.1
192.168.1.2
# Comments allowed
10.143.0.43
```

---

## ▶️ Usage

### 🧪 Dry Run (Recommended First)

```id="fgt5"
python main.py
```

✔ Performs:

* Connectivity check
* Backup
* Upgrade eligibility

❌ Does NOT upgrade devices

---

### ⚡ Enable Upgrade (DANGEROUS)

```python id="fgt6"
DO_UPGRADE = True
```

Then run:

```id="fgt7"
python main.py
```

---

## 🔄 Upgrade Workflow

For each device:

1. Ping check
2. SSH login
3. Detect FortiGate
4. Backup configuration
5. Check firmware version
6. Validate upgrade eligibility
7. Execute upgrade command
8. Wait for device recovery (ping)

---

## ⚠️ Safety Mechanisms

* 🔒 Backup required before upgrade
* 🔒 Refuses major version jumps
* 🔒 Stops on failure (optional)
* 🔒 Controlled concurrency (default: 1 device)
* 🔒 Cooldown between upgrades

---

## 📦 Backups

Saved in:

```id="fgt8"
backups/
```

Includes:

* Full configuration (`show full-configuration`)
* Running configuration (`show`)

---

## 📄 Logs

All results stored in:

```id="fgt9"
output.log
```

Includes:

* Status per device
* Errors
* Upgrade results
* Summary

---

## ⚠️ Important Notes (READ THIS)

* ❗ FortiGate upgrades require **proper upgrade path planning**
* ❗ Not all versions support direct upgrade
* ❗ Some upgrades require intermediate versions
* ❗ Always check Fortinet documentation
* ❗ Prefer FortiManager for production environments

---

## 🔥 Recommended Safe Workflow

1. Run **dry-run mode**
2. Verify:

   * Device detection
   * Backup success
   * Version parsing
3. Test on **1 device only**
4. Validate manually
5. Then scale gradually

---

## 🛠️ Customization

You can modify:

```python id="fgt10"
UPGRADE_COMMAND = "execute update-now"
```

⚠️ Replace with your actual approved upgrade method:

* TFTP
* HTTP
* FortiManager
* Manual staged upgrade

---

## ❗ Known Risks

* Device reboot
* Loss of connectivity
* Partial upgrade failure
* Configuration mismatch

---

## 📜 Disclaimer

This project is provided **as-is**, without any warranty.

By using this script, you agree that:

* You are fully responsible for any impact
* You understand the risks of firmware automation

---

## 🤝 Contribution

Improvements are welcome:

* Pre-check validation
* Upgrade path automation
* GUI dashboard
* Device grouping

---
