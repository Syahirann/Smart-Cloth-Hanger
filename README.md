# Smart-Cloth-Hanger
#include <ESP8266Wifi.h>
#include <Blynk.h>
#include<BlynkSimpleEsp8266.h>

#define BLYNK_PRINT Serial
#define CW D7   //CW is defned as pin #7//
#define CCW D8 //CCW is defined as pin #8//
const char *ssid = "Syah's iPhone";
const char *pass = "ukmi3c40qzsp2";

WiFiClient client;

char auth[] = " a08ae2db7aa04e1f82e48d959fa00a22";

WidgetLCD lcd1(V1);

int rain= 0;

void setup () {
Serial.begin (9600);
pinMode(rain, INPUT);
 Blynk.begin(auth, ssid, pass);
 lcd1.clear ();
 lcd1.print(0, 0, "Distance in cm");
   Serial.printIn("Connecting to ");
   Serial.printIn(ssid);
   Wifi.begin(ssid, pass);
   while (WiFi.status()  != WL_CONNECTED) {
   delay(500);
   Serial.print (".");
   }
   {  pinMode(CW, OUTPUT); //Set CW as an output//
   pinMode(CCW, OUTPUT); //Set CCW as an output//
   }
   Serial.printIn("");
   Serial.printIn("WiFi connected");
   Serial.printIn("IP address: ");
   Serial.printIn(Wifi.localIP());
   }
   void loop() {
    lcd1.clear();
    lcd1.print(0, 0, "Value:");
    int rain1 = analogRead(rain);
    Serial.printIn(rain1);
    lcd1.print(11, 0, rain1);
     Blynk.run();
    //delay(1000);
    
   serial.print("\n");
   
   if(rain1>=900)
   {
   Serial.print("no rain");
   lcd1.print(0, 1, "Cond:");
   lcd1.print(7, 1, "no rain");
    digitalWrite(CW, LOW); //Motor stops//
    digitalWrite(CCW, HIGH); //Motor runs counter-clockwise//
    delay(5000);
    digitalWrite(CCW, LOW); //Motor runs counter-clockwise//
    
    }
    
    else
    {
    Serial.print("rain");
      lcd1.print(0, 1, "Cond:");
      lcd1.print(7, 1, "raining");
    digitalWrite(CW, LOW); //Motor stops//
    digitalWrite(CCW, HIGH); //Motor runs counter-clockwise//
    delay(5000);
    digitalWrite(CCW, LOW); //Motor runs counter-clockwise//    
}
delay(1000);

Serial.print("\n");
)
