# Example SiLabs Thunderboard Sense 2

This example has been designed for the [EOT - Electronic of Tomorrow 2021](https://www.eot.dk/besoeg/workshops) workshops.

* **Duration:** 2.5 hours
* **Difficulty:** Intermediate
* **Objectives:** Build your first TinyML application by collecting data from real sensor, setting your machine learning pipeline in the cloud, validating your model and deploying it back to your device.

## Workshop Agenda

1. Edge Impulse Introduction
2. **Project 1: Movement classification using a 3-axis accelerometer**
 * Flash default Edge Impulse firmware
 * Collect data
 * Create an Impulse
 * Preprocess your data using Spectral Analysis
 * Train your machine learning model using Neural Networks
 * Validate your model 
 * Deeploy your model
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

Alternatively (if not using Docker):

* [Simplicity Studio 5](https://www.silabs.com/developers/simplicity-studio).
  * Gecko SDK v3
  * Bluetooth SDK v3
* Python 3.6.8 or higher and the following packages.
* Java 64 bit JVM 11 or higher:
    - available at [Amazon Correto](https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html) or [releases page](https://github.com/corretto/corretto-11/releases).






