
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

void loop()                     
{
  Serial.println("Ready to enroll a fingerprint!");
  Serial.println("Please type in the ID # (from 1 to 127)");
  id = readnumber();
Serial.print(“ID ");
  Serial.println(id);
  
  while (!  getFingerprintEnroll() 
);

}

uint8_t getFingerprintEnroll() {

  int p = 1;
  Serial.print("Waiting for valid finger print"); 
Serial.println(id);
  while (p != FINGERPRINT_OK) {
    p = finger.getImage();
    switch (p) {
    case FINGERPRINT_OK:
      Serial.println("Image inserted");
      break;
    case FINGERPRINT_NOFINGER:
      Serial.println(" ");
      break;
    case FINGERPRINT_PACKETRECIEVEERR:
      Serial.println("Communication error");
      break;
    case FINGERPRINT_IMAGEFAIL:
      Serial.println("imaging error");
      break;
    default:
      Serial.println("unknown error");
      break;
    }
  }
