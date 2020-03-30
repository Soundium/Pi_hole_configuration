               
## How-to: Pi-Hole Plus DNSCrypt Setup on Raspberry Pi 4 
          
Follow my instructions and make your setup **trouble-free!**
                
Want to report any issue? Feel free to file an <a href="https://github.com/Soundium/Pi_hole_configuration/issues">issue</a>.
***
### My hardware
***
### Raspberry Pi 4 Installation


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

