# First flash (Arduino)

1. Install **Arduino IDE** and **ESP32** board support.
2. Select the correct port.
3. Paste this minimal sketch and upload:

```cpp
#include <Arduino.h>
void setup() {
  // TODO: init OLED + LEDs according to the Cyber Fidget HAL
  pinMode(LED_BUILTIN, OUTPUT);
}
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(200);
  digitalWrite(LED_BUILTIN, LOW);
  delay(200);
}