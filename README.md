// Transmitter mode transceiver
# include <SPI.h>
# include <nRF24L01.h>
# include <RF24.h>
RF24 radio(4, 10); // CE , CS
const byte address[6] = "00001";
int sensor_pin = D2;

boolean sensor_state = 0;
boolean sensor_state1 = 0;
int led_pin = D3;

void setup() void {
  pinMode(sensor_pin, INPUT);
  pinMode(led_pin, OUTPUT);
  radio.begin();
  radio.openWritingPipe(address[0]);
  radio.setPALevel(RF24_PA_MIN);
  radio.stopListening();
}

void loop()
{
  sensor_state = digitalRead(sensor_pin);
  if(sensor_state == HIGH)
  SentMessage[0] = 111;
 {
    digitalWrite(led_pin, HIGH);
    radio.write(SentMessage, 1);
 }
 else
 {
   digitalWrite(led_pin, LOW);
   }
 }
