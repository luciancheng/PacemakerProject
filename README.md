# Pacemaker Project
This is a simulated pacemaker built to visually and functionally represent the various functions of modern pacemakers today. The following project is based of [Boston Scientific's](https://www.bostonscientific.com/en-US/Home.html) pacemaker specifications. 

Through model-based code generation and a python gui, we created the following features:
- 7 unique pacemaker modes (AOO, VOO, AAI, VVI, AOOR, VOOR, AAIR, VVIR)
- Real-time electrocardiogram display
- Local encrypted data storages     

## Technology Stack
[Python](https://www.python.org/) | [Matlab Simulink](https://www.mathworks.com/products/simulink.html) | [Customtkinter](https://customtkinter.tomschimansky.com/) | [NXP FRDM K64F Board](https://www.nxp.com/design/design-center/development-boards/freedom-development-boards/mcu-boards/freedom-development-platform-for-kinetis-k64-k63-and-k24-mcus:FRDM-K64F) | [J-Link](https://www.segger.com/downloads/jlink/)

## Showcase 
#### DCM
https://github.com/luciancheng/PacemakerProject/assets/121974540/d9b10d73-0702-4de9-b870-8f9678ef4c4d
<p align="center">
  <img src="![K64F-Board](https://github.com/luciancheng/PacemakerProject/assets/121974540/d9b10d73-0702-4de9-b870-8f9678ef4c4d)
" alt="" />
  <br>
  <em>The FRDM-K64F Board</em>
</p>
<p align="center">
  <img src="Images\Login-Screen.jpg" alt="" />
  <br>
  <em>Login Screen</em>
</p>
<p align="center">
  <img src="Images\Reg-Screen.jpg" alt="" />
  <br>
  <em>Registration Screen</em>
</p>
<p align="center">
  <img src="Images\Main-Screen.jpg" alt="" />
  <br>
  <em>Main Screen</em>
</p>
<p align="center">
  <img src="Images\Electrogram.jpg" alt="" />
  <br>
  <em>Live Electrogram in UI</em>
</p>

<p align="center">
  <img src="Images\Simulink_Overview.jpg" alt="" />
  <br>
  <em>Simulink Overview</em>
</p>
<p align="center">
  <img src="Images\Mode_Parameter_Stateflow.jpg" alt="" />
  <br>
  <em>Mode and Parameter Stateflow in Simulink</em>
</p>
<p align="center">
  <img src="Images\Serial_Comm.jpg" alt="" />
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
