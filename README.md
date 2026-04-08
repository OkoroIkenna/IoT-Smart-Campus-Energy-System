# IoT-Smart-Campus-Energy-System
Components used for the project:
1. ESP32
2. 4-WAY RELAY MODULE 
3. ACS712 CURRENT SENSOR
4. PIR SENSOR 
5. RESISTORS(220 OHMS,1K OHMS)
6. LED 
7. WALL SOCKET
8. BULB 
9. MANUAL OVERRIDE BUTTON

 BACKGROUND OF STUDY


# A. ESP32 Hardware Verification Test

# 1. Objective

The ESP32 hardware verification test was conducted to confirm that the ESP32 development board is functioning properly and capable of communicating with the computer for program upload and execution. This test ensures that the main controller of the system is operational before integrating other components.

# 2. Components Used
	•	ESP32 Development Board
	•	USB Cable
	•	Computer (Arduino IDE Installed)

# 3. Purpose
	1.	Confirm ESP32 is functioning properly
	2.	Confirm Arduino IDE communication with ESP32
	3.	Confirm program upload functionality
	4.	Confirm serial monitor output working
	5.	Confirm GPIO pins operational

4. Connection Setup

ESP32 connected to computer using USB cable.


# 5. Test Code Used

```cpp
void setup()
{
Serial.begin(115200);
}

void loop()
{
Serial.println("ESP32 Working...");
delay(1000);
}
```

6. Expected Result
	•	Code uploads successfully
	•	Serial monitor displays output
	•	ESP32 resets properly
	•	Communication between ESP32 and computer established

7. Problems Encountered
	1.	ESP32 not detected
	2.	Wrong COM port selected
	3.	Driver issues
	4.	Upload failure

8. Cause of Problem
	•	ESP32 board not installed in Arduino IDE
	•	Incorrect board selection
	•	Incorrect port selection
	•	Missing USB driver

9. Solution
	1.	Installed ESP32 board in Arduino IDE
	2.	Selected correct board (ESP32 Dev Module)
	3.	Selected correct COM port
	4.	Restarted Arduino IDE


10. Result
	•	ESP32 detected successfully
	•	Code uploaded successfully
	•	Serial monitor output confirmed
	•   ESP32 ready for system integration

# Conclusion

The ESP32 development board was successfully tested and verified. The controller is now ready to interface with sensors, relay modules, and other system components for the IoT Smart Campus Energy System.



# B. Relay Module Hardware Verification Test

1. Objective

The relay module test was conducted to confirm that the ESP32 can successfully control external electrical appliances using GPIO pins. This test ensures that switching mechanisms required for appliance automation are functioning correctly.

2. Components Used
	•   ESP32
	•   4-Channel Relay Module
	•   Jumper Wires
	•   LED (for simulation)
	•   Power Supply (5V from ESP32)

3. Purpose
	•   Confirm relay switching functionality
	•   Confirm GPIO control from ESP32
	•   Confirm relay power supply
	•   Confirm active LOW logic behavior
	•   Confirm relay LED indicators working properly

4. Connection Setup

	•   ESP32 → Relay Module
	•   ESP32 VIN → Relay VCC
	•   ESP32 GND → Relay GND
	•   GPIO 26 → IN1


# 5. Test Code Used

```cpp
#define RELAY1 26

void setup()
{
Serial.begin(115200);
pinMode(RELAY1, OUTPUT);
}

void loop()
{
Serial.println("Relay ON");
digitalWrite(RELAY1, LOW);
delay(3000);

Serial.println("Relay OFF");
digitalWrite(RELAY1, HIGH);
delay(3000);
}
```
6. Expected Result
	•   Relay should click ON and OFF
	•   Relay indicator LED should blink
	•   Serial monitor should display switching messages
	•   GPIO should control relay successfully

7. Problems Encountered
	1.  Relay clicking opposite logic
	2.  Relay not turning ON initially
	3.  Confusion with relay active state
	4.  No switching observed at first

8. Cause of Problem

The relay module used is Active LOW, meaning:

LOW signal activates relay
HIGH signal deactivates relay

This behavior is different from normal logic expectations.

9. Solution

Relay logic was reversed in code:

LOW = Relay ON
HIGH = Relay OFF

After correcting logic, relay switching worked properly.

9. Result
	•   Relay switching successful
	•   ESP32 GPIO control confirmed
	•   Relay power supply confirmed
	•   Relay ready for appliance control integration

10. Conclusion

The relay module was successfully tested and verified. The ESP32 can now control electrical loads such as:

Fans
Bulbs
Wall sockets
Other appliances

This confirms that the system can perform automated appliance control required for the IoT Smart Campus Energy System.




# C. PIR Sensor Hardware Verification Test

