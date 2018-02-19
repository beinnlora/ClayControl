# ClayControl
Sporting Flush Clay Target smartphone / wifi controller.


## Introduction
This project describes a Raspberry Pi based smartphone controller for triggering Clay Pigeon traps and flush sequences from a web interface e.g. mobile phone.

It allows any number of clay traps to be controlled via e.g. a smartphone or tablet. 

Sequences (flushes) of clays can be recorded, played back, paused, saved and loaded as required.

Random sequences of clays can be created based on a user's required number of traps, number of clays, and average delay inbetween clays.

Since the interface is web based, it doe not require an App download or external internet connection. Any 'smart' device that has wifi and a browser that supports websockets (Android/iOS) can be used as a controller. Multiple devices can connect to the controller to observe progress through a flush sequence.

## Features:
  * Control any number of traps (up to the limit of how many relays you want to connect to the Pi). We have tried 10 traps with success.
  * Turn any 'smart' phone or tablet into a trap remote control- any device with wifi and a browser can act as your clay controller.
  * Record and playback flush sequences at the touch of a button.
  * Save your favourite flush sequences to USB drive, and load them up any time at the click of a button.
  * Generate random flush sequences: you decide which traps, how many clays, and the average target presentation rate.
  * Live view of clays remaining, time remaining in sequence, which trap is next, how many clays left from each trap etc.

## Installation/Construction
See the individual INSTALL-HARDWARE and  INSTALL-SOFTWARE and  for construction and configuration notes.

## Technical Overview
A Raspberry Pi serves as a wifi hotspot and captive portal, presenting connected users with a web interface for controlling the trap sequence.

Websockets is used to pass control commands from any connected device to the control software.

Traps are triggered via a relay board, or optionally an RF interface to wireless receivers.

### Software
The Raspberry pi controller is made up of four components: 

#### Webpage interface
A Javascript enabled webpage is served to connected clients via Apache running on the Pi. Javascript in the client browser passes events (button presses, clay counters, time remaining etc) to and from the Pi via websockets. 

The webpage layout is made responsive via JQueryMobile so the UI can fit any device - smartphone, tablet or computer.

A websockets interface is instantiated via Tornado on the Pi to pass messages between browser and Python control code.

#### Python Control code
A python script loads on startup, that spawns a websocket listener via Tornado. This code controls the application logic, generation of sequences, loading and saving of sequences etc.

#### Wifi hotspot
The Raspberry Pi acts as a wifi hotspot, DNS and DHCP server. The Pi is configured as a captive portal, so all http requests of connected clients redirect to the web interface
  * hostapd
  * ics-dhcpd-server

#### Startup scripts
These are run at rc.local, and control the sequencing of configuring the Wifi access point, DNS/DHCP, and python code.

#### File systems
The raspberry pi SD card and USB flash drive are mounted read-only, to prevent corruption from power supply interruptions. Only when saving flush sequences to the USB drive is this momentarily mounted r/w. 


### Hardware
#### Raspberry Pi 3 
Built-in wifi could be used, but a USB device offers greater range through external antenna.
#### USB Wifi dongle
High power, external antenna, drivers available for hostapd
#### Relay Board
Generic TTL-triggered relay board
#### Power Supply
A typical ebay 12v-5v DC-DC power supply feeds the PI and the relay board. 
#### USB flash drive
Provides storage for user config files; allowing the SD card to remain mounted RO at all times to help prevent corruption.
Gives the option of transferring trap sequence save files between controllers.
#### Radio Control.
Option to trigger radio trap releases, negating the need for physical connection to each trap.
#### Enclosure
A suitable box, e.g. 200x100x100 IP68 box with cable glands going out to your 


    Copyright (C) 2016 2017 2018 Stephen Wilson

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation version 3 of the License.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.
    
    
    
