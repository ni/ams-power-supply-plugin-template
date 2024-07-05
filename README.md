# bls-power-supply-plugin-template

This repository contains a template for building a Battery Lab Software Plugin for a power Supply.

# How to Use Template

1. Clone or download this repository.
2. Copy its contents into your project (including the hidden .github directory). 
3. Customize each file to suit your project's needs (including the README). Look through the files for "TODO" and \<reponame\>, and replace with content appropriate to your project.

## Supported Versions

- PAtools 8.4+
- LinuxRT 24Q2+
- LabVIEW 2023Q3+
- BLS Capabilities API 0.5+
- ADAS Replay HIL Development Suite 24Q1

1. Install the ADAS Replay and HIL AD Development Suite for LabVIEW.
1. Install the [BLS Capabilities API](https://github.com/ni/bls-capabilities).
1. Refer to the [ADAS Plugin Development](https://github.com/ni/adas-replay-hil-internal/wiki/Node-Development) to create your basic plugin.
1. Refer to the BLS Capabilities API Readme for more information.

## Package Deployer for BLS Plugins

The test/ plugin contains an example for a package which will install the lvlibp to the RT target. Follow these simple steps to update your Plugin.

1. Open your Plugin LabVIEW Project.
1. Right-click Build Specifications.
1. Select Package.
1. Under Source Files, select the lvlibp.
1. Select the blue arrow to add the lvlibp to the destination.
  - :cactus: LabVIEW will compile the lvlibp and automatically configure the directory.
1. Select Package and configure all the fields for your device.
1. Select OK.

# Power Supply with RMX Plugin Description

* The Power Supply Plugin takes in user inputs to control the system and values and then output the set values for items such as the voltage, power, and current of the device. The power supply is static and doesn't have a high current.
* To intialize and close channels used in the power supply plugin, create channels.vi and destroy channels.vi use the close and initialize from the BLS capabilities Power Supply high level capability which initialize and close all of the VI and classes that are implemented.
* The Power Supply with RMX template, uses the RMX412X library and its VIs to allow for testing on the power supply instead of a simulation. For this reason, process data.vi uses thw two VIs mentioned below to handle the data.
* In the Process Data.vi, the process input.vi and process output.vi are used. Using the read VIs and after checking for limits for current and volatge, they are passed as data into process input and set as outputs after checking for errors. Process output checks the status of errors and all of the output data which are then passed on to the write VIs.
* The Exit Initialize (User).vi uses the RMXPowerSupply class and allows for initialization so that the power supply can be used. 
* The Cleanup (User).vi should be adapted to ensure that all hardware and network references that were used in Exit Initialize.vi are closed.

# Testing

* The Power Supply with RMX Plugin can be tested by using the PAtools BLS dashboard and local PXI which allow for the control of input variables and monitoring of output values. 

# PAtools Integration
see [PAtools Integration Readme](/patools-integration/PAtools%20Integration%20README.md)