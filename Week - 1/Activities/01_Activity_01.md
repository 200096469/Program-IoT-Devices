# Activity 1 - IoT Programming Introduction (Week 1)



**Goal:** Practice declaring variables, choosing data types, writing comments, and using the `setup()` / `loop()` structure to build and upload a working device start-up + LED blink program.



## Before You Start

- [ ] Wokwi project open with the correct board selected
- [ ] LED wired in the diagram (with a resistor) to a GPIO pin — note which pin, some boards don't simulate `LED_BUILTIN`
- [ ] Serial Monitor baud rate will match `Serial.begin()` in your code

---

## Task 1 - Build the Base Program 

Recreate the base start-up + blink program yourself, without copy-pasting from the lesson notes.

**Open this Wokwi simulation:** https://wokwi.com/projects/470567521110438913

1. Declare two variables:
   - `ledPin` (type `int`) — use `pin 13` if your board simulates one, otherwise set it to whichever GPIO you wired the LED to in the diagram
   - `deviceName` (type `String`), set to any name you choose
2. In `setup()`:
   - Start Serial communication at `115200`
   - Set `ledPin` as an `OUTPUT`
   - Print a start-up message that includes `deviceName`
3. In `loop()`:
   - Turn the LED on, print `"LED: ON"`, wait 1000 ms
   - Turn the LED off, print `"LED: OFF"`, wait 1000 ms
4. Upload the code and confirm the LED blinks in time with the Serial Monitor output.

**Check yourself:**
- [ ] Program compiles with no errors
- [ ] Serial Monitor shows the start-up message once
- [ ] LED blinks in sync with `"LED: ON"` / `"LED: OFF"` messages

**Task 1**
```cpp
/*
=== Task 1 - Build the Base Program ===
        Author: Roberto Palozzo
=======================================
*/

#define ON HIGH
#define OFF LOW

int ledPin = 13;
String deviceName = "Activity_1";

void setup() 
{
  // put your setup code here, to run once:
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);  
}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(ledPin, ON);
  delay(1000);
  digitalWrite(ledPin, OFF);
  delay(1000);
}
```
https://wokwi.com/projects/471388867031124993

---

## Task 2 - Custom Device Start-Up Sequence

**Open this Wokwi simulation:** https://wokwi.com/projects/470564412054187009 

Modify your Task 1 program to include:

1. At least **three variables** — one `int`, one `float`, one `String`.
2. Print all three values in `setup()` as part of a formatted start-up message, for example:

   ```
   === Smart Sensor Node ===
   Device: TempSensor_01
   Pin: 13
   Threshold: 28.5
   Status: READY
   =========================
   ```

3. In `loop()`, blink the LED **three times quickly** (200 ms on / 200 ms off), then pause for **2 seconds**, then repeat.

**Task 2**
```cpp
/*
=== Task 2 - 3 Times Fast Blinking LED ===
        Author: Roberto Palozzo
==========================================
*/

int ledPin = 13;
float threshold = 0.02;
String deviceStatus = "READY";

void setup() {
  // put your setup code here, to run once:
  Serial.begin(115200);
  Serial.println("=== 3 Times Fast Blinking LED ===");
  Serial.println("Device: Blue_LED_1");
  Serial.print("Pin: ");
  Serial.println(ledPin);
  Serial.print("Threshold: ");
  Serial.println(threshold);
  Serial.print("Status: ");
  Serial.println(deviceStatus);
  Serial.println("=========================");
  pinMode(ledPin, OUTPUT);
}

void loop() {
  for(int i=0; i<3; i++) {
    digitalWrite(ledPin, HIGH);
    delay(200);
    digitalWrite(ledPin, LOW);
    delay(200);
  }
  delay(2000);
}
```
https://wokwi.com/projects/471592836535198721

---

## Task 3 - Blink Patterns (Extension)

**Open this Wokwi simulation:** https://wokwi.com/projects/470569149081367553

Write a program that creates a **"heartbeat" pattern**: two quick blinks followed by a long pause.

Requirements:
- Use clearly named variables for every delay value, e.g.:
  ```cpp
  int shortBlink = 100;
  int longPause = 1500;
  ```
- Do not hardcode delay numbers directly inside `loop()` — always reference your variables.

