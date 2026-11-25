# EdgeDAQ downloads

Two-channel ESP32-S3 data recorder for Windows.

## Download

- **[Download the Windows app](https://github.com/TuzaaBap/EdgeDAQ-downloads/releases/latest/download/EdgeDAQ.exe)**
- **[Download firmware binaries](https://github.com/TuzaaBap/EdgeDAQ-downloads/releases/latest/download/EdgeDAQ-firmware.zip)**
- [All release files and checksums](https://github.com/TuzaaBap/EdgeDAQ-downloads/releases/latest)

The Windows app is standalone and includes the firmware flasher. Python and Arduino are not required to use it.

## Set up

1. Connect the ESP32-S3 N16R8 logger with a USB data cable.
2. Open EdgeDAQ. To install or update firmware, choose **Firmware → Flash Firmware**, select the logger port, and click **Flash Firmware**. Keep USB connected until completion. If needed, hold BOOT, tap RESET, release BOOT, then retry.
3. Click **Connect**. The PC sends its current date, time, and timezone to the ESP32.
4. Choose each channel's sampling rate, apply it, and press **Start Recording**. Channel buttons show or hide graphs and voltage readings.
5. **Save to SD** preserves up to the latest three minutes. Open **Saved Recordings**, select a recording, and use **Download CSV…** to save it on the PC.

Firmware boots idle. Changing rates clears the current memory window. SD files remain saved when firmware is updated.

## Hardware

ESP32-S3, 16 MB flash, 8 MB OPI PSRAM. Channel 1 uses IO5 and Channel 2 uses IO4. Both require suitable input voltage dividers and common ground; do not apply 5 V directly to a GPIO. SD SPI: SCK12, MISO13, MOSI11, CS10. The logger uses ADC DMA, a PSRAM circular history buffer, and SD SPI DMA.

## CSV

```csv
timestamp,unix_time_us,time_us,channel,sample_index,raw,voltage_V
2026-11-26T00:33:54.802164+05:30,1795633434802164,0,1,0,0,0.00000
```

The timestamp includes the PC's timezone. Each recording keeps its own fixed time reference. Sample timing uses the nominal ADC clock; absolute accuracy depends on the PC clock, connection latency, and ADC clock drift. Displayed voltage decimals are not an accuracy guarantee.

## Source and third-party components

This repository holds release downloads and user instructions. The EdgeDAQ application and firmware source repository is private. The separate Espressif flash utility is open source; its corresponding upstream source, build instructions, and third-party notices are included with releases.
