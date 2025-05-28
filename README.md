# Muslim Prayer Reminder Game - High-Fidelity Prototype

## Project Overview

The Muslim Prayer Reminder Game is an innovative IoT-enabled smart device that combines traditional Islamic prayer timing with modern gamification principles. This high-fidelity prototype demonstrates the integration of embedded systems, real-time clock functionality, and interactive user engagement to promote consistent prayer habits within the Muslim community.

## Technical Architecture

### Hardware Components
- **Microcontroller**: Raspberry Pi Pico development board with integrated WiFi capability
- **Display Module**: 16x2 character LCD display with LiquidCrystal interface
- **Audio System**: Piezo buzzer for prayer alerts and feedback tones
- **Input Interface**: Single push button with internal pull-up resistor configuration
- **Connectivity**: Built-in WiFi module for internet-based prayer time synchronization
- **Pin Configuration**: 
  - LCD: RS(8), E(9), D4-D7(10-13)
  - Buzzer: GPIO pin 5
  - Button: GPIO pin 4 with INPUT_PULLUP

### Software Implementation
- **Programming Language**: C++ using Arduino IDE framework
- **API Integration**: Aladhan API (api.aladhan.com) for accurate Islamic prayer time calculations
- **Time Synchronization**: NTP (Network Time Protocol) client with UK pool servers
- **JSON Processing**: ArduinoJson library for API response parsing
- **Timezone Management**: Automatic British Summer Time (BST) and GMT detection
- **Network Protocol**: HTTPClient for RESTful API communication
- **Real-time Processing**: WiFiUDP for NTP time synchronization

## Key Features

### Core Functionality
- **Dynamic Prayer Time Calculation**: Integrates with Aladhan API using Method 2 (Islamic Society of North America) for precise prayer times based on London coordinates (51.5074°N, -0.1278°W)
- **Intelligent Time Zone Detection**: Automatically switches between GMT and BST using astronomical calculations for last Sunday transitions in March and October
- **Multi-Modal Notifications**: Four-tier alert system with distinct audio patterns:
  - 15-minute warning: Urgent rapid beeps
  - 1-hour reminder: Medium-urgency triple tone
  - Half-time alert: Gentle calm beeps (only if previous prayer unconfirmed)
  - Prayer time arrival: High-frequency alternating tone sequence
- **Prayer Confirmation System**: Single-button interface to confirm prayer completion with automatic recent prayer detection
- **Score Tracking**: Real-time point system displaying prayer completion progress on all display modes

### Advanced Features
- **Automatic Network Recovery**: WiFi connection with retry mechanism and fallback error handling
- **Cyclical Display Interface**: Three rotating display modes every 5 seconds:
  - Current UK time with timezone indication (GMT/BST)
  - Next prayer countdown with hours and minutes remaining
  - Prayer confirmation prompt for recently passed prayers
- **Smart Prayer Detection**: Algorithm identifies the most recent prayer time for confirmation based on current time analysis
- **Daily Reset Functionality**: Automatic midnight reset of prayer tracking status and score persistence
- **Robust Error Handling**: Comprehensive validation for API responses, time conversion, and network connectivity

## Technical Implementation Details

### Algorithm Design
The device employs sophisticated time management and prayer calculation algorithms:

- **Astronomical Time Calculations**: Implements Zeller's Congruence algorithm for precise day-of-week calculations
- **BST/GMT Detection**: Custom algorithm calculating last Sunday transitions using mathematical date analysis
- **Prayer Time Processing**: RESTful API integration with JSON deserialization and validation
- **Time Conversion Engine**: Converts various time formats (12/24-hour, AM/PM) to standardized minutes-since-midnight format
- **Intelligent Next Prayer Logic**: Dynamic calculation considering cross-day boundaries and prayer sequence

### User Experience Design
- **Status-Aware Interface**: Context-sensitive display showing relevant information based on prayer status
- **Non-Intrusive Notifications**: Smart alert system that prevents duplicate notifications using state flags
- **Visual Feedback Integration**: Consistent score display across all interface modes for continuous progress awareness
- **Error Recovery Design**: Graceful degradation with user-friendly error messages for network or API failures

### System Architecture
- **Event-Driven Programming**: Non-blocking code structure with time-based state management
- **Memory Efficient Design**: Optimized string handling and minimal dynamic allocation for stable Raspberry Pi Pico operation
- **Modular Function Design**: Separated concerns with dedicated functions for time management, display control, API communication, and audio alerts
- **State Machine Implementation**: Systematic tracking of prayer status, notification states, and display modes

