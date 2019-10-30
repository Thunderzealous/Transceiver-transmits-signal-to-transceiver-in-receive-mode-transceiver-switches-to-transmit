// Transmitter mode transceiver
# include <SPI.h>
# include <nRF24L01.h>
# include <RF24.h>
RF24 radio(2); // CE
const byte addresses [] =  "00002";
int sensor_pin = 2;
int reed_pin = 3;

boolean sensor_state = 0;
boolean sensor_state1 = 0;
boolean reed_state = 0;
boolean reed_state1 = 0;
int actuator_pin = 1;

void setup() {
  pinMode(actuator_pin, OUTPUT);
  Serial.begin(9600);
  radio.begin();                            //Starting the radio communication
  radio.openReadingPipe(addresses[0]);   //Setting the address at which we will receive the data
  radio.setPALevel(RF24_PA_MIN);            //You can set it as minimum or maximum depending on the distance between the transmitter and receiver.
}

void loop() 
{
  delay(5);
  radio.startListening();                    //This sets the module as receiver
  if (radio.available())                     //Looking for incoming data
   {
    radio.read(&sensor_state, sizeof(sensor_state));
    radio.read(&reed_state, sizeof(reed_state));
    if(sensor_state == HIGH)
    if(reed_state == HIGH)
  {
     digitalWrite(actuator_pin, HIGH);
  }
  else
  {
     digitalWrite(actuator_pin, LOW);
  }
  delay(5000);
  }
}
  