1. Objective

The PIR sensor test was conducted to confirm that the system can detect human presence or motion. This is important for implementing automatic appliance control to reduce energy wastage in university environments.

2. Components Used
	•	ESP32
	•	PIR Motion Sensor
	•	LED (Simulation Load)
	•	Resistor (220Ω / 1KΩ)
	•	Jumper Wires

3. Purpose
	1.	Confirm PIR motion detection
	2.	Confirm ESP32 receiving PIR signal
	3.	Confirm automatic control logic
	4.	Confirm motion-based automation
	5.	Simulate appliance control using LED

4. Connection Setup

ESP32 → PIR Sensor
	•	PIR VCC → ESP32 VIN
	•	PIR GND → ESP32 GND
	•	PIR OUT → GPIO 27

LED Connection
	•	LED Positive → GPIO 25
	•	LED Negative → GND (through resistor)

# 5. Test Code Used
```cpp
#define PIR 27
#define LED 25

void setup()
{
Serial.begin(115200);
pinMode(PIR, INPUT);
pinMode(LED, OUTPUT);
}

void loop()
{
int motion = digitalRead(PIR);

if(motion == HIGH)
{
Serial.println("Motion Detected");
digitalWrite(LED, HIGH);
}
else
{
Serial.println("No Motion");
digitalWrite(LED, LOW);
}

delay(500);
}
```

7. Expected Result
	•	PIR detects motion
	•	Serial monitor displays “Motion Detected”
	•	LED turns ON when motion detected
	•	LED turns OFF when no motion

8. Problems Encountered
	1.	PIR sensor not detecting motion initially
	2.	LED not turning ON
	3.	Unstable readings from PIR sensor
	4.	Delay in motion detection

9. Cause of Problem
	•	PIR sensor requires warm-up time
	•	Incorrect GPIO configuration
	•	Loose wiring connections
	•	PIR sensitivity delay

10. Solution
	1.	Allowed PIR sensor warm-up time (10–30 seconds)
	2.	Verified GPIO connections
	3.	Tightened wiring connections
	4.	Adjusted delay timing in code

11. Result
	•	Motion detection successful
	•	LED automation successful
	•	Serial monitor working properly
	•	PIR sensor ready for automation

12. Conclusion

The PIR sensor was successfully tested and verified. The system can now detect occupancy and automatically control appliances to reduce unnecessary power consumption. This feature is essential for implementing smart energy management in university campuses.




# D. Manual Override Button Hardware Verification Test

1. Objective

The manual override button test was conducted to allow users manually control appliances regardless of motion detection. This feature ensures flexibility in situations where automatic control is not desirable.

2. Components Used
	•	ESP32
	•	Push Button
	•	LED (Simulation Load)
	•	Resistor (10KΩ Pull-up / Pull-down if required)
	•	Jumper Wires

3. Purpose
	1.	Confirm manual control functionality
	2.	Confirm override of PIR automation
	3.	Confirm toggle switching behavior
	4.	Confirm GPIO input reading
	5.	Confirm user control capability

4. Connection Setup

ESP32 → Push Button
	•	One Button Leg → GPIO 14
	•	Other Button Leg → GND

Internal Pull-Up Used:

pinMode(BUTTON, INPUT_PULLUP);

LED Connection
	•	LED Positive → GPIO 25
	•	LED Negative → GND (through resistor)

# 5. Test Code Used
```cpp
#define BUTTON 14
#define LED 25

bool manual = false;
bool lastButton = HIGH;

void setup()
{
Serial.begin(115200);
pinMode(BUTTON, INPUT_PULLUP);
pinMode(LED, OUTPUT);
}

void loop()
{
bool button = digitalRead(BUTTON);

if(button == LOW && lastButton == HIGH)
{
manual = !manual;

if(manual)
{
Serial.println("Manual ON");
digitalWrite(LED, HIGH);
}
else
{
Serial.println("Manual OFF");
digitalWrite(LED, LOW);
}

delay(300);
}

lastButton = button;
}
```
6. Expected Result
	•	Button press toggles LED
	•	Serial monitor displays Manual ON/OFF
	•	LED turns ON when manual mode active
	•	LED turns OFF when manual mode disabled

7. Problems Encountered
	1.	Button not responding initially
	2.	Multiple toggles on single press
	3.	LED not switching correctly
	4.	Unstable button readings

8. Cause of Problem
	•	Button bouncing
	•	No debounce delay
	•	Incorrect wiring
	•	Incorrect GPIO configuration

9. Solution
	1.	Added debounce delay
	2.	Verified wiring connections
	3.	Used INPUT_PULLUP configuration
	4.	Implemented toggle logic