## Development Process

### Design Methodology
This project follows a user-centered design approach, incorporating feedback from the Muslim community to ensure cultural sensitivity and practical utility. The development process included:

1. **Requirements Analysis**: Comprehensive study of traditional prayer reminder needs
2. **Prototype Development**: Iterative design and testing phases
3. **User Testing**: Community feedback integration and interface refinement
4. **Technical Optimization**: Performance tuning and reliability enhancements

### Quality Assurance
- Extensive testing across different geographic locations
- Validation of prayer time accuracy against established Islamic authorities
- Long-term reliability testing for continuous operation
- User acceptance testing with diverse demographic groups

## Installation and Setup

### Hardware Assembly
1. **Raspberry Pi Pico Setup**: Connect Raspberry Pi Pico development board to breadboard or PCB
2. **LCD Wiring**: Connect 16x2 LCD using standard 4-bit mode:
   - VSS and RW to ground
   - VDD to 5V power supply
   - V0 to potentiometer for contrast control
   - RS to digital pin 8, Enable to pin 9
   - D4-D7 to digital pins 10-13 respectively
3. **Audio System**: Connect piezo buzzer positive terminal to GPIO pin 5, negative to ground
4. **Input Interface**: Wire push button between GPIO pin 4 and ground (internal pull-up enabled in software)
5. **Power Supply**: Connect appropriate power source (USB or external 5V supply)

### Software Configuration
1. **Arduino IDE Setup**: Install Raspberry Pi Pico board package and required libraries:
   - LiquidCrystal (built-in)
   - WiFi (Raspberry Pi Pico core library)
   - NTPClient library
   - HTTPClient (Raspberry Pi Pico core library)
   - ArduinoJson library
2. **WiFi Credentials**: Update ssid and password variables in source code
3. **Location Settings**: Modify LATITUDE and LONGITUDE constants for your location
4. **Upload Firmware**: Compile and upload code to Raspberry Pi Pico using Arduino IDE

### Initial Calibration
- **Network Connection**: Device automatically connects to WiFi on startup with visual confirmation
- **Time Synchronization**: NTP client initializes with UK pool servers and automatic timezone detection
- **Prayer Time Retrieval**: System fetches current day's prayer times from Aladhan API with retry mechanism
- **Audio Verification**: Startup melody confirms successful initialization
- **Display Activation**: Automatic cycling through three display modes begins immediately

## Usage Instructions

### Daily Operation
- Device automatically displays current time and countdown to next prayer
- Visual and audio reminders activate at configured intervals before each prayer time
- Users confirm prayer completion through simple button interaction
- Progress tracking updates automatically with each confirmed prayer

### Game Mechanics
- Points awarded for timely prayer completion
- Streak bonuses for consecutive days of complete prayer schedules
- Achievement unlocks for reaching specific milestones
- Visual progress indicators showing weekly and monthly performance

## Technical Specifications

### Performance Metrics
- **Prayer Time Accuracy**: ±1 minute precision using Aladhan API with ISNA calculation method
- **Network Response Time**: 3-retry mechanism with 2-second intervals for API requests
- **Display Refresh Rate**: 5-second automatic cycling between display modes with 200ms loop delays
- **Button Response**: Real-time edge detection with debouncing for reliable prayer confirmation
- **Time Synchronization**: 60-second NTP update intervals with automatic BST/GMT switching
- **Memory Usage**: Optimized for Raspberry Pi Pico with efficient string handling and minimal heap allocation

### Compatibility
- **Hardware Platform**: Raspberry Pi Pico development boards with WiFi capability
- **Network Requirements**: 2.4GHz WiFi connection for API and NTP access
- **API Dependencies**: Aladhan.com Islamic prayer time service
- **Time Servers**: UK NTP pool (uk.pool.ntp.org) for accurate time synchronization
- **Geographic Scope**: Global compatibility with coordinate-based prayer time calculation

## Future Enhancements

### Planned Features
- **Enhanced Connectivity**: Integration of additional NTP servers for improved reliability
- **Extended Calculation Methods**: Support for multiple Islamic prayer time calculation methodologies
- **Mobile Integration**: Companion smartphone application for remote monitoring and configuration
- **Data Analytics**: Long-term prayer habit analysis and statistical reporting
- **Multi-User Support**: Family prayer tracking with individual score management

