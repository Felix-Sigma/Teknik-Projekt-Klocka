This project is a temperature and time-based control system utilizing a DS3231 real-time clock (RTC) and temperature sensor module, an SSD1306 OLED display, a servo motor, and a relay-driven motor with LED indicators. It reads and displays the current time and temperature, responding dynamically to environmental changes. Here’s an in-depth breakdown of its functionality:

### Key Components and Functionality
1. **RTC (Real-Time Clock) & Temperature Measurement**:
   - The DS3231 RTC module provides accurate timekeeping and a built-in temperature sensor. Each second, the program reads and formats the time into an `hh:mm:ss` format.
   - The temperature is also measured, formatted, and displayed in real-time. If the temperature is 22°C or higher, it triggers an action sequence to indicate high temperature.

2. **OLED Display Output**:
   - A 1306 OLED display shows the current time and temperature. The display refreshes each second with the latest data.
   - `oledWrite()` handles the formatting and rendering, writing both time and temperature in a readable format, including the temperature symbol (°C).

3. **Relay-Controlled Motor Activation**:
   - A motor connected to a relay (on `motorPin` 10) is controlled based on the temperature condition. If the temperature is 22°C or higher, the motor relay is activated, and it deactivates otherwise. This could be used, for instance, to power a cooling fan when the temperature threshold is reached.

4. **LED Indicators**:
   - Two LEDs connected in series to `ledPin` (pin 11) are also activated at high temperatures. The `blinkLEDs()` function blinks these LEDs rapidly five times to indicate a threshold temperature has been met. If the temperature falls below 22°C, the LEDs turn off.

5. **Servo Motor Temperature Mapping**:
   - A servo motor on `servoPin` 9 adjusts its position based on the temperature reading. Using `servoWrite()`, the temperature is mapped within a specified range (20°C to 30°C) to a servo angle between 0° and 180°. This allows the servo position to represent a relative temperature scale, which could be useful for visual indication or control.

### Code Structure and Flow
- **Setup (`setup()`)**: Initializes all components—RTC, servo, and OLED—along with setting pin modes for the motor relay and LEDs.
- **Loop (`loop()`)**:
   - Reads the time and temperature each second.
   - Displays time and temperature on the OLED.
   - Activates or deactivates the motor and LEDs based on the 22°C threshold.
   - Updates the servo position to reflect the current temperature.
