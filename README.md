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

### Prerequisites

* Download and install Visual Studio Code
* Download and install `arduino-cli` (pre-built binary)<br /> 
  https://arduino.github.io/arduino-cli/0.21/installation/#latest-release
* Set the PATH to the folder where `arduino-cli` is located (`arduino-cli.exe` on Windows).
* Install/Activate the Extension: Arduino for Visual Studio Code.

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
    
    C:\>arduino-cli sketch new esp32-multitask-blink-example
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
