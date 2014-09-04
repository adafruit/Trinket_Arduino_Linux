# Trinket Arduino IDE Configuration for Linux

Configuration files for modifying the official Arduino IDE to program 
Trinket/Pro Trinket/Gemma/Flora on Linux.

## Installation

1.  Switch to a branch of this repository with the same version as the Arduino
    IDE you will modify.  For example to clone this repository for Arduino 1.0.5
    in your home directory execute:
    
        cd ~
        git clone -b 1.0.5 https://github.com/adafruit/Trinket_Arduino_Linux.git

1.  Download the version of the Arduino IDE for Linux that matches the version
    number in the branch you cloned.  You can use either the 32-bit or 64-bit
    version of the Arduino IDE (depending on what your processor and OS support).
    
    See Arduino IDE downloads here: http://arduino.cc/en/main/software

    Then extract the contents of the Arduino IDE archive you downloaded and place
    it wherever you would like the IDE files to live permanently (such as your 
    home directory).

    For example to download the 64-bit version of Arduino 1.0.5 and extract it
    in your home directory execute:

        cd ~
        wget http://arduino.googlecode.com/files/arduino-1.0.5-linux64.tgz
        tar xvfz arduino-1.0.5-linux64.tgz

3.  Copy over the contents of the arduino-(version) directory from the
    Trinket__Arduino__Linux repository that was cloned in step 1 so it overwrites
    the files from the Arduino IDE downloaded in step 2.  Make sure all files
    in the GitHub repository _overwrite_ the files in the Arduino IDE!

    For example to copy the modified 1.0.5 configuration from step 1 over the 
    Arduino IDE downloaded in step 2 execute:

        cd ~
        cp -rf ./Trinket_Arduino_Linux/arduino-1.0.5/. ./arduino-1.0.5/.
    
    Be careful to copy the command above exactly!  The slashes and periods at the
    end of the paths are required to make the copy work as expected.

4.  Finally install the included adafruit-trinket.rules udev file to allow you
    to run the Arduino IDE and program over USB as a non-root user.  Note that
    this configuration is built for Ubuntu (12.04/14.04) but can likely be
    modified to work with other distributions by changing the GROUP="dialout"
    to a different group which identifies your non-root users.

    On Ubuntu copy the included adafruit-trinket.rules file to udev's 
    configuration folder by executing:

        cd ~
        sudo cp ./Trinket_Arduino_Linux/adafruit-trinket.rules /etc/udev/rules.d/

    Then reload udev's configuration by executing:

        sudo reload udev

5.  That's it!  Now run the downloaded and modified Arduino IDE and confirm the
    Trinket, Pro Trinket, Gemma, and Flora boards are listed in the Boards menu.

    *Make sure when programming Trinket, Pro Trinket, Gemma, or Flora boards that
    you change the programmer to "USBtinyISP" in the Tools->Programmer menu!*

    Try loading a simple blink example on your board.  Make sure you press the
    board's reset button and confirm the bootloader LED is pulsing before you
    press the upload button.

    *NOTE:* When programming the Trinket or Gemma, which are based on the ATtiny85
    processor, you might see errors such as the following during the upload:

        avrdude: error: usbtiny_receive: error sending control message: Protocol error (expected 4, got -71)

    These errors can be ignored and the upload should finish successfully.  In
    general uploads to the ATtiny85 boards are a little flakey with Linux's USB
    core so you might need to try the upload a few times before it works.
