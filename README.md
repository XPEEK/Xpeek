Hej hej hej

Se me Shine

#include <NewPing.h> //Includes the library NewPing which is needed for the sensors to work good. 
#define SONAR_NUM 3 //Number of sensors. 
#define MAX_DISTANCE 300 //Maximum distance to ping (cm). 
 //Defining variables, because of the "unsigned" they can only be positive. 
unsigned int frontDist;  
unsigned int leftDist; 
unsigned int rightDist; 
unsigned int Time1; 
unsigned int Time2; 
unsigned int Time3; 
NewPing sonar[SONAR_NUM] = { //Sensors object array. 
 NewPing(3, 2, MAX_DISTANCE), //Each sensor's trigger pin, echo pin, and max distance to ping.  NewPing(5, 4, MAX_DISTANCE), 
 NewPing(7, 6, MAX_DISTANCE), 
}; 
void setup() { 
 Serial.begin(115200); //Sets the data rate to max. 
 //Setup Channel A TURN 
 pinMode(12, OUTPUT); //Initiates Turn Channel A pin. 
 pinMode(9, OUTPUT); //Initiates Brake (steer straight) Channel A pin. 
 //Setup Channel B THROTTLE 
 pinMode(13, OUTPUT); //Initiates Throttle Channel B pin. 
 pinMode(8, OUTPUT); //Initiates Brake Channel B pin. 
} 
void turnLeft() { 
 //Motor A LEFT 
 digitalWrite(12, HIGH); //Establishes left direction of Channel A. 
 digitalWrite(9, LOW); //Disengage the Brake for Channel A. 
 analogWrite(3, 255); //Spins the motor on Channel A at full speed – maximum left turn. } 
void turnRight() {



14 
 //Motor A RIGHT 
 digitalWrite(12, LOW); //Establishes right direction of Channel A. 
 digitalWrite(9, LOW); //Disengage the Brake for Channel A. 
 analogWrite(3, 255); //Spins the motor on Channel A at full speed – maximum right turn. } 
void drive() { 
 //Motor B FORWARD 
 digitalWrite(13, HIGH); //Establishes backward direction of Channel B.  digitalWrite(8, LOW); //Disengage the Brake for Channel B. 
 analogWrite(11, 100); //Spins the motor on Channel B less than half full speed. } 
void fullSpeed() { 
 //Motor B FORWARD 
 digitalWrite(13, HIGH); //Establishes backward direction of Channel B  digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 200); //Spins the motor on Channel B at ~80% speed } 
void reverse() { 
 //Motor B BACKWARDS 
 digitalWrite(13, LOW); //Establishes forward direction of Channel B  digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 200); //Spins the motor on Channel B at ~80% speed } 
void brake() { 
 //Motor B BACKWARDS 
 digitalWrite(13, LOW); //Establishes forward direction of Channel B  digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 255); //Spins the motor on Channel B at full speed  delay(400); 
 slowDown(); 
} 
void slowDown() { 
 digitalWrite(8, HIGH); //Engage the Brake for Channel B 
} 
void steerStraight() { 
 digitalWrite(9, HIGH); //Engage the Brake for Channel A 
} 
void loop() { 
 scan(); //Goes to the scan function.
15 
 if (frontDist == 0 || frontDist >= 40) //The sensors ping 0 if the distance is greater than the MAX_DISTANCE.  { 
 if (rightDist <= 40 || leftDist <= 40) 
 { 
 if (rightDist == 0 || leftDist == 0) { //If the distance is far at the left or the right direction, go forward.   steerStraight(); 
 drive(); 
 Serial.println("Cruising."); 
 } 
 else { //If something appears at the side of the car, brake and then use the navigate function.  slowDown(); 
 navigate(); 
 } 
 } 
 else { //If the distance is further than 40cm at every direction, go forward.   steerStraight(); 
 drive(); 
 Serial.println("Cruising."); 
 } 
 } 
 else //Else (if there is something infront of the robot within 40cm) then slow down and  navigate. 
 { 
 brake(); 
 navigate(); 
#include <NewPing.h> //Includes the library NewPing which is needed for the sensors to work good. 
#define SONAR_NUM 3 //Number of sensors. 
#define MAX_DISTANCE 300 //Maximum distance to ping (cm). 
 //Defining variables, because of the "unsigned" they can only be positive. 
unsigned int frontDist;  
unsigned int leftDist; 
unsigned int rightDist; 
unsigned int Time1; 
unsigned int Time2; 
unsigned int Time3; 
NewPing sonar[SONAR_NUM] = { //Sensors object array. 
 NewPing(3, 2, MAX_DISTANCE), //Each sensor's trigger pin, echo pin, and max distance to ping.  NewPing(5, 4, MAX_DISTANCE), 
 NewPing(7, 6, MAX_DISTANCE), 
}; 
void setup() { 
 Serial.begin(115200); //Sets the data rate to max. 
 //Setup Channel A TURN 
 pinMode(12, OUTPUT); //Initiates Turn Channel A pin. 
 pinMode(9, OUTPUT); //Initiates Brake (steer straight) Channel A pin. 
 //Setup Channel B THROTTLE 
 pinMode(13, OUTPUT); //Initiates Throttle Channel B pin. 
 pinMode(8, OUTPUT); //Initiates Brake Channel B pin. 
} 
void turnLeft() { 
 //Motor A LEFT 
 digitalWrite(12, HIGH); //Establishes left direction of Channel A. 
 digitalWrite(9, LOW); //Disengage the Brake for Channel A. 
 analogWrite(3, 255); //Spins the motor on Channel A at full speed – maximum left turn. } 
void turnRight() {



14 
 //Motor A RIGHT 
 digitalWrite(12, LOW); //Establishes right direction of Channel A. 
 digitalWrite(9, LOW); //Disengage the Brake for Channel A. 
 analogWrite(3, 255); //Spins the motor on Channel A at full speed – maximum right turn. } 
void drive() { 
 //Motor B FORWARD 
 digitalWrite(13, HIGH); //Establishes backward direction of Channel B.  digitalWrite(8, LOW); //Disengage the Brake for Channel B. 
 analogWrite(11, 100); //Spins the motor on Channel B less than half full speed. } 
void fullSpeed() { 
 //Motor B FORWARD 
 digitalWrite(13, HIGH); //Establishes backward direction of Channel B  digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 200); //Spins the motor on Channel B at ~80% speed } 
void reverse() { 
 //Motor B BACKWARDS 
 digitalWrite(13, LOW); //Establishes forward direction of Channel B  digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 200); //Spins the motor on Channel B at ~80% speed } 
void brake() { 
 //Motor B BACKWARDS 
 digitalWrite(13, LOW); //Establishes forward direction of Channel B  digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 255); //Spins the motor on Channel B at full speed  delay(400); 
 slowDown(); 
} 
void slowDown() { 
 digitalWrite(8, HIGH); //Engage the Brake for Channel B 
} 
void steerStraight() { 
 digitalWrite(9, HIGH); //Engage the Brake for Channel A 
} 
void loop() { 
 scan(); //Goes to the scan function.
15 
 if (frontDist == 0 || frontDist >= 40) //The sensors ping 0 if the distance is greater than the MAX_DISTANCE.  { 
 if (rightDist <= 40 || leftDist <= 40) 
 { 
 if (rightDist == 0 || leftDist == 0) { //If the distance is far at the left or the right direction, go forward.   steerStraight(); 
 drive(); 
 Serial.println("Cruising."); 
 } 
 else { //If something appears at the side of the car, brake and then use the navigate function.  slowDown(); 
 navigate(); 
 } 
 } 
 else { //If the distance is further than 40cm at every direction, go forward.   steerStraight(); 
 drive(); 
 Serial.println("Cruising."); 
 } 
 } 
 else //Else (if there is something infront of the robot within 40cm) then slow down and  navigate. 
 { 
 brake(); 
 navigate(); 
 } 
} 
void scan() //This function scans the surroundings with the ultra sonic sensors and determines  the distances in three directions.  
{ //It also prints the three distances, to the left, to the right and to the front, in the Seriell  Monitor.  
 Time1 = sonar[0].ping(); 
 Time2 = sonar[1].ping(); 
Time3 = sonar[2].ping(); 
 leftDist = Time1 / US_ROUNDTRIP_CM; 
 frontDist = Time2 / US_ROUNDTRIP_CM; 
 rightDist = Time3 / US_ROUNDTRIP_CM; 
 delay(50); 
 Serial.println(""); 
 Serial.println("Scanning"); 
 Serial.println(""); 
 Serial.print(leftDist); 
 Serial.print(" ");
16 
 Serial.print(frontDist); 
 Serial.print(" "); 
 Serial.print(rightDist); 
 Serial.println(" "); 
 Serial.println(" "); 
} 
void navigate() //This function determines which way the car should go depending on the three  distances from the function scan and then prints 
{ //which way the car goes in the Seriell Monitor.  
 Serial.println("There's an obstacle!"); 
 scan(); 
 if (frontDist < 20) { 
 if (rightDist < leftDist) { 
 reverse(); 
 turnRight(); 
 Serial.println("Reversing and turning right."); 
 delay(1000); 
 fullSpeed(); 
 turnLeft(); 
 Serial.println("Full speed and turning left!"); 
 delay(1000); 
 } 
 else if (rightDist > leftDist) { 
 reverse(); 
 turnLeft(); 
 Serial.println("Reversing and turning left."); 
 delay(1000); 
 fullSpeed(); 
 turnRight(); 
 Serial.println("Full speed and turning right!"); 
 delay(1000); 
 } 
 } 
 else if (frontDist >= 20) { 
 if (rightDist < leftDist) { 
 fullSpeed(); 
 turnLeft(); 
 Serial.println("Full speed and turning left!"); 
 delay(500); 
 } 
 else if (rightDist > leftDist) {
17 
 fullSpeed(); 
 turnRight(); 
 Serial.println("Full speed and turning right!"); 
 delay(500); 
 } 
 } 
}



8.2 Sensortest 
– Orginalkoden1var gjord för 15 sensorer, vi modifierade denna till våra 3 sensorer. 
#include <NewPing.h> 
#define SONAR_NUM 3 // Number or sensors. 
#define MAX_DISTANCE 40 // Maximum distance (in cm) to ping. 
#define PING_INTERVAL 33 // Milliseconds between sensor pings (29ms is about the min to avoid cross-sensor echo). 
unsigned long pingTimer[SONAR_NUM]; // Holds the times when the next ping should happen for each sensor. unsigned int cm[SONAR_NUM]; // Where the ping distances are stored. 
uint8_t currentSensor = 0; // Keeps track of which sensor is active. 
NewPing sonar[SONAR_NUM] = { // Sensor object array. 
 NewPing(3, 2, MAX_DISTANCE), // Each sensor's trigger pin, echo pin, and max distance to ping.  NewPing(5, 4, MAX_DISTANCE), 
 NewPing(7, 6, MAX_DISTANCE), 
 // NewPing(9, 8, MAX_DISTANCE), // Each sensor's trigger pin, echo pin, and max distance to ping.  // NewPing(11, 10, MAX_DISTANCE), 
}; 
void setup() { 
 Serial.begin(115200); 
 pingTimer[0] = millis() + 75; // First ping starts at 75ms, gives time for the Arduino to chill before starting.  for (uint8_t i = 1; i < SONAR_NUM; i++) // Set the starting time for each sensor. 
 pingTimer[i] = pingTimer[i - 1] + PING_INTERVAL; 
} 
void loop() { 
 for (uint8_t i = 0; i < SONAR_NUM; i++) { // Loop through all the sensors. 
 if (millis() >= pingTimer[i]) { // Is it this sensor's time to ping? 
 pingTimer[i] += PING_INTERVAL * SONAR_NUM; // Set next time this sensor will be pinged.  if (i == 0 && currentSensor == SONAR_NUM - 1) oneSensorCycle(); // Sensor ping cycle complete, do something  with the results.



  
1http://playground.arduino.cc/Code/NewPing. arduino.cc. 
18 
 sonar[currentSensor].timer_stop(); // Make sure previous timer is canceled before starting a new ping  (insurance). 
 currentSensor = i; // Sensor being accessed. 
 cm[currentSensor] = 0; // Make distance zero in case there's no ping echo for this sensor.  sonar[currentSensor].ping_timer(echoCheck); // Do the ping (processing continues, interrupt will call echoCheck to  look for echo). 
 } 
 } 
} 
void echoCheck() { // If ping received, set the sensor distance to array.  if (sonar[currentSensor].check_timer()) 
 cm[currentSensor] = sonar[currentSensor].ping_result / US_ROUNDTRIP_CM; 
} 
void oneSensorCycle() { // Sensor ping cycle complete, do something with the results.  for (uint8_t i = 0; i < SONAR_NUM; i++) { 
 Serial.print(i); 
 Serial.print("="); 
 Serial.print(cm[i]); 
 Serial.print("cm "); 
 } 
 Serial.println(); 
}



8.3 Motortest
void setup() { 
 //Setup Channel A - turning 
 pinMode(12, OUTPUT); //Initiates Motor Channel A pin 
 pinMode(9, OUTPUT); //Initiates Brake Channel A pin 
 //Setup Channel B - forward/backward 
 pinMode(13, OUTPUT); //Initiates Motor Channel A pin 
 pinMode(8, OUTPUT); //Initiates Brake Channel A pin 
} 
void loop(){ 
 //Motor A forward @ full speed 
 digitalWrite(12, HIGH); //Establishes forward direction of Channel A 
 digitalWrite(9, LOW); //Disengage the Brake for Channel A 
 analogWrite(3, 255); //Spins the motor on Channel A at full speed 
 delay(2000); 
 //Motor B backward @ half speed 
 digitalWrite(13, LOW); //Establishes backward direction of Channel B 
 digitalWrite(8, LOW); //Disengage the Brake for Channel B



19 
 analogWrite(11, 123); //Spins the motor on Channel B at half speed 
 delay(3000); 
digitalWrite(9, HIGH); //Engage the Brake for Channel A 
 digitalWrite(9, HIGH); //Engage the Brake for Channel B 
 delay(1000); 
  
 //Motor A forward @ full speed 
 digitalWrite(12, LOW); //Establishes backward direction of Channel A 
 digitalWrite(9, LOW); //Disengage the Brake for Channel A 
 analogWrite(3, 123); //Spins the motor on Channel A at half speed 
 delay(2000); 
  
 //Motor B forward @ full speed 
 digitalWrite(13, HIGH); //Establishes forward direction of Channel B 
 digitalWrite(8, LOW); //Disengage the Brake for Channel B 
 analogWrite(11, 255); //Spins the motor on Channel B at full speed 
 delay(3000); 
digitalWrite(9, HIGH); //Engage the Brake for Channel A 
 digitalWrite(9, HIGH); //Engage the Brake for Channel B 
 delay(1000); 
}



20
