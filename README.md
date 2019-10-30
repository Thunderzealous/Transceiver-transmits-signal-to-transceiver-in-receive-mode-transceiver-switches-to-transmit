// Transmitter mode transceiver
# include <SPI.h>
# include <nRF24L01.h>
# include <RF24.h>
RF24 radio(2, 10); // CE , CS
const byte addresses [][6] = {"00001", "00002"};
int sensor_pin = 2;

int reed_pin = 3;
boolean sensor_state = 0;
boolean sensor_state1 = 0:
boolean reed_state = 0;
boolean reed_state1 =0;

void setup()  {
  pinMode(reed_pin, input);
  Serial.begin(9600);
  radio.begin();
  radio.OpenReadingPipe(1, addresses[1]);
  radio.OpenWritingPipe(addresses[0]);
  radio.setPALevel(RF24_PA_MIN);
}
void loop()
{
  delay(5)
  radio.startListening();
  if (radio.available());
  {
    radio.read(&sensor_state, sizeof(sensor_state));
    radio.read(&reed_state, sizeof(reed_state));
    if(sensor_state == HIGH)
    if(reed_state == HIGH)
  {
     radio.stopListening();
     radio.write(&sensor_state, sizeof(sensor_state));
     radio.write(&reed_state, sizeof(reed_state));
