# Workshop SiLabs Thunderboard Sense 2

This example has been designed for the [EOT - Electronic of Tomorrow 2021](https://www.eot.dk/besoeg/workshops) workshops.

* **Duration:** ~2.5 hours
* **Difficulty:** Intermediate
* **Objectives:** Build your first TinyML application by collecting data from real sensor, setting your machine learning pipeline in the cloud, validating your model and deploying it back to your device.

## Workshop Agenda

1. **Introduction** (~10 min)
2. **Setup local environment** (~15 min)
2. **Colaborative Project: Keyword Spotting using a microphone** (~20 min)
3. **Individual Project: Movement classification using a 3-axis accelerometer** 
 * Flash default Edge Impulse firmware (~15 min)
 * Collect data (~15 min)
 * Create an Impulse (~5 min)
 * Preprocess your data using Spectral Analysis (~5 min)
 * Train your machine learning model using Neural Networks (~15 min)
 * Validate your model (~5 min)
 * Deploy your model (~15 min)



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
* [Simplicity Studio 5](https://www.silabs.com/developers/simplicity-studio).

## Setup your local environment 

You can download the tools while we do the first collaborative project together so you can save time. Below is a quick guide on how to setup Simplicity Studio 5:

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

## Colaborative Project: Keyword Spotting using a microphone

During this first project, we will be **collecting the data together** and the instructor will show you the entire **pipeline to build your machine learning project**.
We will try to classify 4 keywords: `Play`, `Pause`, `Answer`, `Ignore` and a last class `Unknown` class. 

We will follow part of this tutorial in order to collect the data together: [Utilize the Power of the Crowd for Data Collection](https://www.edgeimpulse.com/blog/utilize-the-power-of-the-crowd-for-data-collection). Collecting data from various participants will have several benefits such as being able to quickly gather a lot of data while reducing the bias in the machine learning model. 

## Individual Project: Movement classification using a 3-axis accelerometer

In this project we will try to classify 5 kind of movements sampled at 100Hz: 

* `Circle`, drawing circles in the air with the board.
* `Square`, drawing rectangles in the air with the board.
* `Idle`, board sits idly on your desk.
* `Hold`, board is held in your hand, very close but slightly different from `idle` because of your breath movement for example. We will see later that it will be hard to classify `hold` vs `idle` correctly.
* `Unknown`, moving the board randomly.

Feel free to classify other kind of movements, such as `updown`, `snake`, `wave` like in this [tutorial](https://docs.edgeimpulse.com/docs/continuous-gestures) or `squats`, `jumping jacks` and `rest` like in this [tutorial](https://github.com/edgeimpulse/example-SparkFun-MicroMod-nRF52840).

The public version of this project can be found here: [https://studio.edgeimpulse.com/public/45631/latest](https://studio.edgeimpulse.com/public/45631/latest)


### 1) Flash default Edge Impulse firmware

#### Connect the development board to your computer

Use a micro-USB cable to connect the development board to your computer. The development board should mount as a USB mass-storage device (like a USB flash drive), with the name TB004. Make sure you can see this drive.

#### Update the firmware

The development board does not come with the right firmware yet. To update the firmware:

1. [Download the latest Edge Impulse firmware](https://cdn.edgeimpulse.com/firmware/silabs-thunderboard-sense2.bin).
2. Drag the silabs-thunderboard-sense2.bin file to the TB004 drive.
3. Wait 30 seconds, your board's led will switch on, change colors and switch off.

*If dragging and dropping Edge Impulse .bin file results FAIL.TXT, to fix this error, install the [Simplicity Studio 5 IDE](#simplicity-studio) and flash the binary through the IDE's built in "Upload application..." menu under "Debug Adapters", and select your Edge Impulse firmware to flash:*

![ss5-upload](assets/ss5-upload.png)


### 2) Collect data

If you do not have an Edge Impulse account yet, start by creating an account on [Edge Impulse Studio](https://studio.edgeimpulse.com) and create a project.

On this new project, select the `SiLabs Thunderboard Sense 2` board so the latency and performance estimations will calculated for your microcontroller:

![studio-overview](assets/studio-overview.png)

To start collecting some data, go to the `Data acquisition` view and click on the `Connect using WebUSB` button on the upper right corner:

![studio-webusb](assets/studio-webusb.png)

Collect your samples in the **Training data** tab. In this reference project, we collected 7m 30s equally split between 5 classes. You can set the `label`, the `frequency` and the `sample length` directly from the form on the right of the page: 

![studio-data-acquisition](assets/studio-data-acquisition.png)

Do not forget to add some samples in the **Test data** tab. We usually use around 80% of the samples for the training set and 20% in the test set. Here we collected 20 seconds for each class in the test set:

![studio-test-data](assets/studio-test-data.png)

The samples in the **Test data** won't be used during the training phase. We will use them later to validate the accuracy of our model.

Once you are happy with your data collection, you can move on to the next section where we will design our impulse.

### 3) Create an Impulse

With the training set in place you can design your impulse. An impulse takes the raw data, slices it up in smaller windows, uses signal processing blocks to extract features, and then uses a learning block to classify new data. Signal processing blocks always return the same values for the same input and are used to make raw data easier to process, while learning blocks learn from past experiences.

For this tutorial we'll use the `Spectral analysis` signal processing block. This block applies a filter, performs spectral analysis on the signal, and extracts frequency and spectral power data. Then we'll use a `Neural Network` learning block, that takes these spectral features and learns to distinguish between the four (idle, snake, wave, updown) classes.

![studio-create-impulse](assets/studio-create-impulse.png)

In the studio go to `Create impulse`, set the window size to `2000` (you can click on the 2000 ms. text to enter an exact value), the window increase to `80`, and add the `Spectral Analysis` and `Classification (Keras)` blocks. Then click `Save Impulse`.

### 4) Preprocess your data using Spectral Analysis

Navigate to the `Spectral analysis` page. You can leave the default parameters for now and come back later to this page to modify the parameters if you are not happy with your results. I also invite you to read our documentation on the [Spectral Analysis](https://docs.edgeimpulse.com/docs/spectral-features) processing block if you want to understand all the parameters.

![studio-spectral-analysis](assets/studio-spectral-analysis.png)

Click on `Save parameters` at the bottom of the page. You will arrive on the `Generate feature` view. Click on `Generate features` button as on the picture below:

![studio-generate-features](assets/studio-generate-features.png)

What is interesting to observe in the 3D visualisation is the ability to quickly detect some clusters in the samples. Here, the `idle` and `hold` classes are very close. This will certainly lead to some confusion in our Neural Network classification. We will see this in the next section.

You can play with the DSP parameters and regenerate your features to see if you can obtain a better speration of your samples according to their classes. In our case, we will leave the default parameters.


### 5) Train your machine learning model using Neural Networks

To train your machine learning model using neural networks, go to the `NN Classifier` page. 

**Keep in mind that working on a machine learning project is an iterative process, to obtain better results, you can add more data, train longer, adjust the DSP parameters, change your neural network architecture or hyper parameters.** You can check the [increasing model performances](https://docs.edgeimpulse.com/docs/increasing-model-performance) section on our documentation website for more tips. 

We will see several iterations we did for this project so you can better understand the process we have been following:

#### Version 1:

For the first version, leave the default parameters and click on `Start training`. Based on the data of this project and the previous parameters. We obtained a 77.1% of accuracy:

![studio-nn-1](assets/studio-nn-1.png)

As expected, when looking at the confusion matrix, we clearly see that the difficulty is to classify correctly `idle` and `hold`.

It is usually a good idea to verify the accuracy on samples that were unknown to the model during the training phase. To do so, under the `Model testing` page and click on `Classify all`. If you see a significant difference between the training accuracy and the testing accuracy, it usually means that your model was underfitting or overfitting:

![studio-validate-1](assets/studio-validate-1.png)

From now, we have several options to make the model better. 
Save the version of this model by clicking on `#1` and `Clone as new primary version`:

![studio-nn-version](assets/studio-nn-version.png)

#### Version 2:

The next step will be to add another layer to our model architecture. Click on `Add an extra layer` and choose a `Dense` layer of 10 neurons.

Train again your model, in this project, the accuracy won almost 20%!

![studio-nn-2](assets/studio-nn-2.png)

And for the model testing:

![studio-validate-2](assets/studio-validate-2.png)

#### Version 3:

For the third version, we trained longer (90 epochs), decreased the learning rate to `0.0003`, added a dropout layer to avoid overfitting. We obtained a 97.1% accuracy:

![studio-nn-3](assets/studio-nn-3.png)
![studio-validate-3](assets/studio-validate-3.png)

We will stop here but if you want to get an even better model, the next step would be to add some more data in your training set.


### 6) Deploy your model

To deploy the model, you can either download the binary firmware from the studio or build the firwmare from the generated C++ libraries on your local machine. I strongly encourage you to test the second option as it will let you build custom applications in the future that can exactly match your needs. 

We will show you the two ways.


#### Download and flash the ready-to-go firmware

![deployment-library](assets/deployment-library.png)

Select the SiLabs Thunderboard Sense 2 and click on `Build` at the bottom of the page.
Wait few seconds while your firmware gets generated. 

*What actually happens in the background is that by clicking on the build button, you trigger a pre-configured docker job that is compiling your firmware with your model parameters, similar to what we will see in the next section.*

Now you should have download the `.bin` firmware. Just drag and drop it under the `/TB004` USB mass-storage device. Wait a few seconds and open a terminal and type:

```
edge-impulse-run-impulse
```

And the device will start classifying your movements:

```
Edge Impulse impulse runner v1.13.10
WARN: You're running an outdated version of the Edge Impulse CLI tools
      Upgrade via `npm update -g edge-impulse-cli`
[SER] Connecting to /dev/tty.usbmodem0004401637981
[SER] Serial is connected, trying to read config...
[SER] Retrieved configuration
[SER] Device is running AT command version 1.3.0
[SER] Started inferencing, press CTRL+C to stop...
LSE
Inferencing settings:
	Interval: 10ms.
	Frame size: 600
	Sample length: 2000ms.
	No. of classes: 5
Starting inferencing, press 'b' to break
Starting inferencing in 2 seconds...
Sampling...
Predictions (DSP: 29 ms., Classification: 1 ms., Anomaly: 0 ms.): 
    circle: 	0.00000
    hold: 	0.10937
    idle: 	0.89062
    square: 	0.00000
    unknown: 	0.00000
Starting inferencing in 2 seconds...
```

#### Build the firmware from the C++ library

To build the firmware from the C++ library using Simplicity Studio 5, we will import a simplicity project file (`.sls` file), replace some generated folders in the `edgeimpulse` folder in order to build the firmware according to your projects parameters and finally, flash the firmware.

First open Simplicity Studio 5 and import the `simplicity-studio` folder present in this repository:

![ss5-import-project](assets/ss5-import-project.png)

Browse the folder location:

![ss5-import-project-1](assets/ss5-import-project-1.png)

Leave the default parameters:

![ss5-import-project-2](assets/ss5-import-project-2.png)

![ss5-import-project-3](assets/ss5-import-project-3.png)

![ss5-import-project-4](assets/ss5-import-project-4.png)

Once your workspace has successfully imported your project, go back to Edge Impulse Studio and download the C++ library of your project from the Deployment tab:

![studio-deployment-c+](assets/studio-deployment-c+.png)

Extract the `.zip` and copy the `model-parameters` and `tflite-model` folder from the generated library to the `edgeimpulse` folder in Simplicity Studio:

![ss5-copy-folders](assets/ss5-copy-folders.png)

*Note: As of Aug 26, 2021, `edge-impulse-sdk` from the generated library has not been updated with the latest version present in the `.sls` file. Do not replace it.*

Now select the "Copy files and folder" option, click `OK` and choose "Overwrite all" on the next screen.

![ss5-copy-file-and-folder](assets/ss5-copy-file-and-folder.png)

You can now compile the firmware by clicking on the hammer icon on the upper menu:

![ss5-compile](assets/ss5-compile.png)

Once finish, you should see a message on the Console looking similar to this:


```
Building hex file: ei-ssv5-project.hex
arm-none-eabi-objcopy -O ihex "ei-ssv5-project.axf" "ei-ssv5-project.hex"
 
Building bin file: ei-ssv5-project.bin
arm-none-eabi-objcopy -O binary "ei-ssv5-project.axf" "ei-ssv5-project.bin"
 
Building s37 file: ei-ssv5-project.s37
arm-none-eabi-objcopy -O srec "ei-ssv5-project.axf" "ei-ssv5-project.s37"
 
Running size tool
arm-none-eabi-size "ei-ssv5-project.axf" -A
ei-ssv5-project.axf  :
section              size        addr
.text              349576           0
.ARM.exidx              8      349576
.stack              32768   536870912
.data                1892   536903680
.bss                19464   536905572
.heap              208016   536925040
.nvm                 4096      349584
.ARM.attributes        46           0
.comment               77           0
.debug_info       1207717           0
.debug_abbrev      117623           0
.debug_loc         448371           0
.debug_aranges      13256           0
.debug_ranges       53416           0
.debug_macro       353083           0
.debug_line        585662           0
.debug_str        1997941           0
.debug_frame        53416           0
Total             5446428

16:08:49 Build Finished. 0 errors, 13 warnings. (took 21s.205ms)
```

To flash the device, do a right click on the `ei-ssv5-project.hex` file and select `Flash to Device`:

![ss5-flash](assets/ss5-flash.png)

Leave the default parameters and click on `Program`:

![ss5-flash-1](assets/ss5-flash-1.png)

![ss5-flash-2](assets/ss5-flash-2.png)

You device's RGB leds should blink. Wait a few seconds and open a terminal and type:

```
edge-impulse-run-impulse
```

And the device will start classifying your movements:

```
Edge Impulse impulse runner v1.13.10
WARN: You're running an outdated version of the Edge Impulse CLI tools
      Upgrade via `npm update -g edge-impulse-cli`
[SER] Connecting to /dev/tty.usbmodem0004401637981
[SER] Serial is connected, trying to read config...
[SER] Retrieved configuration
[SER] Device is running AT command version 1.3.0
[SER] Started inferencing, press CTRL+C to stop...
LSE
Inferencing settings:
	Interval: 10ms.
	Frame size: 600
	Sample length: 2000ms.
	No. of classes: 5
Starting inferencing, press 'b' to break
Starting inferencing in 2 seconds...
Sampling...
Predictions (DSP: 29 ms., Classification: 1 ms., Anomaly: 0 ms.): 
    circle: 	0.00000
    hold: 	0.10937
    idle: 	0.89062
    square: 	0.00000
    unknown: 	0.00000
Starting inferencing in 2 seconds...
```
