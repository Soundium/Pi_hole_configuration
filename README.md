               
## How-to: Pi-Hole Plus DNSCrypt Setup on Raspberry Pi 4 
          
Follow my instructions and make your setup **trouble-free!**
                
Want to report any issue? Feel free to file an <a href="https://github.com/Soundium/Pi_hole_configuration/issues">issue</a>.
***
### My hardware
- <a href="https://www.raspberrypi.org/products/raspberry-pi-4-model-b/">Raspberry Pi 4 Computer Modell B, 4GB RAM</a>
- <a href="https://www.raspberrypi.org/products/poe-hat/">Power over Ethernet (PoE) HAT for Raspberry Pi 4 & 3B+, Rev. 1.01</a>
- <a href="https://www.amazon.de/SanDisk-SDSQXCG-032G-GN6MA-Extreme-Adapter-Schwarz/dp/B06XYHN68L">SanDisk Extreme Pro microSDHC A1 UHS-I U3 Card + Adapter 32GB</a>
- <a href="https://www.jacob.de/produkte/aluminium-gehaeuse-fuer-rpi4-aluc-si-artnr-6009241.html">Aluminium Gehäuse für Raspberry Pi 4 Modell B, silber</a>

### Important informaiton
The Raspberry Pi uses an SD card for local storage, and as such, it's essential to be smart about the SD card you use. I suggest at least a 32GB card, and for a few more dollars, you can get a high endurance or extreme pro card. I like the SanDisk Extreme Pro 32GB micro SDHC card for $12. You won't need the full 32GB of storage, but this allows for additional write locations that can further extend the life of the card. 

***
### Raspberry Pi 4 Installation

 1. Download the latest version of <a href="https://www.raspberrypi.org/downloads/raspbian/">Raspbian Buster with desktop and recommended software</a>. Do NOT unzip it.

2. Download and install <a href="https://www.balena.io/etcher/">Etcher.io</a>, which we will use to write the Raspbian Buster image to the SD card. There are both PC and Mac versions.

3. Connect your card reader and insert the microSD card. Warning: contents will be overwritten!

4. Start Etcher, click "Select Image" and find the Raspbian Lite zip file you downloaded.

5. Click "Flash!" and wait for the zip to be written to the memory card and the validation to complete. If an error occurs, make sure the card reader/card is not locked. If it's not locked, possibly the download is corrupted or not complete. Try and re-download the Raspbian Buster zip. 

**Note:** If you are doing this on a Windows computer, you may get a pop-up about needing to format a drive. This is erroneous, dismiss it and click Cancel.

7. There is a small Fat32 partition in which we need to create a zero byte file called ssh. 
  - **On Windows**, open a command prompt, CD to the Fat32 partition and enter the following command (ignore the output error..that is expected). If you don't see a drive letter associated with the Fat32 partition, open Disk Manager and assign it a letter. Enter:

```
.>ssh
```

- **On a Mac computer** CD to the Fat32 partition (e.g. cd /Volumes/boot) and type: **touch ssh**

9. Cleanly unmount the microSD card. Yes, don't pull it out! Insert the microSD card into the Raspberry Pi. 

10. Connect your Raspberry Pi to a suitable power source. Since there's no power switch, it will start to immediately boot. 

- If you have a monitor and keyboard attached when booting the first time, a helpful GUI wizard will appear to walk you through the configuration of items such as locale, keyboard, timezone, new password, software updates, etc. 

- If you are doing the setup 'headless', wait a couple of minutes for the system to boot. Using a network scanning app find your "Raspberry Pi" IP. Or if you get lucky, you can open a terminal and type **ping raspberry.pi** and see if it responds.


### Whitelist script Installation
1. Download
```
cd /opt/
sudo git clone https://github.com/Soundium/Pi_hole_Whitelist.git
```
2. Make the script to run the script at 1AM every day.

`sudo nano /etc/crontab`

Add this line at the end of the file:       
`0 1 * * *   root    /opt/Pi_hole_Whitelist/scripts/whitelist.sh`

CTRL + X then Y and Enter

3. First run
```
sudo /opt/Pi_hole_Whitelist/scripts/whitelist.sh
```         
### Youtube blocker script Installation

1. Register on <a href="https://www.wolframalpha.com/">Wolfram Alpha</a> and get your APPID. 
2. Download scripts.
```
cd /opt/
git clone https://github.com/Soundium/Pi_hole_youtube_blocklist.git
cd Pi_hole_youtube_blocklist/scripts
```
3. Add your APPID to temp.sh. 
```
sudo nano /opt/Pi_hole_youtube_blocklist/scripts/temp.sh
```
```
# Wolfram Alfa APPID
APPID="Register on https://www.wolframalpha.com/ and put your APPID here"
```
CTRL + X then Y and Enter

4. Give the rights.
```
sudo chmod +x /opt/Pi_hole_youtube_blocklist/scripts/temp.sh
```
5. Add scripts to crontab to run at 1 AM and 5 AM every day.

`sudo nano /etc/crontab`

Add those lines at the end of the file:       
`0 1 * * *      root    /opt/Pi_hole_youtube_blocklist/scripts/temp.sh`

`0 5 * * *      root    /opt/Pi_hole_youtube_blocklist/scripts/youtube-ads.sh`

CTRL + X then Y and Enter

6. First run
```
sudo Pi_hole_youtube_blocklist/scripts/temp.sh
sudo Pi_hole_youtube_blocklist/scripts/youtube-ads.sh
```
7. Add http://localhost/youtube.txt as blacklist from local to Pi-hole setup.

Happy Adblocking :-)
   
***     

### Donation
All donations are welcome and will help me to maintain this project. Please use "**Sponsor**" button on the top of this page.

***
### License
```
MIT License

Copyright (c) 2020 Soundium

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

