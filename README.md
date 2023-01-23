# esp32-multitask-blink-example
FreeRTOS blink two LEDs example for the ESP32, FreeRTOS allows us to handle several tasks in parallel that run independently.

***

### Prerequisites

* Download and install Visual Studio Code
* Download and install `arduino-cli` (pre-built binary) https://arduino.github.io/arduino-cli/0.21/installation/#latest-release
* Set the PATH to the folder where arduino-cli is (arduino-cli.exe on Windows).
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
        
  