**Task 3**
```cpp
/*
===Task 3 - Heart Pulse ======
    Author: Roberto Palozzo
==============================
*/

int ledPin = 13;
int shortBlink = 100;
int longPause = 1500;
float threshold = 0.01;
String deviceStatus = "READY";

void setup() {
  Serial.begin(115200);
  Serial.println("=== Heart Pulse ===");
  Serial.println("Device: HeartPulse_01");
  Serial.print("Pin: ");
  Serial.println(ledPin);
  Serial.print("Threshold: ");
  Serial.println(threshold);
  Serial.print("Status: ");
  Serial.println(deviceStatus);
  Serial.println("=========================");
  pinMode(ledPin, OUTPUT);
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(shortBlink);
  digitalWrite(ledPin, LOW);
  delay(longPause);
}
```
https://wokwi.com/projects/471604323201745921

---

## Task 4 - Annotated Code (Extension)

Take your Task 1 or Task 2 program and add a comment above **every line** explaining what it does, in your own words.

- Focus on explaining **why** a line exists, not just restating what it says.
- Use the comment best practices from the lesson (explain why, comment formulas, label pins, don't over-comment obvious lines).

**Task 4**
```cpp
/*
==== Task 4 - Annotated Code (Extension) ====
          Author: Roberto Palozzo
=============================================
*/

int ledPin = 13;                           // Variable that set the pin no. 13 as output power for LEDs.
String deviceName = "Start-Up + Blink";    // Name given to the code

void setup() 
{
  Serial.begin(115200);                    // Initialize serial communication, so Serial.println can be used.
  pinMode(ledPin, OUTPUT);                 // Configure ledPin as an output, so it can supply power to the LED
  Serial.println(deviceName);              // Start-up message using the deviceName variable
}

void loop() {
  digitalWrite(ledPin, HIGH);              // Turn ON the LED
  Serial.println("LED: ON");               // Matches the LED turning on
  delay(1000);                             // Keep the LED ON for 1000 ms or 1 second
  digitalWrite(ledPin, LOW);               // Turn OFF the LED
  Serial.println("LED: OFF");              // Matches the LED turning off 
  delay(1000);                             // Keep the LED OFF for 1000 ms or 1 second
}
```
https://wokwi.com/projects/471468429836264449

---

## Task 5 - Find and Fix the Bugs (Extension)

Each bug set below is a broken sketch containing **three separate mistakes** covered in the lesson. For each set: copy it into the IDE, use the **commenting-out technique** to isolate and fix each bug one at a time (don't fix everything at once), and write a one-line comment above each fixed line explaining what was wrong.

### Bug Set A 
```cpp
const int LED_PIN = 13;

void Setup() {
  Serial.begin(115200);
  LED_PIN = 9;
  Serial.println("Ready");
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(500);
  digitalWrite(LED_PIN, LOW);
  delay(500);
}
```
**Check yourself:**
- [ ] Program compiles with no errors
- [ ] LED blinks as expected
- [ ] Each fix has a comment explaining the original mistake

**Bug Set A**
```cpp
/*
==== Task 5 - Find and Fix the Bugs Set A ====
          Author: Roberto Palozzo
==============================================
*/

const int LED_PIN = 13;                    // Variable that can't be changed set the pin no. 13 as output power for LEDs.
String deviceName = "Activities Task 5";   // Name given to the code

void setup()                               // FIX 1: It was "void Setup()
{
  Serial.begin(115200);                    // Initialize serial communication, so Serial.println can be used.
  pinMode(LED_PIN, OUTPUT);                // FIX 2: it was LED_PIN = 9; Set the pin as output to give power to the LED.
  Serial.println("Ready");                 // Print "Ready" on the terminal when the code is ready to start.
}

void loop() {
  digitalWrite(LED_PIN, HIGH);             // Turn ON the LED 
  delay(500);                              // Keep the LED ON for 500 ms or half second
  digitalWrite(LED_PIN, LOW);              // Turn OFF the LED 
  delay(500);                              // Keep the LED OFF for 500 ms or half second
}
```
https://wokwi.com/projects/471469955015348225

---

### Bug Set B 

```cpp
int 2ledPin = LED_BUILTIN;
float temperature = "23.5";
String device name = "Node1";

void setup() {
  Serial.begin(9600);
  pinMode(2ledPin, OUTPUT);
}

void loop() {
  digitalWrite(2ledPin, HIGH);
  delay(500);
  digitalWrite(2ledPin, LOW);
  delay(500);
}
```
**Check yourself:**
- [ ] Program compiles with no errors
- [ ] All variable names follow the naming rules
- [ ] Each fix has a comment explaining the original mistake

**Bug Set B**
```cpp
/*
==== Task 5 - Find and Fix the Bugs Set B ====
          Author: Roberto Palozzo
==============================================
*/

int ledPin = 4;                          // FIX 1: was "2ledPin" — an identifier can't start with a digit (pin set to 4 for the actual wiring).
float temperature = 23.5;                // FIX 2: was "23.5" in quotes — a float can't be assigned a string.
String deviceName = "Node1";             // FIX 3: was "device name" with a space — identifiers can't contain spaces.

void setup() 
{
  Serial.begin(9600);
  Serial.println("Ready");
  pinMode(ledPin, OUTPUT);               // pin set as output, now consistent with the corrected ledPin name
}

void loop() {
  digitalWrite(ledPin, HIGH);
  delay(500);
  digitalWrite(ledPin, LOW);
  delay(500);
}
```
https://wokwi.com/projects/471468786632111105

---

### Bug Set C

```cpp
int ledPin = LED_BUILTIN;

void setup() {
  pinMode(ledPin, OUTPUT);
  Serial.println("Starting...")
}

void loop() {
  digitalWrite(ledPin, HIGH);  // Turn LED off
  delay(1000);
  digitalWrite(ledPin, LOW);
  delay(1000);
}
```

**Check yourself:**
- [ ] Program compiles with no errors
- [ ] Serial Monitor shows "Starting..." on upload
- [ ] Every comment accurately describes the line below it

**Bug Set C**
```cpp
/*
==== Task 5 - Find and Fix the Bugs Set C ====
            Author: Roberto Palozzo
==============================================
*/

int ledPin = 4;

void setup() {
  Serial.begin(115200);                             // FIX 1: Serial.begin(...) was missing
  pinMode(ledPin, OUTPUT);
  Serial.println("Starting...");                    // FIX 2: was missing the closing semicolon
}

void loop() {
  digitalWrite(ledPin, HIGH);  // Turn LED On          FIX 3: comment said "Turn LED off"
  delay(1000);
  digitalWrite(ledPin, LOW);
  delay(1000);
}
```
https://wokwi.com/projects/471923319088985089

---

## Questions

Answer these in your own words before moving on:

1. What data type would you use to store a decimal temperature reading? Why?  
   Float. Temperature is normally read with decimals for greater precision. Int would truncate the decimal part.  

2. What is the difference between `Serial.print()` and `Serial.println()`?  
   Serial.print() prints the text and stays on the same line;  
   Serial.println() prints the text and then adds a new line, useful for separating subsequent readings in the serial monitor.  

3. What happens if you remove `Serial.begin(115200)` from `setup()`?  
   The code compiles without errors, but serial communication is not initialized. Serial.println() and Serial.print() print nothing readable, or nothing at all, because there is no active serial connection.  

4. What does `void` mean at the start of `setup()` and `loop()`?  
   void indicates that the function does not return any value. Essentially, "this function performs actions, but should not return any results."  

5. Why is it useful to use a variable (or constant) for a pin number instead of typing `13` directly in the code?  
   Using a variable/constant (e.g., LED_PIN) makes the code more readable and easier to modify: if you change the physical connection of the LED, you update the value in a single place instead of searching every 13 places throughout the code, reducing the risk of errors.  

6. What is the difference between a `variable` and a `constant`? Give one example of when you'd use each.  
   A variable can change value during execution (e.g., temperature, which varies with each sensor reading); a constant, on the other hand, has a fixed value that must not change (e.g., const int LED_PIN = 13;, because the LED pin is always the same throughout the program).

---
## Self-Check Before Submitting

- [ ] Program compiles and uploads without errors
- [ ] Serial Monitor shows the correct start-up message
- [ ] LED blinks in sync with Serial Monitor output
- [ ] Variables are declared with appropriate, descriptive data types and names
- [ ] Constants (if used) are in `UPPER_CASE`
- [ ] Comments explain *why*, not just *what*
- [ ] I can explain the purpose of `setup()` and `loop()` out loud
