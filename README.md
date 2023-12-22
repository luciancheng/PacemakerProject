# Pacemaker Project
This is a simulated pacemaker built to visually and functionally represent the various functions of modern pacemakers today. The following project is based of [Boston Scientific's](https://www.bostonscientific.com/en-US/Home.html) pacemaker specifications. 

Through model-based code generation and a python gui, we created the following features:
- 7 unique pacemaker modes (AOO, VOO, AAI, VVI, AOOR, VOOR, AAIR, VVIR, DDD, DDDR)
- Real-time electrocardiogram display
- Local encrypted data storages     

## Technology Stack
[Python](https://www.python.org/) | [Matlab Simulink](https://www.mathworks.com/products/simulink.html) | [Customtkinter](https://customtkinter.tomschimansky.com/) | [NXP FRDM K64F Board](https://www.nxp.com/design/design-center/development-boards/freedom-development-boards/mcu-boards/freedom-development-platform-for-kinetis-k64-k63-and-k24-mcus:FRDM-K64F) | [J-Link](https://www.segger.com/downloads/jlink/)

## Showcase 
#### DCM

<p align="center">
  <img src="https://github.com/luciancheng/PacemakerProject/assets/121974540/bedb9ad1-2879-42bf-a6e7-fcb664fa2192"/>
  <em>The FRDM-K64F Board</em>
</p>

![Login-Screen](https://github.com/luciancheng/PacemakerProject/assets/121974540/06ba023e-5ed8-410f-9da2-7d511245351c)

<p align="center">
  <br>
  <em>Login Screen</em>
</p>

![Reg-Screen](https://github.com/luciancheng/PacemakerProject/assets/121974540/be1af9e4-7fe8-4fe8-9742-6201c47416f6)

<p align="center">
  <br>
  <em>Registration Screen</em>
</p>

![Main-Screen](https://github.com/luciancheng/PacemakerProject/assets/121974540/6b640e71-7199-4250-8c9a-636f1ad628ae)

<p align="center">
  <br>
  <em>Main Screen</em>
</p>

![Electrogram](https://github.com/luciancheng/PacemakerProject/assets/121974540/523ae781-556d-49fd-928e-475a5920ca20)

<p align="center">
  <br>
  <em>Live Electrogram in UI</em>
</p>

![Simulink_Overview](https://github.com/luciancheng/PacemakerProject/assets/121974540/11ed58a5-c518-4c06-8126-b36a201e1ca3)

<p align="center">
  <br>
  <em>Simulink Overview</em>
</p>

![Mode_Parameter_Stateflow](https://github.com/luciancheng/PacemakerProject/assets/121974540/03a3141e-0181-449d-b27d-221a6d90c3c9)

<p align="center">
  <br>
  <em>Mode and Parameter Stateflow in Simulink</em>
</p>

![Serial_Comm](https://github.com/luciancheng/PacemakerProject/assets/121974540/61bb4548-36a7-4f1c-a27a-426864e7b848)

<p align="center">
  <br>
  <em>Serial Communication Stateflow in Simulink</em>
</p>


## Development Process
#### Modeling with MATLAB Simulink
Central to modelling our pacemaker's functionality was the use of MATLAB Simulink, which allowed us to generate code iteratively and quickly flash our code into our board. 

Through user-set parameters, our Simulink code allow for pacing of both the atrium and ventricle alongside rate adaptive pacing with a in-built accelerometer. 

All important user-set data and electrocardiogram data was framed. The resulting packet was sent through a micro-usb to the device controller monitor.  
#### Device Controller Monitor (DCM)
Through python's tkinter, we created a secure interface that allows for the modification of the pacemaker. Our GUI allows for:
- Real-time display of the simulated heartbeat
- Patient data to be saved and modified
- Encryption of patient data
- Serial communication to the K64F board

#### Validation
To test and validate our pacemaker mode function, we employed Heartview, a McMaster created cardiac simulation tool that was pre-flashed onto our board.

## Installation
#### Prerequisites
1. Python 3.18 or later
2. MATLAB Simulink 2023 or later

#### Python Libraries 
```bash
pip install customtkinter matplotlib serial cyrptography 
```

#### MATLAB Simulink Libraries
- Embedded Coder, Fixed-Point Designer, MATLAB Coder, Simulink Check, Simulink Coder, Simulink Coverage, Simulink Design Verifier, Simulink Desktop Real-Time, Simulink Test, and Stateflow
- [Simulink Coder Support Package for NXP FRDM-K64F Board](https://www.mathworks.com/matlabcentral/fileexchange/55318-simulink-coder-support-package-for-nxp-frdm-k64f-board#:~:text=Simulink%C2%AE%20Coder%E2%84%A2%20Support,K64F%20peripherals%20and%20communication%20interfaces.)
- [Kinetis SDK 1.2.0 mainline release](https://www.nxp.com/design/design-center/designs/software-development-kit-for-kinetis-mcus:KINETIS-SDK)
- [V6.20a of the J-Link Software](https://www.segger.com/downloads/jlink/)

In MATLAB, write the following in to the terminal:
```matlab
open([codertarget.freedomk64f.internal.getSpPkgRootDir,
'/src/mw_sdk_interface.c']);
```
Upon opening the device change the following line:
```matlab
{ GPIO_MAKE_PIN(GPIOA_IDX, 0),  MW_NOT_USED},// PTA0, D8
```
into the following:
```matlab
{ GPIO_MAKE_PIN(GPIOC_IDX, 12),  MW_NOT_USED},// PTC12, D8
```