10. Result
	•	Manual override working successfully
	•	Button toggling confirmed
	•	LED switching confirmed
	•	User control implemented successfully

11. Conclusion

The manual override button was successfully tested and verified. The system now supports manual appliance control, allowing users to override automatic motion detection when necessary. This improves system flexibility and usability.



# E. PIR and Manual Override Integration Test

1. Objective

The PIR and manual override integration test was conducted to confirm that both automatic motion detection and manual control can function together without interfering with each other. This ensures that the system can automatically control appliances while still allowing users to manually override the system when necessary.

2. Components Used
	•	ESP32
	•	PIR Motion Sensor
	•	Push Button (Manual Override)
	•	LED (Simulation Load)
	•	Resistor (220Ω / 1KΩ / 10KΩ if needed)
	•	Jumper Wires


3. Purpose
	1.	Confirm PIR automatic control
	2.	Confirm manual override functionality
	3.	Confirm toggle switching behavior
	4.	Confirm PIR pause during manual mode
	5.	Confirm system integration logic

4. Connection Setup

PIR Sensor Connection
	•	PIR VCC → ESP32 VIN
	•	PIR GND → ESP32 GND
	•	PIR OUT → GPIO 27

Manual Override Button
	•	Button → GPIO 14
	•	Button → GND

LED Connection
	•	LED Positive → GPIO 25
	•	LED Negative → GND (through resistor)

5. Test Code Used

```cpp
#define PIR 27
#define LED 25
#define BUTTON 14

bool manual = false;
bool lastButton = HIGH;

void setup()
{
Serial.begin(115200);

pinMode(PIR, INPUT);
pinMode(LED, OUTPUT);
pinMode(BUTTON, INPUT_PULLUP);

digitalWrite(LED, LOW);
}

void loop()
{
bool button = digitalRead(BUTTON);

if(button == LOW && lastButton == HIGH)
{
manual = !manual;

if(manual)
{
Serial.println("Manual Mode ON");
digitalWrite(LED, HIGH);
}
else
{
Serial.println("Manual Mode OFF");
digitalWrite(LED, LOW);
}

delay(300);
}

lastButton = button;

if(!manual)
{
int motion = digitalRead(PIR);

if(motion == HIGH)
{
Serial.println("Motion Detected");
digitalWrite(LED, HIGH);
}
else
{
Serial.println("No Motion");
digitalWrite(LED, LOW);
}
}

delay(200);
}
```

6. Expected Result
	•	PIR detects motion and turns LED ON
	•	LED turns OFF when no motion detected
	•	Button toggles manual mode
	•	Manual mode pauses PIR sensor
	•	Manual mode allows user control

7. Problems Encountered
	1.	PIR interfering with manual override
	2.	Button toggling multiple times
	3.	LED switching incorrectly
	4.	Manual mode not pausing PIR

8. Cause of Problem
	•	Logic conflict between PIR and manual override
	•	Button bounce issues
	•	Incorrect toggle logic
	•	Timing conflicts

9. Solution
	1.	Implemented manual mode flag
	2.	Added debounce delay
	3.	Separated PIR logic and manual logic
	4.	Corrected toggle logic

10. Result
	•	PIR automation working correctly
	•	Manual override working correctly
	•	System logic stable
	•	Integration successful

11. Conclusion

The PIR and manual override integration was successfully implemented. The system can now automatically detect occupancy and control appliances while still allowing manual user control. This improves system intelligence and flexibility for smart campus energy optimization.



# F. ACS712 Current Sensor Hardware Verification Test

1. Objective

The ACS712 current sensor test was conducted to measure electrical current consumption of connected appliances. This enables the system to monitor power usage and detect abnormal or low current conditions for smart energy optimization.

2. Components Used
	•	ESP32
	•	ACS712 Current Sensor
	•	12V Fan (Test Load)
	•	12V Power Supply
	•	Jumper Wires
	•	Resistor (Optional for stabilization)

3. Purpose
	1.	Confirm current measurement capability
	2.	Confirm ESP32 analog reading
	3.	Confirm load current detection
	4.	Confirm real-time monitoring
	5.	Enable smart energy optimization feature

4. Connection Setup

ACS712 → ESP32
	•	VCC → ESP32 3.3V (or VIN depending on module)
	•	GND → ESP32 GND
	•	OUT → GPIO 35 (Analog Pin)

Load Connection (Fan Through ACS712)
	•	12V Positive → ACS712 Input Terminal
	•	ACS712 Output Terminal → Fan Positive
	•	Fan Negative → 12V Negative

This allows ACS712 to measure current flowing to the fan.

5. Test Code Used

