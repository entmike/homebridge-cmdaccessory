## NEW: Now supports GarageDoorOpener. Original author has gone dark and cannot approve pull request.

# homebridge-cmdaccessory [![npm version](https://badge.fury.io/js/homebridge-cmdaccessory.svg)](https://badge.fury.io/js/homebridge-cmdaccessory)
CMD Plugin for [HomeBridge](https://github.com/nfarina/homebridge) (API 2.0)

Based off of: [homebridge-cmdswitch2](https://github.com/luisiam/homebridge-cmdswitch2)

### Special Thanks

Special thanks to @luisiam for cmdswitch2.  It's great.  This is 95% that plugin, but I met a friend who wanted certain "switches" to appear as different types of accessories.

### What this plugin does
This plugin works much like [homebridge-cmdswitch2], it allows you to run Command Line Interface (CLI) commands via HomeKit. This means you can run a simple commands such as `ping`, `shutdown`, or `wakeonlan` just by telling Siri to do so. An example usage for this plugin would be to turn on your PS4 or HTPC, check if it’s on, and even shut it down when finished.

This plugin also adds a `type` property for the `config.json` to support a few different HAP types.  At this time, the following types are supports:

- Switch
- Lightbulb
- Outlet
- LockMechanism

### How this plugin works
1. `on_cmd`: This is the command issued when the accessory is set to "ON" (or Locked, etc).
2. `off_cmd`: This is the command issued when the accessory is turned OFF (or Unlocked, etc).
3. `state_cmd`: This is the command issued when HomeBridge checks the state of the accessory.
  1. If there is no error, HomeBridge is notified that the accessory is ON (or Locked, etc).
  2. If there is an error, HomeBridge is notified that the accessory is OFF (or Unlocked, etc).

### Things to know about this plugin
This plugin can only run CLI commands the same as you typing them yourself. In order to test if your `on_cmd`, `off_cmd`, or `state_cmd` are valid commands you need to run them from your CLI. Please keep in mind you will want to run these commands from the same user that runs (or owns) the HomeBridge service if different than your root user.

# Installation
1. Install homebridge using `npm install -g homebridge`.
2. Install this plugin using `npm install -g homebridge-cmdaccessory`.
3. Update your configuration file. See configuration sample below.

# Configuration
Edit your `config.json` accordingly. Configuration sample:
 ```
"platforms": [{
    "platform": "cmdAccessory"
}]
```

### Advanced Configuration (Optional)
This step is not required. HomeBridge with API 2.0 can handle configurations in the HomeKit app.
 ```
"platforms": [{
			"platform": "cmdAccessory",
			"name": "CMD Accessory",
			"switches": [{
					"name": "iTunes Switch Test",
					"on_cmd": "start /B c:/start_itunes.cmd",
					"off_cmd": "Taskkill /IM itunes.exe /F",
					"state_cmd": "c:/itunes.cmd",
					"polling": true,
					"interval": 3,
					"manufacturer": "Apple",
					"type" : "Switch"
				},{
					"name": "Test Outlet",
					"on_cmd": "start /B c:/start_itunes.cmd",
					"off_cmd": "Taskkill /IM itunes.exe /F",
					"state_cmd": "c:/itunes.cmd",
					"polling": true,
					"interval": 3,
					"manufacturer": "Apple",
					"type" : "Outlet"
				},{
					"name": "Test Lock 2",
					"on_cmd": "start /B c:/start_itunes.cmd",
					"off_cmd": "Taskkill /IM itunes.exe /F",
					"state_cmd": "c:/itunes.cmd",
					"polling": true,
					"interval": 3,
					"manufacturer": "Apple",
					"type" : "LockMechanism"
				},{
					"name": "Test Bulb 3",
					"on_cmd": "start /B c:/start_itunes.cmd",
					"off_cmd": "Taskkill /IM itunes.exe /F",
					"state_cmd": "c:/itunes.cmd",
					"polling": true,
					"interval": 3,
					"manufacturer": "Apple",
					"type" : "Lightbulb"
				}
			]
		}
	]
```


| Fields           | Description                                             | Required |
|------------------|---------------------------------------------------------|----------|
| platform         | Must always be `cmdSwitch2`.                            | Yes      |
| name             | For logging purposes.                                   | No       |
| switches         | Array of switch config (multiple accesories supported). | Yes      |
| \|- name\*       | Name of your device.                                    | Yes      |
| \|- type\*       | Type of accessory.                                      | Yes      |
| \|- on_cmd       | Command to turn on your device.                         | No       |
| \|- off_cmd      | Command to turn off your device.                        | No       |
| \|- state_cmd    | Command to detect an ON state of your device.           | No       |
| \|- polling      | State polling (Default false).                          | No       |
| \|- interval     | Polling interval in `s` (Default 1s).                   | No       |
| \|- manufacturer | Manufacturer of your device.                            | No       |
| \|- model        | Model of your device.                                   | No       |
| \|- serial       | Serial number of your device.                           | No       |
\*Changing the switch `name` in `config.json` will create a new switch instead of renaming the existing one in HomeKit. It's strongly recommended that you rename the switch using a HomeKit app only.
