# Analog PID Motor Speed Controller

## 📌 Project Overview
This project presents the design and implementation of an analog PID-based motor speed controller capable of maintaining a constant DC motor speed under varying load conditions. The entire control loop is built using operational amplifiers and discrete analog components, offering a fully analog approach to closed-loop speed regulation. 

## ✨ Key Features
* **Full Analog Control:** Realizes Proportional (P), Integral (I), and Derivative (D) control actions entirely using operational amplifier circuits.
* **Frequency-to-Voltage (F-V) Feedback:** Utilizes an encoder-based F-V converter to translate the motor's speed into a clean, proportional DC voltage.
* **PWM Actuation:** Generates a stable triangular carrier wave and compares it against the PID output to produce a duty-cycle-modulated PWM signal for efficient motor driving.
* **Robust Driver Stage:** Employs a power transistor to safely interface the low-power analog control circuit with the higher-current DC motor.

## 🏗️ System Architecture
The system consists of three main functional stages:

1. **Feedback Generation (F-V Converter):** The motor's built-in magnetic encoder produces a pulse train proportional to its speed. This signal is AC-coupled, shaped by a diode and transistor, and low-pass filtered to create a stable DC feedback voltage.
2. **PID Controller:** A differential amplifier detects the error between the user-defined reference voltage and the feedback voltage. This error signal is processed through parallel adjustable Proportional, Integral, and Derivative paths, which are then combined using an inverting summing amplifier.
3. **PWM Generation & Motor Driver:** A relaxation oscillator and integrator form a triangular wave generator. A comparator checks this wave against the PID output to create a PWM signal. This signal drives the base of a TIP41C NPN power transistor, switching the motor current on and off to maintain speed while minimizing power dissipation.

## 🛠️ Hardware Components
* **Op-Amps:** TL071 (used for fast switching in the PWM stage) and LM741 (used for general-purpose PID and feedback stages).
* **Transistors:** 2N3906 (for F-V converter signal conditioning) and TIP41C (power switching).
* **Diodes:** 1N914 (for pulse shaping and clamping).
* **Actuator:** N20 DC Motor with a built-in magnetic encoder.
* **Power Supply:** Requires a regulated +/-12V dual supply for the control logic and a dedicated 6V supply rail for the motor to prevent switching noise interference.

## 📊 Testing & Performance
* The analog sub-circuits were evaluated using Multisim to verify transient response, gain accuracy, and PWM switching behavior.
* Hardware testing on a breadboard confirmed stable operation, effective disturbance rejection, and a minimal steady-state error (between 0% and 0.1%). 
* The system effectively minimizes overshoot (typical 0.2%) and quickly corrects speed drops when external loads are applied.

## 🚀 Future Scope
Potential future improvements for this project include:
* Incorporating Kalman filtering techniques to improve noise rejection and state estimation accuracy.
* Upgrading the driver stage to support bidirectional motor control, enabling the motor to rotate in both clockwise and counterclockwise directions.
