This is the PebblePower ESPHome firmware for all PebblePower devices. This README.md is intended to be a quickstart guide for users to get up and running with their devices.

For more detailed information on flashing and configuration please refer to the [PebbleTek documentation](https://pebbletek.notion.site/)

# PebblePower ESPHome Firmware

This repository contains the ESPHome firmware for all PebblePower devices and is used to flash the devices. It is designed to enable users to make minimal changes to templates and all the heavy lifting is done with packages and includes that users don't need to edit.

It is a maintained project and will be updated regularly to add new features and fix bugs. Please follow the recommended processes to ensure that you can update your clone of this project in the future without breaking any of your local changes.

> [!TIP]
> The general concept of ESPHome is that you create a .yaml file for each device and ESPHome uses that file to compile a binary unique to your device. There are various pros and cons of using different firmware solutions and one of ESPHome specific benefits is that it directly integrates with Home Assistant. Visit the [ESPHome website](https://esphome.io/) for more information.

## Features

- Supports PebblePower1, 2, 4, 8 and 12
- Configurable onboard and external buttons
- Relay control
- Real-Time Power Monitoring
- Wi-Fi connectivity
- Sensor integration
- OTA updates
- Home Assistant integration

## Installation
The following instructions assume that you have a working pyhtin, pip and Github environment with SSH access keys setup for Github.

1. Clone the repository
```
git clone https://github.com/PebbleTek/pebblepower_esphome.git
```
2. Install esptool.py (optional but recommended)
```
pip install esptool
```

3. Install ESPHome
```
pip install esphome
```

## Configuration

The general process to get your device flashed and running is to connect it via USB to your PC or Mac then follow the steps below:

1. Create a secrets.yaml file from the secrets.yaml.example file. This file should contain all your local sensitive information and is excluded from the repository.

2. Create a unique esphome file for your device using the PebblePower_uniquename.yaml.template file as a template
- Rename the file to PebblePower_uniquename.yaml updating "uniquename" with a name of your choice.  
- Edit the file to set your desired features and options using the comments in the file as a guide.

3. Flash the device using the esphome CLI
```
esphome run PebblePower_uniquename.yaml
```
Once the device has been flashed you should see from the esphome CLI that the device has booted and connected to your Wi-Fi network. You can use this information to find the IP address of your device and then access the PebblePower dashboard to use the device.

## Additional Information

### Secrets

To ensure that your sensitive information is not exposed to the public repository it should be stored in a `secrets.yaml` file which is specifically excluded from the repository using .gitignore. Create a `secrets.yaml` file based on the `secrets.yaml.example` provided. This file should contain your sensitive information such as:

- Wi-Fi SSID and password
- Home Assistant API key
- OTA password
- Access Point password

### Advanced Configuration

The default and simplest option is to have Relay names resued across relays, onboard buttons and external switches. You can however create much more complex configurations if you wish to do so with seprate names and actions for any combination of Relays, Buttons and Switches. 

You can customise the names of onboard and external buttons independently by modifying your device specific .yaml file and overriding the defaults provide in the /devices folder.

The recommended way to create your own unique device specific configuration is to keep the /devices file as an include and override the specific items you wish to change in the device specific .yaml file.

### Everything is Addressable

PebblePower devices use independent GPIO pins for relays, buttons, and external buttons. PebblePower8 and PebblePower12 also have addressable LEDs which are also individually addressable by individual LED. All devices also have two I2C busses which can be used for sensors or other devices.

The default firmware utilises all of the above in its simplest form but its important to note that, by design, everything is individually addressable and you can create much more complex interactions if you wish to do so.

## Development

PebblePower devices are ESP32 based and there are different firmware projects available depending on the use case. This specific project uses ESPHome for firmware development. Make sure you have ESPHome installed and configured properly before making any changes.

### Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

GNU Affero General Public License (AGPL)

This project is licensed under the GNU Affero General Public License (AGPL) v3.0. This means that you are free to use, modify, and distribute the software, but you must disclose the source code, allow users to access the source code, and you must do so with the same license.

## Support

For support, please refer to the [PebbleTek documentation](https://pebbletek.notion.site/) or contact PebbleTek support.
