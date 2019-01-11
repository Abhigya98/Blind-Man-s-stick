# Blind-Man-s-stick
An arduino based project that can be used by visually impaired individuals as a means of safe travel. It notifies the user on detecting an obstacle (buzzes). Obstacles and safe distance are determined using ultrasonic sensor.
The code is written on Arduino IDE:

const int trigPin = 10;//initializing sensor pins
const int echoPin = 9;
const int buzzer=13;


void setup() { 
Serial.begin(9600);
pinMode(trigPin, OUTPUT); 
pinMode (echoPin, INPUT); 
pinMode (LED_BUILTIN,OUTPUT);
pinMode(buzzer,OUTPUT);}

void loop()
{
long duration, distance; 
digitalWrite(trigPin, LOW); 
delayMicroseconds(2); 
digitalWrite(trigPin, HIGH); 
delayMicroseconds(10); 
digitalWrite(trigPin, LOW);

duration = pulseIn(echoPin, HIGH);
distance=(duration/2)/29.1;
if(distance>=2000)
{
  Serial.println("out of range");
  digitalWrite(LED_BUILTIN,LOW);
  noTone(buzzer);
  
 
}
else
{
  Serial.print(distance);
  Serial.println("cm");
  digitalWrite(LED_BUILTIN,HIGH);
  tone(buzzer, 1000);
  
}

delay(500);
}
