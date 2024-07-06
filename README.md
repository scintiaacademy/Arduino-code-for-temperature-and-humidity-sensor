# Arduino-code-for-temperature-and-humidity-sensor
"Arduino code to read and display humidity and temperature data using DHT11/DHT22 sensors."
#include <DHT.h>

#define DHTPIN A0     // Pin where the DHT11 is connected
#define DHTTYPE DHT11   // DHT 11 sensor type

DHT dht(DHTPIN, DHTTYPE);

void setup() {
  Serial.begin(9600);
  dht.begin();
}

void loop() {
  delay(2000);  // Wait for 2 seconds between measurements
  
  float humidity = dht.readHumidity();     // Read humidity value from sensor
  float temperatureC = dht.readTemperature();  // Read temperature in Celsius from sensor
  float temperatureF = dht.readTemperature(true);  // Read temperature in Fahrenheit from sensor
  
  // Check if any reads failed and exit early (to try again).
  if (isnan(humidity) || isnan(temperatureC) || isnan(temperatureF)) {
    Serial.println("Failed to read from DHT sensor!");
    return;
  }

  // Print humidity and temperature values to serial monitor
  Serial.print("Humidity: ");
  Serial.print(humidity);
  Serial.print("%\t");
  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.print("°C\t");
  Serial.print(temperatureF);
  Serial.println("°F");
}
