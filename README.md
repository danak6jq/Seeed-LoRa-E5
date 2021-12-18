# Seeed-LoRa-E5
LoRaWAN end node built from scratch using STM32CubeIDE/CubeMX for the LoRa-E5 WLE5x

## This assumes a general familiarity with STM32CubeIDE and LoRaWAN concepts.
If you haven't used STM32CubeIDE before, I suggest doing a couple of smaller projects using ST Nucleo boards to familiarize yourself.

## From the Seeed-Studio repo: Before starting

- Please read [Erase Factory AT Firmware](https://wiki.seeedstudio.com/LoRa_E5_mini/#21-erase-factory-at-firmware) section first, you need to retrieve and save the Device EUI, then erase the Factory AT Firmware before we program with SDK

- Install V1.7.0 or later [STM32CubeIDE(to compilation and debug)](https://my.st.com/content/my_st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-ides/stm32cubeide.html) and [STM32CubeProgrammer(to program STM32 devices)](https://my.st.com/content/my_st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-programmers/stm32cubeprog.license=1614563305396.product=STM32CubePrg-W64.version=2.6.0.html). Launch STM32CubeIDE and install V1.1.0 of [STM32Cube MCU Package for STM32WL series(SDK)](https://my.st.com/content/my_st_com/en/products/embedded-software/mcu-mpu-embedded-software/stm32-embedded-software/stm32cube-mcu-mpu-packages/stm32cubewl.license=1608693595598.product=STM32CubeWL.version=1.0.0.html#overview)

- LoRaWAN Gateway connected to LoRaWAN Network Server(e.g. TTN; I am using a local gateway and local ChirpStack server)

- Prepare an USB TypeC cable and a ST-LINK. Connect the TypeC cable to the TypeC port for power and serial communication, connect the ST-LINK to the SWD pins like this (recommend connecting Vcc and nRST as well):

![image](https://user-images.githubusercontent.com/942815/145846356-6c3d4828-18b1-40a3-a6d0-25d979629093.png)

- Before erasing the Seeed factory AT firmware, get the Device EUI. Connect a USB-C cable to the LoRa-E5, and send AT command AT+ID=DevEui to get your Device EUI:

<img width="271" alt="image" src="https://user-images.githubusercontent.com/942815/145845362-979a73a7-1e80-4a8b-911a-979d7df967b1.png">

- Do not lose this Device EUI; it is unique for each LoRaWAN device.

# Building the repo

- Clone this repo onto a system with STM32CubeIDE, v1.7.0 or later. Using "Open Projects From Filesystem"

<img width="275" alt="image" src="https://user-images.githubusercontent.com/942815/145841281-36e9181f-250d-4432-864e-ef5096f2731d.png">

- Locate and open the top-level directory of the cloned repo:

<img width="134" alt="image" src="https://user-images.githubusercontent.com/942815/145841729-a7c1243e-06eb-4d5d-81ed-4a3109695db2.png">

- Modify your Device EUI, Application EUI, Application KEY and your LoRawan Region

- Use Cube to reconfigure the project to your LoRaWAN commissioning parameters:

![image](https://user-images.githubusercontent.com/942815/145844142-675eb76c-7bb3-4991-9df4-8e86999afb3b.png)

and

![image](https://user-images.githubusercontent.com/942815/145844024-5a685612-e9ca-46f8-a8a8-25919aa81b03.png)

- Save the IOC file and generate code when prompted:

<img width="477" alt="image" src="https://user-images.githubusercontent.com/942815/145848348-1f3722f7-1265-4442-8851-5d90d8161167.png">

<img width="477" alt="image" src="https://user-images.githubusercontent.com/942815/145848405-9c149798-f944-4b62-be2c-e204ea618cf5.png">

- Note that generating code overwrites many files; in particular, if you've selected Hybrid Mode to operate a in a sub-band, you need to check and correct the channel mask after generating code - example here is for US915 Sub-band 2:

![image](https://user-images.githubusercontent.com/942815/145849008-5042b29e-5772-4bd6-a7d0-ca22ff51df11.png)

- Build project and program it into the LoRa-E5

<img width="184" alt="image" src="https://user-images.githubusercontent.com/942815/145849530-b4362b56-9a94-4ca7-8a5a-805bc0044b18.png">
<img width="245" alt="image" src="https://user-images.githubusercontent.com/942815/145849464-3384556a-ce2e-4521-918a-dba60e583022.png">

## Starting a new project

- Use "Start a new project from an existing configuration file" and select "Seeed-LoRa-E5.ioc" in the repo

<img width="613" alt="image" src="https://user-images.githubusercontent.com/942815/145850066-bbd75cbc-b373-4332-898d-0140b003da20.png">

- This creates a new "End client framework" project with no user code (such as contained in the repo code) included. You'll want to refer to the repo code and ST documentation for using their LoRaWAN stack.

