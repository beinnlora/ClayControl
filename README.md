# ClayControl
Sporting Clay controller
Wireless Sporting Clay Trap Controller 

#Introduction
This project describes a Wifi controller for triggering Clay Pigeon traps from a web interface e.g. mobile phone.

It allows any number of clay traps to be controlled via e.g. a smartphone or tablet. 
Sequences of clays can be recorded, played back, paused, recorded and loaded as required.
Random sequences of clays can be created based on a user's required number of traps, number of clays, and average delay inbetween clays.

#Technical Overview
A Raspberry Pi serves as a wifi hotspot and captive portal, presenting connected users with a web interface for controlling the trap sequence.
Websockets is used to pass control commands from any connected device to the control software.

Traps are triggered via a relay board, or optionally an RF interface to wireless receivers.

#Software

The Raspberry pi controller is made up of four components: 
##Webpage interface
A Javascript enabled webpage is served to connected clients. Javascript passes events to and from the Pi via websockets. 
The webpage is made responsive via JQueryMobile so the UI can fit any device - smartphone, tablet or computer.
Tornado serves

##Python Control code
A python script loads on startup, that spawns a websocket listener via Tornado. This code controls the application logic, generation of sequences, loading and saving of sequences etc.

##Wifi hotspot
The Raspberry Pi acts as a wifi hotspot, DNS and DHCP server. The Pi is configured as a captive portal, so all web requests of connected clients redirect to the web interface
  *hostapd
  *dnsmasq as dhcp and dns

##Startup scripts
These are run at rc.local, and control the sequencing of 

The raspberry pi and USB flash drive are mounted read-only, to prevent corruption from power supply interruptions


#Hardware
##Raspberry Pi 3 
Built-in wifi could be used, but a USB device offers greater range through external antenna.
##USB Wifi dongle
High power, external antenna, drivers available for hostapd
##Relay Board
Generic TTL-triggered relay board
##Power Supply
A typical ebay 12v-5v DC-DC power supply feeds the PI and the relay board. 
##USB flash drive
Provides storage for user config files; allowing the SD card to remain mounted RO at all times to help prevent corruption.
Gives the option of transferring trap sequence save files between controllers.
##Radio Control.
Option to trigger radio trap releases, negating the need for physical connection to each trap.



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
    
    
    This p
