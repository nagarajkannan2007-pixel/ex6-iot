# ex6-iot
#include <WiFi.h>
#include "ThingSpeak.h"

const char* ssid = "YourWiFi";
const char* password = "YourPassword";
WiFiClient client;

unsigned long channelID = 3024778;
const char* writeAPIKey = "C3L7LVEWTZZH3455";

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) delay(500);
  ThingSpeak.begin(client);
}

void loop() {
  float temp = analogRead(36) * (3.3 / 4095.0) * 100.0;
  ThingSpeak.writeField(channelID, 1, temp, writeAPIKey);
  delay(15000);
}
