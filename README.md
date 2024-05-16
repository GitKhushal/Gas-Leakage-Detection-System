
# Gas-Leakage-Detection-System

## Objective
The LPG Gas Leakage Detection and Notification System is a project designed to detect the presence of Gas leaks in households or industrial environments. This system utilizes gas sensors to detect the presence of LPG gas and sends real-time notifications to the user's smartphone through the Blynk 2.0 platform, ensuring prompt action in case of gas leaks.

### Skills Learned

- IOT
- Blynk 2.0
- C
- Hardware and Circuit Design

### Tools Used

- Arduino IDE
- Blynk

### Components required
- ESP8266
- MQ5 Gas Sensor
- Connecting Wires 

### Code
```
#define BLYNK_PRINT Serial
#include &amp;lt;ESP8266WiFi.h&amp;gt;
#include &amp;lt;BlynkSimpleEsp8266.h&amp;gt;
 
// You should get Auth Token in the Blynk App.
char auth[] = &amp;quot;Auth_Token&amp;quot;;
 
// Your WiFi credentials.
// Set password to &amp;quot;&amp;quot; for open networks.
char ssid[] = &amp;quot;Your_SSID&amp;quot;;
char pass[] = &amp;quot;Your_Network_Password&amp;quot;;
 
int buzzer = D2; //buzzer
int sensor = A0; //sensor
int led_green = D5; //no leakage indication
int led_red = D6; // leakage indication
 
// Define threshold value. You might need to change it.
int sensor_limit = 600;
 
void setup()
{
pinMode(buzzer, OUTPUT);
pinMode(sensor, INPUT);
pinMode(led_green, OUTPUT);
pinMode(led_red, OUTPUT);
digitalWrite(led_green, LOW);
digitalWrite(led_red, LOW);
Serial.begin(9600);
Blynk.begin(auth, ssid, pass);
}
 
void loop()
{
int sensor_value = analogRead(sensor);
Serial.print(&amp;quot;Gas Level: &amp;quot;);
Serial.println(sensor_value);
Blynk.virtualWrite(V1, sensor_value);
// Checks if it has reached the threshold value
if (sensor_value &amp;gt; sensor_limit)
{
digitalWrite(led_green, HIGH);
digitalWrite(led_red, LOW);
digitalWrite(buzzer, HIGH);
delay(500);
digitalWrite(buzzer, LOW);
Blynk.notify(&amp;quot;Alert: Gas Leakage Detected&amp;quot;);
}
else
{
digitalWrite(buzzer, LOW);
digitalWrite(led_green, LOW);
digitalWrite(led_red, HIGH);
}
delay(100);
Blynk.run(); // Initiates Blynk
}
```
![Screenshot 2024-05-17 000144](https://github.com/GitKhushal/Gas-Leakage-Detection-System/assets/168212318/746837bc-58fe-46b1-b440-7fc05efaa552)
