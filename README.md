CIP-B106 Mobile and IoT Forensics - Echo Show 8 Case Study Evidence and Investigation Report Repository.
# 🛡️ CIP-B106: MOBILE AND IOT FORENSICS
## Comprehensive Digital Forensic Investigation Report: Amazon Echo Show 8 IoT Evidence Analysis

[![ICDFA Standards](https://img.shields.io/badge/Standard-ICDFA%20Forensic-blue.svg)](https://icdfa.org)
[![Assessment](https://img.shields.io/badge/Assessment-Case%20Study%203-success.svg)]()
[![Forensic Status](https://img.shields.io/badge/Status-Verified%20%26%20Complete-orange.svg)]()
[![Compliance](https://img.shields.io/badge/Compliance-ISO%2FIEC%2027037-yellow.svg)]()

---

## 📑 1. Executive Summary & Case Overview
This repository hosts the official, verified digital forensic investigation report and analytical documentation for **Case Study 3 (Echo Show 8 IoT Evidence Investigation)**, completed under the **CIP-B106** module at the **International Cybersecurity and Digital Forensics Academy (ICDFA)**. 

The primary objective of this case study is to perform a rigorous, non-destructive, device-level forensic reconstruction of an **Amazon Echo Show 8 (1st Gen / Board Name: `AEOAT`, Codename: `athena`)** smart display device. The examination utilizes an authorized physical eMMC memory dump archive (`EMMC_8GTF4R_ROM1`, ~2.3 GB) and structured logical extraction directories (`Lab_4_1_1` through `Lab_4_3_1`). 

In strict compliance with **ISO/IEC 27037** guidelines for digital evidence handling, all procedures were conducted using write-blocking methodologies, read-only mounts, and verifiable binary inspections. No cloud accounts were accessed, and no live network transmissions were triggered, ensuring absolute evidentiary integrity.

---

## 🔬 2. Technical Investigation Scope & Methodology

The investigation is methodically partitioned into six core forensic phases, addressing hardware profiling, operating system architecture, network configurations, web activity, VoIP communications, media carving, and multi-artifact timeline correlation.

### 📌 Task A: Evidence Preservation, Scope & Acquisition Audit
* **Primary Image Container:** `EMMC_8GTF4R_ROM1_0000000000000000_0001D20000000000.7z` (~2.3 GB physical eMMC dump).
* **Extraction Manifest & Error Auditing:** Parsed the extraction audit log (`__All_Errors.txt`, Correlation ID: `ecc17369-3fe5-4e75-89db-912a8fdcb065`) which recorded specific acquisition boundaries and limitations:
  * *Unextracted XML Artifacts:* `Lab_4_2_2/recovered-xml/xml-0-3` and `xml-0-8` were absent from the logical container.
  * *Missing Carved JPEGs:* 24 specific carved image sectors (`13082855.jpg` to `13097724.jpg`) failed during initial logical parsing.
* **Forensic Qualification:** Rather than fabricating data or assuming cloud presence, these gaps are formally documented as source-level acquisition limitations, satisfying evidentiary standards.

### 📌 Task B: Device Profiling & Operating System Architecture
* **Low-Level Build Properties (`build.prop`):**
  * *Hardware Board / Model:* `AEOAT` (`ro.product.model=AEOAT`)
  * *Codename / Platform:* `athena` (`ro.product.device=athena`)
  * *Operating System:* Fire OS based on Android 9 / Pie (`ro.build.version.release=9`, SDK 28)
  * *System Build ID:* `PS7560.3677N` (`ro.build.display.id=PS7560.3677N`)
  * *Compilation Timestamp:* Thu Sep 21 02:41:50 UTC 2023 (`ro.build.date.utc=1695264110`)
* **Device Naming Configuration (`deviceNameSharedPref.xml`):**
  * Identified assigned system display label: `<string name="deviceNameKey">Amazing Assistant</string>`.
* **User Accounts & Security Enforcements (`userlist.xml` & Databases):**
  * Primary system User ID confirmed as `0` (`<user id="0"/>`) with Device Owner ID `-10000`.
  * Enforced guest security restriction policies: SMS disabled (`no_sms="true"`), sideloading blocked (`no_install_unknown_sources="true"`), Wi-Fi reconfiguration restricted (`no_config_wifi="true"`), and outgoing calls blocked (`no_outgoing_calls="true"`).
  * Associated Credential/Device Encrypted databases: `accounts_ce.db` (40 KB) and `accounts_de.db` (64 KB).

### 📌 Task C: Network Connectivity & Wireless Analysis
* **Wireless Access Point Binding (`WifiConfigStore.xml`):**
  * SSID: `"Fios-pJK9q"`
  * Key Management: WPA2-PSK (`ConfigKey: Fios-pJK9qWPA_PSK`)
  * Pre-Shared Key (Raw): `cop576him662ill`
  * Interface Status: Validated Internet Access (`true`), Association count: `9`.
* **Bluetooth Subsystem & Peripheral Pairing (`bt_config.conf`):**
  * Host MAC Address: `b0:f7:c4:41:cc:93` (Name: `"Echo Show 8 (2nd Gen)-3SD"`)
  * Paired Peripheral Target: `"Sarfraz’s MacBook Pro"` (MAC: `f4:5c:89:c7:54:f0`)
  * Extracted Pairing Link Key: `32be2e808a74ec0559411eecbb7cd975`.

### 📌 Task D: Web Browsing & SIP Communication Analysis
* **Web Browser Artifacts (`Lab_4_2_1/History`):**
  * File Size: 256 KB.
  * Manual Binary Inspection: Verified valid SQLite header bytes (`SQLite format 3`) and internal WebKit schema tables (`visits`), confirming active local browser rendering.
* **VoIP / SIP Communication State (`chatgptJSON.json`):**
  * Framework & Domain: Amazon Alexa Communications (`Domain:Application:Communications:Calling`).
  * Call Parameters: Call ID `5c32191e-c27f-472e-a81f-50e7dce5788f`, Call State: `CALLING`, Provider: `Bacon`.
  * Participant Endpoint Mapping: Caller ID `amzn1.comms.id.hg.amzn1~HH3Q6VLVSQSPYV2` targeting Callee Display Name `"Hibna Sarfraz"`.
  * Timestamp Metrics: Absolute Device Timestamp `1697926862078` (Epoch ms, Oct 2023).

### 📌 Task E: Multimedia Evidence & File Carving
* **Carved Static Assets (`Lab_4_3_1/rec_jpg_foremost/`):**
  * Carving Tool: `Foremost version 1.5.7` executed against the 7 GB eMMC image source (`7818182656 bytes`).
  * Recovered Artifacts: Static JPEGs, album art, and UI background graphics logged in `audit.txt` with precise block offsets (`bs=512`).

### 📌 Task F: Manual Tool Validation, Chronology & Finding Log
* **Manual Tool Validation:** Verified automated SQLite parser output against raw binary headers (`SQLite format 3` in Notepad), confirming structural integrity without data corruption.
* **Corroborated 24–72 Hour Chronology:** Mapped system initialization (`build.prop`), Bluetooth provisioning (`bt_config.conf`), WPA binding (`WifiConfigStore.xml`), user provisioning (`userlist.xml`), web session logs (`History`), and SIP calls (`chatgptJSON.json`) into a cohesive timeline.
* **Comprehensive Finding Log:** Documented formal findings **F-01 through F-08**, establishing strict evidential qualifications and material limitations.

---

## 📂 Repository File Structure

```text
├── CIP-B106_CaseStudy3_C1126DFIT17289_Muzamil.pdf  # Official 100-mark formal academic forensic report
└── README.md                                       # Exhaustive technical case brief write-up & documentation
