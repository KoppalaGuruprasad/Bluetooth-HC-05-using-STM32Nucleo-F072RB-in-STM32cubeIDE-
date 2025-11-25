# Bluetooth-HC-05-using-STM32Nucleo-F072RB-in-STM32cubeIDE-
This repository contains a complete STM32CubeIDE project for the STM32 Nucleo-F072RB board that interfaces with a Bluetooth module (HC-05 / HC-06) using USART1 (PA9–TX, PA10–RX).
The project demonstrates UART communication with interrupt handling and LED control via Bluetooth using simple character commands.

🚀 Project Features

✔ Fully configured STM32CubeIDE project

✔ USART1 @ 9600 baud for Bluetooth communication

✔ Interrupt-based UART receive (HAL_UART_Receive_IT)

✔ Control on-board LED (PA5) using Bluetooth commands

✔ Extremely beginner-friendly structure

✔ Ready to flash on Nucleo-F072RB

🧩 Hardware Used
Component	Details
Microcontroller	STM32 Nucleo-F072RB
Bluetooth Module	HC-05 / HC-06 (UART based)
USB Cable	For flashing the board
Jumper wires	For RX/TX/GND connections
🔌 Wiring Connections
Bluetooth Module	STM32F072RB Pin
TXD	PA10 (USART1_RX)
RXD	PA9 (USART1_TX)
GND	GND
VCC	5V or 3.3V

HC-05 RX is 3.3V tolerant, safe for PA9.

📂 Project Structure
Bluetooth/
 ├── Core/
 │   ├── Inc/
 │   ├── Src/
 │       ├── main.c        <-- UART + Bluetooth logic
 │       ├── stm32f0xx_it.c
 │       └── system_stm32f0xx.c
 ├── Drivers/
 ├── Bluetooth.ioc         <-- CubeMX configuration
 ├── .project
 ├── .cproject
 └── .mxproject

🛠 How the Code Works
1. UART Initialization

USART1 is initialized at 9600 baud, 8-N-1, bidirectional mode.

2. Interrupt-Based Receiving

The MCU constantly listens for 1 byte over UART:

HAL_UART_Receive_IT(&huart1, &rxData, 1);

3. Bluetooth Command Handling

Inside the UART RX callback:

if (rxData == 'O')      // Turn LED ON
    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_SET);

else if (rxData == 'X') // Turn LED OFF
    HAL_GPIO_WritePin(GPIOA, GPIO_PIN_5, GPIO_PIN_RESET);

4. Loop-Free Operation

The system runs fully on interrupts and requires no polling.

📱 How to Test Using Android Bluetooth App

Pair mobile with HC-05 / 06
Default password: 1234 or 0000

Install any Bluetooth terminal app:

Serial Bluetooth Terminal

BlueTerm

Connect → Type:

O → LED ON

X → LED OFF

▶️ Build & Flash Instructions

Open STM32CubeIDE

Select File → Import → Existing Projects into Workspace

Choose the project folder Bluetooth/

Build the project (Ctrl + B)

Connect Nucleo via USB

Click Run → Debug or Run

The firmware will be flashed and start running immediately.

📘 Bluetooth Commands
Character	Action
O	LED ON
X	LED OFF
📄 Dependencies

STM32CubeIDE (v1.14+ recommended)

HAL Library for STM32F0 series

ARM GCC toolchain (Bundled with CubeIDE)

📝 License

This project uses STM32 HAL under ST’s license terms.
Your custom application code can be used freely.