```cpp
#define ACS712 35

float voltage = 0;
float current = 0;
float offset = 0;

void setup()
{
Serial.begin(115200);

analogReadResolution(12);

delay(3000);

// Calibration
for(int i=0;i<100;i++)
{
offset += analogRead(ACS712);
delay(10);
}

offset = offset / 100.0;

Serial.print("Offset Value: ");
Serial.println(offset);
}

void loop()
{
int value = analogRead(ACS712);

voltage = (value * 3.3) / 4095.0;

float offsetVoltage = (offset * 3.3) / 4095.0;

current = (voltage - offsetVoltage) / 0.185;

Serial.print("Current: ");
Serial.println(current);

delay(500);
}
```

6. Expected Result
	•	Serial monitor displays current readings
	•	Current changes when fan is ON
	•	Current near zero when fan is OFF
	•	Stable readings after calibration

7. Problems Encountered
	1.	Constant maximum value (4095)
	2.	No current change when load connected
	3.	Noisy or unstable readings
	4.	Incorrect calibration values

8. Cause of Problem
	•	No load connected initially
	•	Incorrect analog pin selection
	•	Incorrect power connection
	•	Sensor calibration not performed

9. Solution
	1.	Connected fan as load
	2.	Verified analog pin GPIO 35
	3.	Performed sensor calibration
	4.	Verified wiring connections

10. Result
	•	Current readings successfully detected
	•	Fan load current measured correctly
	•	Sensor calibration successful
	•	Real-time monitoring confirmed

11. Conclusion

The ACS712 current sensor was successfully tested and verified. The system can now monitor power consumption of connected appliances. This feature enables smart energy optimization, low current detection, and improved energy management within university campus environments.



# G. Relay and ACS712 Integration Test

1. Objective

The relay and ACS712 integration test was conducted to confirm that the system can both control electrical appliances and monitor their power consumption simultaneously. This allows the system to intelligently manage energy usage and detect abnormal power conditions.

2. Components Used
	•	ESP32
	•	4-Channel Relay Module
	•	ACS712 Current Sensor
	•	12V Fan (Test Load)
	•	12V Power Supply
	•	Jumper Wires

3. Purpose
	1.	Confirm relay controlled load switching
	2.	Confirm current monitoring during load operation
	3.	Confirm power usage detection
	4.	Confirm system integration
	5.	Enable smart energy optimization

4. Connection Setup

Relay Connection
	•	Relay VCC → ESP32 VIN
	•	Relay GND → ESP32 GND
	•	Relay IN1 → GPIO 26

ACS712 Connection
	•	ACS712 VCC → ESP32 3.3V
	•	ACS712 GND → ESP32 GND
	•	ACS712 OUT → GPIO 35

Load Connection
	•	12V Positive → Relay COM
	•	Relay NO → ACS712 Input
	•	ACS712 Output → Fan Positive
	•	Fan Negative → 12V Negative

This configuration allows:
	•	Relay controls fan ON/OFF
	•	ACS712 measures fan current

5. Test Code Used

```cpp
#define RELAY 26
#define ACS712 35

float offset = 0;

void setup()
{
Serial.begin(115200);

pinMode(RELAY, OUTPUT);
digitalWrite(RELAY, HIGH);

delay(3000);

for(int i=0;i<100;i++)
{
offset += analogRead(ACS712);
delay(10);
}

offset = offset / 100.0;
}

void loop()
{
digitalWrite(RELAY, LOW);
Serial.println("Fan ON");

delay(3000);

int value = analogRead(ACS712);

float voltage = (value * 3.3) / 4095.0;
float offsetVoltage = (offset * 3.3) / 4095.0;
float current = (voltage - offsetVoltage) / 0.185;

Serial.print("Current: ");
Serial.println(current);

digitalWrite(RELAY, HIGH);
Serial.println("Fan OFF");

delay(3000);
}
```

6. Expected Result
	•	Relay switches fan ON and OFF
	•	ACS712 detects current when fan ON
	•	Current reduces when fan OFF
	•	Serial monitor displays current values

7. Problems Encountered
	1.	No current detected initially
	2.	Relay switching but no fan operation
	3.	Incorrect wiring between relay and sensor
	4.	Unstable current readings

8. Cause of Problem
	•	Incorrect wiring order
	•	No load connected initially
	•	Sensor calibration required
	•	Loose wiring connections

9. Solution
	1.	Corrected wiring order
	2.	Connected fan properly
	3.	Calibrated ACS712 sensor
	4.	Verified connections

10. Result
	•	Relay switching successful
	•	Current detection successful
	•	Load control confirmed
	•	Integration successful

11. Conclusion

The relay and ACS712 integration test was successfully completed. The system can now control electrical appliances and monitor their energy consumption simultaneously. This forms the foundation for smart energy optimization and intelligent appliance control in university campuses.