# Automation-Project-RaspberryPi
This project implements a low-cost smart irrigation controller using a Raspberry Pi, an MCP3208 ADC, a soil moisture sensor, a toggle button, and a relay that powers a Gardena irrigation system. The Raspberry Pi reads soil moisture as a percentage, publishes telemetry to MQTT, and can automatically start/stop irrigation based on a configurable threshold with hysteresis. A physical button toggles automation mode.

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
