# Eval Prompts: source-first-citation

---

## Prompt 1 — POSITIVE

**Prompt:**
> "Here's my sensor_driver.c. The temperature readings are always 0. What's wrong?
> ```c
> float read_temperature() {
>     uint8_t data[2];
>     i2c_read(SENSOR_ADDR, data, 2);
>     return (data[0] << 8 | data[1]) / 100.0;
> }
> ```"

**Expected Behavior:** Agent analyzes the provided code, not general I2C practices. Cites `read_temperature()` function. Identifies potential issues in the provided code (e.g., missing I2C init check, endianness, sensor-specific register read sequence).

**Pass Criteria:** Response references `read_temperature()`, `data[0]`, `data[1]`, `SENSOR_ADDR` from the provided code. Does not invent functions or variables not shown.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "Look at this boot log. Why is WiFi failing to connect?
> ```
> I (423) wifi: mode : sta (aa:bb:cc:dd:ee:ff)
> I (425) wifi: STA_START
> W (5426) wifi: timeout, state: 2
> E (5427) wifi: esp_wifi_connect: 0x3007
> ```"

**Expected Behavior:** Agent analyzes the provided log output. References specific log lines (state: 2, error 0x3007). Uses ESP-IDF error codes from the log.

**Pass Criteria:** Cites specific log entries. Labels any ESP-IDF documentation reference as external. Does not fabricate error code meanings.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "Based on my platformio.ini, am I using the right framework version?
> ```ini
> [env:esp32s3]
> platform = espressif32@6.5.0
> board = esp32-s3-devkitc-1
> framework = arduino
> ```"

**Expected Behavior:** Analyzes the provided platformio.ini. References `platform = espressif32@6.5.0` and `framework = arduino` directly.

**Pass Criteria:** Cites specific lines from the provided config. Does not assume different settings.

---

## Prompt 4 — NEGATIVE

**Prompt:**
> "How does the ESP32 WiFi stack work internally?"

**Expected Behavior:** General knowledge question. No user sources provided. Agent answers from general knowledge without source-first behavior.

**Pass Criteria:** No source citation attempted (no sources were provided).

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "What are the best practices for I2C bus design?"

**Expected Behavior:** General best practices question. No user sources. Direct answer or structured response.

**Pass Criteria:** No source-first behavior activated.

---

## Prompt 6 — POSITIVE (Boundary)

**Prompt:**
> "Here's my schematic description: SDA is on GPIO21, SCL on GPIO22. I'm using 4.7k pull-ups to 3.3V. The sensor is an SHT30 at address 0x44. Is this setup correct?"

**Expected Behavior:** Agent works with the provided schematic description as source material. References the specific GPIO numbers, pull-up values, and sensor details from the user's description.

**Pass Criteria:** References GPIO21, GPIO22, 4.7k, 3.3V, SHT30, 0x44 from the user's description. Any external info (SHT30 datasheet specs) labeled as external.
