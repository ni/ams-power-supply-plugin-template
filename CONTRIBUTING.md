# Contributing to BLS Power Supply


# Getting Started

- Build steps
    - Expand "RT PXI Target"
    - Expand "Build Specifications"
    - Right-click "BLS Power Supply Template" and select "Build"

-  Rename the following project files
    - build file under build specifications
    - class and library
    - project
    - make sure this name change is reflected under configuration on PAtools

- Inisde of the Configuration Params.ctl file, which can be found by expanding "User Custom Config", change and adapt the parameters as needed.

# Using a Real Device

- Ensure that in Process Data.vi from the template, the simulation helper VIs and connections are removed and replaced with driver calls.The Process Data.vi can be used as a simulator to create connections between LLCs and ensure that an accurate output is generated. To use a real device, connect the ADAS HIL obect and Power Supply Objects to the Read and Write VIs for the capabilities. Process Input.vi and Process Output.vi can be used as helper VIs. 

- Make sure that inside of the Exit Initialize.vi, the device initialize VI is connected.

- Using the Cleanup (User).vi, make sure that everything is closed and exited such as hardware ports and network references.

# Testing

- Using PA tools
- Make sure to have the right IP address to input for the RMX Power Supply and PXI
- See PAtools Integration README.md for more info and details on how to connect and test

# Style Guide

These basic requirements should enforce meaningful consistency across capabilities without causing considerable developer pain.

1. All Block Diagrams should be arranged using `ctrl+u`
1. All Block Diagrams and Front Panels shall be sized using the built-in `ctrl+space` `ctrl+f` quick-drop formatter.
1. All Controls and Indicators on a block diagram shall be configured with "Show as Icon" `Unchecked`.
1. All Block Diagrams shall have Controls/Indicators formatted using the built-in `ctrl+space` `ctrl+t` quick-drop formatter.
1. All icons shall have a meaningful class name in the header.
1. All icons shall be formatted using the built-in `ctrl+space` `ctrl+k` quick-drop formatter (Use this after saving the VI).