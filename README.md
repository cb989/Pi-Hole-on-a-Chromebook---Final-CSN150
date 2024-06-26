# Pi-Hole-on-a-Chromebook---Final-CSN150
## Rundown of everything:
For anyone that knows me well, they know that I have three passions. Tech, video games, and repurposing old hardware! What better chance to repurpose my old stinky chromebook than now? Feast your eyes upon an amazing project called "chrultrabook" that i found while scrolling through youtube one night. What chrultrabook allows you to do, is to reflash the original INCREDIBLY limting uefi firmware normally present on chromeOS devices, and replace it with another firmware called coreboot. This custom firmware allows you to install any operating system under the sun and with this power I decided to insatll Ubuntu server, download docker, and finally install Pi-Hole, the amaing network wide adblocker.
## So, why Pi-Hole?
I firmly believe that one of the most important security tools to have in your aresenal, is a good adblocker. There are thousands of malicious advertisements out there on the web, and adblocking is just a great tool to get rid of most of them all together. Now look, most young people are often savvy enough to skip out on clicking that weird download button, but my mother on the otherhand is not. I loved the idea of being able to improve the overall security of every single device all at once, particularly to help protect my family members who arent as tech savvy while they're surfing the web.

## Name of Project:
Pi-Hole on a chromebook
### Equipment needed:
1. The chromebook itself
2. Sandisk USB Flash drive (that I had laying around)
3. [USB to Ethernet Adapter](https://www.amazon.com/USB-Ethernet-Adapter-Gigabit-Switch/dp/B09GRL3VCN/ref=sr_1_4?crid=30CWKI378JWHR&dib=eyJ2IjoiMSJ9.QCN-6MlAIK3XarnN3gP4fLbrMEAm52ww8ZoRwiIWI4saSq457syxb6VuKhrTKz_w0lEv1nZBh5tP8HAJrBxvmuV4a5rTTm7YsEr4yF2r0Q2M-anX1NXQPOUMzdsk8lwA_sdDtz0tliGR87IyIPwLnO-WjX5a1VDSIgU1OH3eHJDzFNLU-EVxinkDl53n8UjhiqIJeFYUdnsAFtKyXVQaPYXRkkEidw0SfwnKNAMRKMk.rghjz-2dPzFUxpbcGNH-HBJudSpe3xKmQbk7CUXLKj4&dib_tag=se&keywords=usb%2Bto%2Bethernet%2Badapter&qid=1715213440&sprefix=usb%2Bto%2Bthern%2Caps%2C157&sr=8-4&th=1)
### Links to Documentation that I used in order of use:
1. [Chrultrabook Docs](https://docs.chrultrabook.com/)
2. [Disable Write-Protect Screw on Samsung Chromebook 3 CELES](https://maxwyb.github.io/linux/2016/11/05/chromebook-write-protection.html)
3. [How to setup static IP on Ubuntu linux](https://www.freecodecamp.org/news/setting-a-static-ip-in-ubuntu-linux-ip-address-tutorial/)
4. [Running Pi-Hole in Docker](https://github.com/pi-hole/docker-pi-hole/#running-pi-hole-docker)
### Here are the steps I took in order to flash coreboot on my chromebook, install Debian, run Docker, and finally, install Pi-Hole!
1. Following the chrultrabook documentation I refrenced earlier, I first looked to find the exact version of chromebook that I had: The Samsung Chromebook 3.
2. I then had to enable developer mode by booting the chromebook up into recovery mode, hitting Ctrl + D, and then pressing enter. 
3. Now that I knew which version of chromebook I had, I researched how to disable write protection on my specific chromebook model. Following this [guide](https://maxwyb.github.io/linux/2016/11/05/chromebook-write-protection.html) I linked up above, I opened the laptop up, and simply removed the screw that enabled the write protection. Here is a picture of the location of that screw that I took myself:
4. Now, lets flash the firmware. I turned on the chromebook and entered the VT-2 command shell on the chromebook by tapping Ctrl + Alt + F2 on the keyboard. Copied and pasted this command to run the firmware installation script:
   * cd; curl -LO mrchromebox.tech/firmware-util.sh && sudo bash firmware-util.sh
5. Finally coreboot has been flashed onto the chromebook and I can get onto installig Ubuntu Server! I downloaded a Ubuntu ISO from their official download mirror, burned the ISO to my USB flash drive, and I went on to change the boot order and install the operating system.
6. While installing Ubuntu server, you have the option to install docker as you install the operating system, so of course I went ahead and did that to make my life easier.
7. After finishing the instalation, I had to first make my chromebooks ip address static. To do this I simply had to edit the file named interfaces located at /etc/networks, change the interface from dhcp to static, and add my preferred IP address, subnet mask, and dns servers there.
8. Finally, lets startup a container to install Pi-Hole! All I had to do now is copy Pi-Hole's docker compose.yml onto my chromebook by using ssh on my main laptop, changing the defualt password located in the text file, saving the edit on vim by using the command :w, and finally, running the command
   * docker compose up -d
## Finally, I have Pi-Hole installed on a strange device!
Using my favorite web browser, all i had to do was paste the the IP address of the chromebook, login as admin and the beauty of pi-hole was right underneath my finger tips! 
### Issues Faced:
Surprisingly, I had faced only one issue throughout this entire process and it was incredibly easy to fix. When I first attempted to access the Pi-Hole web interface, it didn't connect at all. I went back to check the docker compose file to see if any issues were present in the startup config, and yeah, I forgot to change the timezone from "America/Chicago" to "America/New_York". Apparently timezones are very important when it comes to setting up docker containers which use web interfaces!  While it did take me a while to complete this entire installation process (around a full day), I got it up and running with no errors thanks to the fantastic documentation I refrenced earlier in my links section.

## Thank you for reading this Prof. Have a great day!
