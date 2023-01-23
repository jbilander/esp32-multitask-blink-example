# esp32-multitask-blink-example
FreeRTOS blink two LEDs example for the ESP32, FreeRTOS allows us to handle several tasks in parallel that run independently.<br />
<br />
Example is taken from here:<br />
https://randomnerdtutorials.com/esp32-dual-core-arduino-ide/
<br />
<br />
Why is this useful? <br />
In real life, instead of blinking LEDs, this can be tasks like making a network request, measuring sensors, controlling a motor, etc…<br />
It will then be useful to assign specific parts of the code to a specific core in order to optimize performance.

***

<a href="https://user-images.githubusercontent.com/1673918/214081208-1367c18b-2388-4d43-b41c-8212f15f3aa6.jpg">
<img src="https://user-images.githubusercontent.com/1673918/214081208-1367c18b-2388-4d43-b41c-8212f15f3aa6.jpg" width="512" height="384">
</a>

***

Demo video here:<br />
https://drive.google.com/file/d/1HbspRSdvF7cROVlgxRoYOVJftApYekXf/view?usp=sharing

***

### Prerequisites

* Download and install Visual Studio Code
* Download and install `arduino-cli` (pre-built binary)<br /> 
  https://arduino.github.io/arduino-cli/0.21/installation/#latest-release
* Set the PATH to the folder where `arduino-cli` is located (`arduino-cli.exe` on Windows).
* Install/Activate the Extension: Arduino for Visual Studio Code.
* CP2102 USB to UART bridge chip drivers installed (or whatever chip your ESP32 module has for this)<br />
  https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers?tab=downloads
  <br />
  <br />
  ![CP2102_USB_to_UART_Bridge](https://user-images.githubusercontent.com/1673918/214069209-56d945dc-1b37-4c78-b382-b7765a6d2505.jpg)


***

![VSCode_screenshot_pic3](https://user-images.githubusercontent.com/1673918/214077845-6be800e5-e5d7-4c59-bd0b-4736d077ea9f.jpg)

***

### Installation (on Windows)

    C:\>arduino-cli config init
        Config file written to: C:\Users\Jorgen\AppData\Local\Arduino15\arduino-cli.yaml
    
    C:\>arduino-cli config add board_manager.additional_urls https://dl.espressif.com/dl/package_esp32_index.json
    
    C:\>arduino-cli config dump
        board_manager:
          additional_urls:
          - https://dl.espressif.com/dl/package_esp32_index.json
    
    C:\>arduino-cli board listall
        Downloading missing tool builtin:ctags@5.8-arduino11...
        builtin:ctags@5.8-arduino11 downloaded
        Installing builtin:ctags@5.8-arduino11...
        builtin:ctags@5.8-arduino11 installed
        Downloading missing tool builtin:serial-discovery@1.3.3...
        builtin:serial-discovery@1.3.3 downloaded
        Installing builtin:serial-discovery@1.3.3...
        builtin:serial-discovery@1.3.3 installed
        Downloading missing tool builtin:mdns-discovery@1.0.6...
        builtin:mdns-discovery@1.0.6 downloaded
        Installing builtin:mdns-discovery@1.0.6...
        builtin:mdns-discovery@1.0.6 installed
        Downloading missing tool builtin:serial-monitor@0.12.0...
        builtin:serial-monitor@0.12.0 downloaded
        Installing builtin:serial-monitor@0.12.0...
        builtin:serial-monitor@0.12.0 installed
        Board Name FQBN
        
    C:\>arduino-cli core install esp32:esp32
        Downloading packages...
        esp32:xtensa-esp32-elf-gcc@1.22.0-97-gc752ad5-5.2.0 downloaded
        esp32:esptool_py@3.0.0 downloaded
        esp32:mkspiffs@0.2.3 downloaded
        esp32:esp32@1.0.6 downloaded
        Installing esp32:xtensa-esp32-elf-gcc@1.22.0-97-gc752ad5-5.2.0...
        esp32:xtensa-esp32-elf-gcc@1.22.0-97-gc752ad5-5.2.0 installed
        Installing esp32:esptool_py@3.0.0...
        esp32:esptool_py@3.0.0 installed
        Installing esp32:mkspiffs@0.2.3...
        esp32:mkspiffs@0.2.3 installed
        Installing platform esp32:esp32@1.0.6...
        Configuring platform....
        Platform esp32:esp32@1.0.6 installed
    
    Please note, this last step below is not needed if you clone this repository
    
    C:\Users\Jorgen\Projects>arduino-cli sketch new esp32-multitask-blink-example
        Sketch created in: C:\Users\Jorgen\Projects\esp32-multitask-blink-example
        
***
### VSCode configuration:
Change path where needed, these files are located under the `.vscode`-folder in this repository but I show the content here for clarity, you don't have to copy-paste if you clone or download them from this repository, just change to your board, your COM-port and your PATH.

`settings.json`
    
    {
        "arduino.enableUSBDetection": true,
        "arduino.logLevel": "verbose",
        "arduino.path": "C:/Bin",
        "arduino.commandPath": "arduino-cli.exe",
        "arduino.useArduinoCli": true,
        "arduino.disableIntelliSenseAutoGen": true,
        "arduino.defaultBaudRate": 115200
    }
    
***    
    
`arduino.json`

    {
        "configuration": "FlashFreq=40,UploadSpeed=115200,DebugLevel=none",
        "board": "esp32:esp32:esp32doit-devkit-v1",
        "sketch": "esp32-multitask-blink-example.ino",
        "port": "COM4",
        "output": "build"
    }

***

`c_cpp_properties.json`
    
    {
        "configurations": [
            {
                "name": "ESP32",
                "includePath": [
                    "${workspaceFolder}/**",
                    "C:/Users/Jorgen/AppData/Local/Arduino15/packages/esp32/hardware/esp32/1.0.6/**"
                ],
                "defines": [
                    "_DEBUG",
                    "UNICODE",
                    "_UNICODE"
                ],
                "compilerPath": "C:/Users/Jorgen/AppData/Local/Arduino15/packages/esp32/tools/xtensa-esp32-elf-gcc/1.22.0-97-gc752ad5-5.2.0/bin/xtensa-esp32-elf-g++",
                "cStandard": "c11",
                "cppStandard": "gnu++11",
                "intelliSenseMode": "gcc-x86"
            }
        ],
        "version": 4
    }
    
***

<br />

If you got everything configured right you should be able to `CTRL`-click on `Arduino.h` and VSCode will take you there:

<br />

![VSCode_screenshot_pic2](https://user-images.githubusercontent.com/1673918/214077814-a9b102e9-f8b4-4e04-80e1-0f4865920751.jpg)

***

![VSCode_screenshot_pic1](https://user-images.githubusercontent.com/1673918/214077575-0687077c-f12d-47dc-9f40-a6748afeb2e9.jpg)
