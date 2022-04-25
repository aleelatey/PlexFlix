This is the record of my attempt to create a fully portable Plex install

## Purpose:
  Create a portable Plex server that can be accessed by various client devices where Internet is not available. 
  
## Why?
  Why use this instead of miniDLNA? I want the Plex interface.
  
## Assumptions:
   You have prior experience with Plex, Linux and networking.
   
   I am documenting this for my own use and sharing it in the hope it is of value to others.
   
   The Plex libraries will be a subset of existing libraries and the files are already correctly formatted for the server.
  
## Equipment
  * Raspberry Pi 3B
  * Case with external SATA interface and power button
  * 2.5" external HDD
  * Power source
  * Internet connection for setup and testing
  
## Method
  * Set up Raspberry Pi as access point
  * Add Plex server

# Instructions
   ### Wireless access point instructions
   
   I tried a few work instructions with limited success. The instructions here are the only ones that worked:
       
   ~~https://learn.sparkfun.com/tutorials/setting-up-a-raspberry-pi-3-as-an-access-point/all~~
   https://pimylifeup.com/raspberry-pi-wireless-access-point/comment-page-1/
       
   ### Plex server
   #### Installation
   Use these instructions:
        https://pimylifeup.com/raspberry-pi-plex-server/
          Stop after the instalation instructions.
          Static IP is not needed.
        
   #### Before creating the libraries:
   Create folders on the external hard drive (ony create the folders you will be using)
             Videos/
                TV
                Movies
                Family
                Photos
           Add some content to the folders. And a couple of items for testing. You can add more later.
           Change these Settings:
              DLNA - enable
              Agents - under all the options, move Loval Media Assets to the bottom of all the agent lists
              Network - disable IPV6 support
                      - add this to "List of IP address allowed access without auth" changing the IP addresses to your LAN and the AP you created earlier
                        192.168.1.1/255.255.255.0,192.168.2.1/255.255.255.0
              Users and Sharing - enable Guest
         #### Create libraries
            Create the libraries you require for your share. Plex will automaticaly start scanning.
            
   I have not moved the database so there are a few optional setting to change if your SD card is less than 32gb.
            
   Turn off all the options for trailers and video previews under Libraries / Setting / Advanced.
            
   Share the libraries with the Guest user.
       
   You should be able to access the libraries through the LAN address and via the wifi connection.
      
   ## To do...
   - [ ] Add captive portal software to simplify connecting to the unit
   - [ ] Add file sharing - books, etc
   - [ ] Duplicate Wikipedia locally
   - [ ] Automatic updates from USB stick
      
            
 
           
          
## Issues:

#### Hostapd not starting...
```
>sudo service hostapd status
returns hostapd is masked. Run these commands
>sudo systemctl unmask hostapd
>sudo systemctl enable hostapd
>sudo systemctl start hostapd
```       
