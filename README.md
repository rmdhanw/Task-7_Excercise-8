# STM32 LED Control with FreeRTOS

This project demonstrates how to control multiple LEDs using FreeRTOS on an STM32 microcontroller. It features multitasking, synchronization using semaphores, and GPIO control to toggle LEDs at different intervals while ensuring safe access to shared resources.

## Features

- **Multitasking**: Three independent tasks control different LEDs (Green, Red, and Orange).
- **Synchronization**: Semaphores are used to protect shared resources, ensuring mutual exclusion and safe access.
- **GPIO Control**: The system toggles LEDs connected to GPIO pins.
- **FreeRTOS**: Utilizes FreeRTOS for task management and inter-task synchronization.

## System Overview

The program runs on an STM32 microcontroller and uses FreeRTOS to manage three tasks that flash the Green, Red, and Orange LEDs. Each LED is toggled at different time intervals. 

- **Green LED**: Flashes every 200 ms.
- **Red LED**: Flashes every 550 ms.
- **Orange LED**: Flashes every 50 ms.

The Green and Red LED tasks access a shared resource, protected by a semaphore, to ensure that only one task can access it at a time. The Orange LED task runs independently.

## Hardware Requirements

- **STM32 Microcontroller** (tested on [specify your board, e.g., STM32F4 Discovery, Nucleo, etc.])
- **LEDs**: Green, Red, and Orange (connected to GPIO pins)

## Software Requirements

- **STM32CubeMX**: For initializing peripherals and generating initialization code.
- **STM32CubeIDE**: For writing and debugging the application.
- **FreeRTOS**: FreeRTOS is used for task management and synchronization.

## Setup

### 1. **Hardware Setup**

Connect the LEDs to the appropriate GPIO pins of the STM32 microcontroller. The default pins used are:

- Green LED: `GPIO_PIN_0`
- Red LED: `GPIO_PIN_2`
- Orange LED: `GPIO_PIN_3`

### 2. **Software Setup**

1. Open STM32CubeIDE.
2. Import this project into STM32CubeIDE.
3. Ensure that the FreeRTOS middleware is included and configured.
4. Build and flash the program to your STM32 board.

### 3. **Pin Configuration**

Make sure the following GPIO pins are configured as output:

- Green LED: `GPIO_PIN_0`
- Red LED: `GPIO_PIN_2`
- Orange LED: `GPIO_PIN_3`
- Blue LED (optional for debugging): `GPIO_PIN_1`

## Code Structure

### 1. **Main File (`main.c`)**

- **System Initialization**: The system clock and peripherals are configured here.
- **GPIO Initialization**: The GPIO pins for the LEDs are initialized.
- **FreeRTOS Task Creation**: Three tasks are created to control the Green, Red, and Orange LEDs.
- **Semaphore**: A semaphore is used to manage access to the shared `startFlag` resource between the Green and Red LED tasks.

### 2. **Tasks**

- **Green LED Task (`GreenLedTask`)**: Toggles the Green LED every 200 ms. It waits for access to the semaphore before modifying shared data.
- **Red LED Task (`RedLedTask`)**: Toggles the Red LED every 550 ms. It also uses the semaphore to manage shared resource access.
- **Orange LED Task (`OrangeLedTask`)**: Toggles the Orange LED every 50 ms. It operates independently and doesn't use the semaphore.

### 3. **Semaphore Management**

The semaphore is used to ensure that the Green and Red LED tasks don’t interfere with each other when accessing the shared `startFlag`. This prevents potential data corruption or unexpected behavior.

## How It Works

1. **Task Creation**: Three FreeRTOS tasks are created to manage the LEDs.
2. **Semaphores**: The Green and Red LED tasks use a semaphore to ensure safe access to shared resources.
3. **LED Control**: Each task toggles its LED at different intervals, with the Green and Red tasks accessing shared resources protected by the semaphore.
4. **Scheduler**: The FreeRTOS scheduler ensures that the tasks are run according to their priorities.

https://github.com/user-attachments/assets/78243ec6-7d79-4fba-9174-60adc3044a94

