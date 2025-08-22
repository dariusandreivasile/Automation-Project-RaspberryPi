# Automation-Project-RaspberryPi
The purpose of this project is to design and implement an automatic irrigation system that is able to monitor soil moisture levels and water the plants whenever the soil becomes too dry. The system is intended to reduce manual work, optimize water consumption, and ensure that plants remain healthy. The main objective is to use a Raspberry Pi as the central controller, connected to a soil moisture sensor and a relay that switches the power supply of a Gardena irrigation system through a controlled outlet.

## Features
- Soil moisture acquisition via MCP3208 (12-bit) → percentage with dry/wet calibration
- Automatic irrigation: threshold + hysteresis + minimum ON time + cooldown
- Manual button (GPIO17) to toggle AUTO mode
- Relay control on GPIO5 (supports active-LOW modules)
- MQTT payload: `{ "moisture": <percent>, "button_state": true/false }`

## Hardware
- Raspberry Pi (any with 40-pin header)
- MCP3208 ADC
- Soil moisture sensor (analog output)
- Relay module (GPIO-driven, ideally opto-isolated)
- Gardena irrigation system powered through the relay-controlled outlet
- Breadboard & jumper wires

## Wiring (summary)
- MCP3208: VDD→3.3V, VREF→3.3V, AGND/DGND→GND, CLK→GPIO11, DOUT→GPIO9, DIN→GPIO10, CS→GPIO8
- Sensor AO→MCP3208 CH0, Sensor VCC→3.3V, Sensor GND→GND
- Button: one leg → GPIO17, opposite leg → GND (internal pull-up in code)
- Relay IN→GPIO5, VCC→(module spec: 3.3V or 5V), GND→GND (common with Pi)
