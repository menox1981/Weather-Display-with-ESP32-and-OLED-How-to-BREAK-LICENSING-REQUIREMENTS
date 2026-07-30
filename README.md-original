# Weather-Display-with-ESP32-and-OLED  

This project demonstrates how to build a versatile and dynamic weather display using an ESP32 microcontroller and an OLED screen. The device fetches real-time weather data from the OpenWeatherMap API and displays the current temperature for a user-specified location.  

## Features  

- 🌐 **Real-Time Weather Display**  
  Fetches live weather data for any location using the OpenWeatherMap API.  

- ✨ **Dynamic Configuration**  
  Configure Wi-Fi credentials, OpenWeatherMap API key, and location through a user-friendly web interface—no need to modify the code!  

- 📶 **Wi-Fi Provisioning**  
  Uses the WiFiManager library to enable seamless connection to different Wi-Fi networks without modifying the firmware.  

- 🖥️ **OLED Display Integration**  
  Displays weather information on an OLED screen using the Adafruit SSD1306 library, with a clean and readable layout.  

- 🚨 **Error Handling**  
  Gracefully handles issues such as failed API requests, invalid responses, or connectivity problems, ensuring the interface remains responsive.  

## Getting Started  

### Hardware Requirements  

- ESP32 microcontroller  
- SSD1306-compatible OLED display (e.g., 128x64 pixels)  
- Breadboard and jumper wires  

### Software Requirements  

- Arduino IDE (with ESP32 board support installed)  
- Required libraries:  
  - [WiFiManager](https://github.com/tzapu/WiFiManager)  
  - [Adafruit SSD1306](https://github.com/adafruit/Adafruit_SSD1306)  
  - [Adafruit GFX](https://github.com/adafruit/Adafruit-GFX-Library)  

## Configuration Steps  

1. 📥 **Clone or Download**  
   Clone this repository to your local machine.  

2. 🛠️ **Open the Code**  
   Open the `.ino` file in the Arduino IDE.  

3. 🔧 **Initial Setup**  
   Upload the code to your ESP32. Upon the first run, the device will host a Wi-Fi setup portal named `ESP32-Config`. Connect to this network using a smartphone or computer, and follow the web interface to input:  
   - Wi-Fi credentials  
   - OpenWeatherMap API key  
   - City and country code  

4. 🌍 **Change Configuration Anytime**  
   The web interface can be accessed later to update credentials or location without re-uploading the code.  

## Example Configuration  

To fetch weather data for **Berlin, Germany**:  
- **City**: `Berlin`  
- **Country Code**: `de`  
- Example API Request:  
  `https://api.openweathermap.org/data/2.5/weather?q=Berlin,de&appid=[API_KEY]&units=metric`  

## How It Works  

1. The ESP32 hosts a web portal to allow easy configuration of Wi-Fi and weather settings.  
2. Once connected, the device fetches weather data from OpenWeatherMap at regular intervals.  
3. The OLED screen displays the city name, current temperature, and additional error messages if needed.  

## Next Steps  

Consider extending the functionality:  
- Add support for displaying additional weather details like humidity, wind speed, or weather conditions.  
- Enable multi-language support for location names and weather descriptions.  

## Contributions  

Feedback and contributions are welcome! If you encounter any issues or have suggestions, feel free to open an issue or create a pull request.  
