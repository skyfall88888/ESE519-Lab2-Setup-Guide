# ESE519-Lab2-Setup-Guide

by Yu Feng, on Oct 10 2022

Setup up environment: 2018 Macbook Pro 15-inch, MacOS Monterey 12.4

Goal: Setup this Mac for RP2040 development using C/C++ SDK, test compiling and running example codes with RP2040 board.

### References:

1. RP2040 Datasheet

          https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf

2. Pico SDK Datasheet

          https://datasheets.raspberrypi.com/pico/raspberry-pi-pico-c-sdk.pdf

3. Pico C/C++ SDK

          https://github.com/raspberrypi/pico-sdk
          
4. Pico C/C++ SDK Examples

          https://github.com/raspberrypi/pico-examples
          
5. Getting started with Raspberry Pi Pico

          https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf

### Procedures:

1. Building RP2040 on Apple macOS, reference 5 section 9.1

    a. Install Homebrew
          
             Install from website: https://brew.sh/
              
    b. After installation, run necessary configuration: 
          
              $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
              
    c. Install Toolchain
         
              $ brew install cmake
              $ brew tap ArmMbed/homebrew-formulae
              $ brew install arm-none-eabi-gcc
              
2. Setup SDK, reference 5 section 2.1

    a. Setup pico repository
    
              $ cd ~/
              $ mkdir pico
              $ cd pico
              
    b. Clone pico-sdk and pico-examples git repositories
    
              $ git clone -b master https://github.com/raspberrypi/pico-sdk.git
              $ cd pico-sdk
              $ git submodule update --init
              $ cd ..
              $ git clone -b master https://github.com/raspberrypi/pico-examples.git
              
     c. !!!Caution: Skip 2.2 'Install the Toolchain' 
     
     d. Updating the SDK
     
              $ cd pico-sdk
              $ git pull
              $ git submodule update
             
3. Example Code Setup

  Since the Blinking an LED in C example will not work with RP2040 because of the nature of the chip, the hello world example will be executed. However,     basic setup should be configured. 
  
  Setup code-running configurations from reference 5 section 3.1

   a. Create build directory
   
              $ cd pico-examples
              $ mkdir build
              $ cd build
              
   b. Setup PICO_SDK_PATH
   
              $ export PICO_SDK_PATH=/home/pi/pico/pico-sdk
              
   c. Prepare cmake build directory
   
              $ cmake ..
              
              The last line back from the terminal is: 'Build files have been written to:/Users/yourdirectoryofchoice/pico/pico-examples/hello_world'
              
   Now the basic configurations have been completed, ready to run example codes for hello_world
   
   Navigate to Reference 5 Section 4.2:
   
   d. make the hello_world directory
   
              $ cd hello_world
              $ make -j4
              
              The terminal will start from 0% ----- 100%. The last line back from the terminal is: 'Built target pio_ir_loopback'
              
  Four files have been built into two seperate examples programs. Respectively, hello_world/serial/ and hello_world/usb/ directories.
              
  • serial/hello_serial.elf, which is used by the debugger
  • serial/hello_serial.uf2, which can be dragged onto the RP2040 USB Mass Storage Device (UART serial binary)
  • usb/hello_usb.elf, which is used by the debugger
  • usb/hello_usb.uf2, which can be dragged onto the RP2040 USB Mass Storage Device (USB serial binary)
              
 4. View 'hello world' text on console

    To see the result of the example code on PC, minicom should be installed.
    
    a. Install minicom through Homebrew
    
               $ Brew install minicom
               
    b. Run minicom command to open minico console
    
               $ minicom -b 115299 -o -D /dev/tty.usbmodem*
               
5. Run hello_world Code

    Resetting the RP2040 using the two buttons.
    
    Then drag one of the uf2 file mentioned above onto the usb-drive icon.
    
6. Hello World displayed on console!

<img width="962" alt="Screen Shot 2022-10-10 at 12 24 15 PM" src="https://user-images.githubusercontent.com/95589555/194929276-cc7ee274-8f01-4583-b440-ddb269b66354.png">

              
            
            
