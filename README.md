# Public Disclosure: Firmware Analysis & Open Source License Audit

This repository serves as a factual, public compliance audit and technical disclosure for the ESP32 "RollingClockModular" firmware distributed by **Timothy Mwala** (`official.timothymwala@gmail.com`). 

The upstream project distributes an opaque, pre-compiled binary block within an empty repository structure. This audit documents multiple open-source license violations alongside the hardware configuration and a technical analysis of the firmware's authentication paywall.

---

## 1. Hardware & System Architecture
* **Target Processor:** Tensilica Xtensa LX6 Dual-Core 32-bit Microprocessor (ESP32).
* **Instruction Set:** Xtensa Architecture ISA Version 6.
* **Compilation Timeline:** Stamped on June 12, 2023 (`Jun 12 2023`).
* **Underlying Kernel:** FreeRTOS v10.4.3 (Inherited from the ESP-IDF framework baseline).

---

## 2. Bypassing the Serial/UI Activation Lock
The firmware implements a commercial paywall interface that locks functionality until an access code is entered. Technical analysis reveals this mechanism is not cryptographic and does not communicate with a validation server. It checks user input against a single plaintext string compiled directly into the binary data layout.

* **Trigger Interface Loop:**
  ```text
  === Device locked ===
  Send: UNLOCK <code>
  Contact official.timothymwala@gmail.com for a code
  Enter Access Code
  ```
* **Universal Master Unlock Key:** `201995`
* **Success Indicator:** Sending `UNLOCK 201995` via the serial console or entering it into the interface flips the internal state variable `lic_ok` to `true`, permanently unlocking the device functionalities.

---

## 3. Open Source License Violations Matrix
While the developer commercializes this binary and charges transaction fees via PayPal, the entire stack relies on copyleft and permissive open-source frameworks. The distribution methods fail to meet the bare minimum legal obligations of these licenses:

| Component / Library | License Type | Infraction / Compliance Failure | Evidence Strings Found |
| :--- | :--- | :--- | :--- |
| **PlatformIO Arduino Core** | **LGPL v2.1** | **Violation.** Static linkage requires providing source or unlinked object files (`.o`/`.a`) to allow user relinking. | `arduino-lib-builder`, `otadata`, `spiffs`, `coredump` |
| **TFT_eSPI Display Driver** | **LGPL v2.1** | **Violation.** Closed distribution of derivative work without providing mechanism for user relinking. | `TFT_eSPI`, `Sprite alloc failed` |
| **Apache MyNewt NimBLE** | **Apache 2.0** | **Violation.** Permissive but requires prominent copyright attributions and license text files. | `NimBLE initialization failed`, `Failed to get NimBLE scanner instance` |
| **Improv Wi-Fi** | **Apache 2.0** | **Violation.** Direct use of the onboarding protocol without including mandatory license disclosures. | `QR via BLE provisioning`, `improv` |
| **LVGL Graphics Library** | **MIT License** | **Violation.** Fails the mandatory requirement to include original copyright and permission notices. | `Touch Calibration`, `Tap each target as it appears`, `Animations Page` |
| **FreeRTOS Kernel** | **MIT License** | **Violation.** Fails the mandatory requirement to include original copyright and permission notices. | `esp-idf: v4.4.5 ac5d805d0e`, task creation headers |

---

## 4. Analysis of External Integrations & API Plumbing
The firmware does not utilize a custom backend infrastructure. It relies entirely on standard HTTP client libraries to query public telemetry networks, parsing the data locally via embedded JSON libraries.

### Network Time Sync (NTP)
The firmware checks three hardcoded targets to manage the local RTC system clock:
* `time.nist.gov`
* `pool.ntp.org`
* `UTC%c%02d:%02d`

### Weather & Geocoding APIs
* **Open-Meteo (No-Key Baseline):**
  * Geocoding: `https://open-meteo.com`
  * Forecast: `https://open-meteo.com...`
* **OpenWeatherMap (Premium Fallback):**
  * Current: `https://openweathermap.org`

### AI Insights Payload
The "custom weather insights" feature utilizes a standard HTTP proxy call sending user configuration details straight to OpenAI API infrastructure:
* **Endpoint:** `https://openai.com`
* **Target Model:** `gpt-4o-mini`
* **System Prompt:** `"You are a concise weather assistant. Keep replies under 2 sentences."`

---

## 5. Remediation Requirements
To correct these active software compliance infractions, the distributing developer must immediately alter the repository structure to:
1. Provide the complete public source code or unlinked build object files to satisfy LGPL v2.1 terms for `TFT_eSPI` and the `Arduino Core`.
2. Include full legal attributions, copyright headers, and license copies for all `Apache 2.0` and `MIT` components utilized.
