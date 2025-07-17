# STM32F411VET6 – ADC to UART Logger

This project implements a simple measurement system for the **STM32F411VET6** microcontroller. It:

- reads data from two ADC channels (PA0 and PA1),
- sends the values periodically via **UART2** (TX on PA2),
- uses **DMA** for both ADC data acquisition and UART transmission,
- uses **TIM2** to control the sampling frequency.

## ⚙️ How it works

1. On startup, the program waits briefly to stabilize.
2. It initializes UART, ADC with DMA, and Timer2.
3. Timer2 triggers periodic ADC conversions via hardware triggering.
4. ADC results are transferred to a buffer using DMA.
5. When new data is available, it's sent over UART using DMA.

## 🔧 Configuration

- **System clock:** 16 MHz
- **Baud rate:** 750000 bps
- **Sampling rate:** Set by `TIM_PSC` and `TIM_ARR`:
  ```c
  #define TIM_PSC 16000
  #define TIM_ARR 100

