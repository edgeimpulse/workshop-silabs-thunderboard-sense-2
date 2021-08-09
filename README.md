# Example SiLabs Thunderboard Sense 2

This example has been designed for the [EOT - Electronic of Tomorrow 2021](https://www.eot.dk/besoeg/workshops) workshops.

* **Duration:** 2.5 hours
* **Difficulty:** Intermediate
* **Objectives:** Build your first TinyML application by collecting data from real sensor, setting your machine learning pipeline in the cloud, validating your model and deploying it back to your device.

## Workshop Agenda

1. Setup local environment
2. **Project 1: Movement classification using a 3-axis accelerometer**
 * Flash default Edge Impulse firmware
 * Collect data
 * Create an Impulse
 * Preprocess your data using Spectral Analysis
 * Train your machine learning model using Neural Networks
 * Validate your model 
 * Deploy your model
3. **Project 2: Keyword Spotting using a microphone**

## Hardware overview:

The Silicon Labs Thunderboard Sense 2 is a complete development board with a Cortex-M4 microcontroller, a wide variety of sensors, a microphone, Bluetooth Low Energy and a battery holder - and it's fully supported by Edge Impulse. You'll be able to sample raw data, build models, and deploy trained machine learning models directly from the studio - and even stream your machine learning results over BLE to a phone. It's available for around 20 USD directly from [Silicon Labs](https://docs.edgeimpulse.com/docs/silabs-thunderboard-sense-2).

![board-overview](assets/board-overview.png)

Thunderboard Sense 2 User's Guide: [Download PDF](https://www.silabs.com/documents/public/user-guides/ug309-sltb004a-user-guide.pdf)


## Requirements

### Hardware

* [SiLabs Thunderboard Sense 2](https://www.silabs.com/development-tools/thunderboard/thunderboard-sense-two-kit) development board.

### Software & tools

* [Edge Impulse Studio](https://studio.edgeimpulse.com/)
* [Edge Impulse CLI](https://docs.edgeimpulse.com/docs/cli-installation)
* [Docker](https://docs.docker.com/get-docker/) (optional but much easier to build the firmware)

If you don't want to use Docker, you will need:

* [Simplicity Studio 5](https://www.silabs.com/developers/simplicity-studio).
* [Python 3.6.8](https://www.python.org/downloads/release/python-368/) (make sure your Python version exactly match this version).
* [Java 64 bit JVM 11](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html) or higher.

## Setup your local environment (if not using Docker)

### Simplicity Studio

Download Simplicity Studio from this link: [Simplicity Studio 5](https://www.silabs.com/developers/simplicity-studio).

Use the provided installer to install it on your local machine.

Once installed, you should see the following view:

![ss5-installation-1](assets/ss5-installation-1.png)

Accept the agreements and create an account:

![ss5-create-account](assets/ss5-create-account.png)

Click on install in the menu and click on `Install by connecting device(s)`:

![ss5-installation-2](assets/ss5-installation-2.png)

Connect your SiLabs Thunderboard Sense 2 board to your computer using a micro usb:

![ss5-installation-3](assets/ss5-installation-3.png)

Now use the default parameters to install the required SDKs and dependencies. This step can take up to 15 minutes depending on your internet connection. Once finish, you will need to restart Simplicity Studio 5:

![ss5-installation-6](assets/ss5-installation-6.png)



## Project 1: Movement classification using a 3-axis accelerometer

### 1) Flash default Edge Impulse firmware

#### Connect the development board to your computer

Use a micro-USB cable to connect the development board to your computer. The development board should mount as a USB mass-storage device (like a USB flash drive), with the name TB004. Make sure you can see this drive.

#### Update the firmware

The development board does not come with the right firmware yet. To update the firmware:

1. [Download the latest Edge Impulse firmware](https://cdn.edgeimpulse.com/firmware/silabs-thunderboard-sense2.bin).
2. Drag the silabs-thunderboard-sense2.bin file to the TB004 drive.
3. Wait 30 seconds.

If dragging and dropping Edge Impulse .bin file results in FAIL.TXT

### 2) Collect data

### 3) Create an Impulse

### 4) Preprocess your data using Spectral Analysis

### 5) Train your machine learning model using Neural Networks

### 6) Validate your model 

### 7) Deploy your model

To deploy the model, you can either download the binary firmware from the studio or build the firwmare from the generated C++ libraries on your local machine. I strongly encourage you to test the second option as it will let you build custom applications in the future that can exactly match your needs. 

We will show you the two ways.

#### Download and flash the ready-to-go firmware:

![deployment-library](assets/deployment-library.png)