### Scalability Considerations
The modular Raspberry Pi Pico architecture supports integration of additional features:
- **GPS Module**: Automatic location detection for travelers
- **SD Card Storage**: Local prayer time caching and historical data storage
- **Bluetooth Connectivity**: Wireless configuration and smartphone synchronization
- **Additional Sensors**: Light sensors for automatic display brightness adjustment
- **Expandable Audio**: Support for full Adhan playback and customizable notification sounds

## Video Demonstration

A comprehensive video demonstration showcasing the device functionality, user interface, and game mechanics is available at: [https://youtu.be/gQxA02iXMRs](https://youtu.be/gQxA02iXMRs)

## Technical Skills Demonstrated

This project showcases comprehensive proficiency in multiple technical domains:

### Embedded Systems Programming
- **Raspberry Pi Pico Development**: Advanced microcontroller programming with WiFi integration
- **Real-time Systems**: Time-critical event handling and non-blocking code architecture
- **Hardware Interfacing**: LCD display control, buzzer audio generation, and button input processing
- **Memory Management**: Efficient resource utilization optimized for microcontroller constraints

### Network Programming & API Integration
- **RESTful API Consumption**: HTTP client implementation with JSON response parsing
- **Network Protocol Implementation**: NTP client integration for accurate time synchronization
- **Error Handling & Recovery**: Robust network connectivity management with retry mechanisms
- **Data Validation**: Comprehensive API response validation and error recovery

### Algorithm Development
- **Mathematical Implementations**: Zeller's Congruence algorithm for calendar calculations
- **Time Zone Logic**: Complex BST/GMT transition calculations using astronomical principles
- **State Machine Design**: Multi-state system management for prayer tracking and notifications
- **String Processing**: Efficient parsing and conversion of various time formats

### User Interface Design
- **Human-Computer Interaction**: Intuitive single-button interface design for diverse user demographics
- **Information Architecture**: Clear visual hierarchy and context-aware information display
- **Accessibility Considerations**: Simple interaction model suitable for users of all technical backgrounds
- **Real-time Feedback**: Immediate visual and audio confirmation of user actions

## Project Impact

The Muslim Prayer Reminder Game addresses a genuine need within the Muslim community by combining traditional religious practices with modern technology. The gamification approach encourages consistent prayer habits while respecting Islamic principles and cultural sensitivities.

## Repository Structure

```
├── src/
│   └── prayer_reminder_game.ino    # Complete Arduino/Raspberry Pi Pico source code
├── documentation/
│   ├── circuit_diagram/            # Hardware connection schematics
│   ├── api_documentation/          # Aladhan API integration details
│   └── user_manual.pdf            # End-user operation guide
├── hardware/
│   ├── component_list.txt         # Bill of materials and specifications
│   └── wiring_diagram.png         # Visual connection guide
└── demo/
    └── video_demonstration.mp4    # Complete functionality showcase
```

## Libraries and Dependencies

### Required Arduino Libraries
```cpp
#include <LiquidCrystal.h>       // LCD display control
#include <WiFi.h>                // Raspberry Pi Pico WiFi functionality  
#include <NTPClient.h>           // Network Time Protocol client
#include <WiFiUdp.h>             // UDP protocol for NTP
#include <HTTPClient.h>          // RESTful API communication
#include <ArduinoJson.h>         // JSON parsing and serialization
#include <time.h>                // Standard C time functions
#include <sys/time.h>            // System time utilities
```

### External API Services
- **Aladhan API**: Islamic prayer time calculations (api.aladhan.com)
- **UK NTP Pool**: Network time synchronization (uk.pool.ntp.org)

## Configuration Parameters

### Network Settings
- **WiFi SSID**: Configurable network name
- **WiFi Password**: Network authentication credentials
- **NTP Server**: UK pool NTP server with 60-second update intervals
- **API Endpoint**: Aladhan service with Method 2 (ISNA) calculation

### Location Settings
- **Default Coordinates**: London, UK (51.5074°N, -0.1278°W)
- **Timezone Management**: Automatic GMT/BST detection and switching
- **Prayer Method**: Islamic Society of North America (Method 2)

---

**Author**: Mohammad Faraj  
**Contact**: farajmohammad1427@gmail.com
**Project Type**: Digital Design & Smart Device Development  
**Development Period**: 3 days

This project demonstrates comprehensive skills in IoT development, embedded programming, and user-centered design, suitable for roles in hardware engineering, embedded systems development, and IoT product management.
