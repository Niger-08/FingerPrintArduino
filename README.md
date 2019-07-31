
#include <Adafruit_Fingerprint.h>
#include <SoftwareSerial.h>

SoftwareSerial mySerial(2, 3);

Adafruit_Fingerprint finger = Adafruit_Fingerprint(&mySerial);

uint8_t id;

void setup()  
{
  Serial.begin(9600);
  while (!Serial);  
  delay(500);
  Serial.println("\nenrollment");


  finger.begin(57600);
  
  if (finger.verifyPassword()) {
  
    Serial.println("Found teh sensor!");
  } 
  else {
  
    Serial.println("Did not find it");
    
    while (1) {
    delay(1); 
    }
  }
}
