# IS2101-Interrupts--NNM24IS192-
# Interrupt Controller Simulation (C++)

## 🧠 Overview
This project simulates a simple **Interrupt Controller** using **C++ multithreading**.  
It demonstrates how hardware interrupts (such as from a keyboard, mouse, or printer) are handled using **threads**, **priorities**, and **interrupt masking** — similar to how a real CPU interrupt controller works.

Each simulated device runs on its own thread and randomly raises interrupts.  
The controller receives these interrupts, filters them based on their **mask status**, and processes them in order of **priority**.

---

## ⚙️ Features
- Simulates multiple hardware devices:
  - **Keyboard**
  - **Mouse**
  - **Printer**
- Devices can be **masked** (disabled) or **enabled**.
- Interrupts are handled based on **priority**:
  1. Keyboard (highest)
  2. Mouse
  3. Printer (lowest)
- Thread-safe using:
  - `std::mutex`
  - `std::condition_variable`
  - `std::lock_guard`
- Real-time interrupt logs with timestamps.
- Random interrupt generation for realism.

---

## 🧩 Classes Overview

| Class | Description |
|--------|-------------|
| `Device` | Enum representing device types and priorities. |
| `InterruptEvent` | Structure representing an interrupt request from a device. |
| `InterruptController` | Core class managing masking, queuing, and interrupt handling. |
| `DeviceThread` | Class that simulates device behavior (random interrupt generation). |
| `InterruptControllerMain` | Entry point that sets up and runs the simulation. |

---

## ▶️ How It Works
1. Each device runs on a separate thread.
2. Devices periodically (and randomly) raise interrupts.
3. The interrupt controller:
   - Checks if the device is masked.
   - Adds unmasked interrupts to a **priority queue**.
4. The controller thread continuously processes pending interrupts in **priority order**.
5. Each handled interrupt is logged with a **timestamp**.

---

## 🧪 Example Output

```bash
Keyboard enabled
Mouse enabled
Printer masked
Keyboard → ISR done
Mouse → ISR done
Keyboard → ISR done
Mouse → ISR done
Printer (masked) → Ignored
...

=== ISR Log ===
12:34:56 - Keyboard
12:34:57 - Mouse
12:34:59 - Keyboard

Simulation complete.
# How to Run
#1️⃣ Compile

Ensure you have a C++17 (or newer) compiler installed (like g++).
In your terminal, navigate to the project directory and compile using:

g++ -std=c++17 -o InterruptControllerMain InterruptControllerMain.cpp -lpthread
2️⃣ Run

After compilation, run the simulation with:

./InterruptControllerMain

⏱️ Simulation Duration

The simulation runs for 8 seconds by default.
You can modify this in your main() function:

std::this_thread::sleep_for(std::chrono::seconds(8));
⚙️ Configuration

You can control which devices are masked (disabled) or enabled initially.
Inside main() or your controller setup, edit:

ic.maskDevice(Device::KEYBOARD, false);  // true = masked, false = enabled
ic.maskDevice(Device::MOUSE, false);
ic.maskDevice(Device::PRINTER, true);


Masked devices will not raise interrupts — they will be ignored and printed as (masked).
## 👨‍💻 Author

*Saanvi J Shetty*
Project: Interrupt Controller Simulation using Java Threads
