# Eval Prompts: review-debug-deep-mode

---

## Prompt 1 — POSITIVE

**Prompt:**
> "Review this ISR handler for correctness:
> ```c
> void IRAM_ATTR gpio_isr_handler(void* arg) {
>     int sensor_value = read_adc();  // Takes ~100μs
>     char msg[64];
>     sprintf(msg, "Sensor: %d", sensor_value);
>     uart_write(msg, strlen(msg));
>     vTaskDelay(pdMS_TO_TICKS(10));
> }
> ```"

**Expected Behavior:** Multi-pass analysis. Finds: (S1) `vTaskDelay` in ISR — will crash. (S2) `read_adc` is too slow for ISR. (S2) `sprintf` and `uart_write` are not ISR-safe. (S3) `char msg[64]` stack allocation in ISR. Root cause: treating ISR as a normal function.

**Pass Criteria:** At least 3 findings with severity levels. Identifies the fundamental design error (heavy processing in ISR). Proposes fix: set flag in ISR, process in task.

---

## Prompt 2 — POSITIVE

**Prompt:**
> "My UART drops packets every ~30 seconds. Here's the receive code:
> ```c
> void uart_task(void* arg) {
>     uint8_t buf[256];
>     while(1) {
>         int len = uart_read_bytes(UART_NUM, buf, sizeof(buf), portMAX_DELAY);
>         process_packet(buf, len);  // Takes 50ms
>     }
> }
> ```"

**Expected Behavior:** Identifies: (S2) `portMAX_DELAY` blocks indefinitely — no timeout. (S3) 50ms `process_packet` blocks receive — data loss during processing. (S4) No packet framing — partial reads possible. Suggests ring buffer or double-buffering.

**Pass Criteria:** Identifies the timing relationship between receive blocking and processing time as root cause. Severity classifications present.

---

## Prompt 3 — POSITIVE

**Prompt:**
> "Optimize this sensor sampling loop — it's running at 50Hz but I need 200Hz:
> ```c
> void sample_loop() {
>     while(1) {
>         float temp = read_i2c_sensor(TEMP_ADDR);
>         float hum = read_i2c_sensor(HUM_ADDR);
>         float pres = read_i2c_sensor(PRES_ADDR);
>         log_to_sd(temp, hum, pres);
>         vTaskDelay(pdMS_TO_TICKS(5));
>     }
> }
> ```"

**Expected Behavior:** Analysis identifies bottlenecks: 3 sequential I2C reads, SD card write in the sampling loop. Measures needed: actual I2C read time per sensor, SD write time. Proposes: async SD writes, DMA I2C, or reduce sampling sensors.

**Pass Criteria:** Asks for or estimates timing of each operation. Identifies the critical path. Does not optimize blindly.

---

## Prompt 4 — NEGATIVE

**Prompt:**
> "Write a new UART driver from scratch for STM32."

**Expected Behavior:** This is a creation task, not a review. Use `architecture-first-solutioning` or `embedded-automation-design`.

**Pass Criteria:** No review report produced. Proceeds to design/implementation.

---

## Prompt 5 — NEGATIVE

**Prompt:**
> "Explain how DMA works on ESP32."

**Expected Behavior:** General explanation request. Use `structured-technical-response`.

**Pass Criteria:** No finding/severity format. Structured explanation instead.

---

## Prompt 6 — POSITIVE (Boundary)

**Prompt:**
> "This code works fine but I'm worried about edge cases. Can you check?
> ```c
> int divide(int a, int b) { return a / b; }
> ```"

**Expected Behavior:** Agent activates review mode. Finds: (S1) Division by zero when b=0. (S4) Integer overflow possible with INT_MIN / -1. Even though the code "works fine," latent bugs exist.

**Pass Criteria:** Identifies division by zero as a real finding with severity. Does not dismiss the review because it "works fine."
