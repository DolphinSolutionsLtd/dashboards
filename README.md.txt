## Get Grow Dashboard URL's. Ensure they are in the below format:
## https://app.gogrow.com/dashboard/share/c57cff6a529a23c023f54fe6ab060e16 (must NOT have the words "share token" in the URL)
## Create a .txt file with a list of Grow dashboards URL's for the host Pi on your PC
## Name it accordingly
## Upload .txt file to Git - https://github.com/login
## UN : rpiconnectsvcaccount@dolphinsolutions.co.uk - PW in Dashlane
## Add any new approved dashboard URL's to the MASTER DASHBOARD LIST.txt file with the name of the dashboard at the end as below:
## https://app.gogrow.com/dashboard/share/c57cff6a529a23c023f54fe6ab060e16 - MSI's
## Connect to the respective Pi using Pi Connect - https://connect.raspberrypi.com/devices - PW in Dashlane
## UN : rpiconnectsvcaccount@dolphinsolutions.co.uk - PW in Dashlane
## Open a terminal to create a folder for the dashboard.sh file
 
sudo mkdir Dolphin
 
## Create the dashboard.sh file
 
sudo nano /home/admin/Dolphin/dashboard.sh
 
## Save the script below (everything between the "line breaks") to the file:
 
-------------------------------------------------------------------------------------------------------------
 
#!/bin/bash
 
# config options - Rename the DASHBOARD= .txt file to the one you want to run on the Pi

export ORG=DolphinSolutionsLtd

export REPO=dashboards

export BRANCH=main

export DASHBOARD=Global_2025.txt
 
# don't let this display sleep

export DISPLAY=:0.0

xset s noblank

xset s off

xset -dpms
 
# hide mouse pointer

unclutter -idle 0.5 -root &
 
# trick Chromium into believing it shut down successfully last time

sed -i 's/"exited_cleanly":false/"exited_cleanly":true/' #/home/admin/Dolphin/dashboard.sh/home/admin/Dolphin/.config/chromium/Default/Preferences

sed -i 's/"exit_type":"Crashed"/"exit_type":"Normal"/' /home/admin/Dolphin/.config/chromium/Default/Preferences
 
# Launch Chromium 

/usr/bin/chromium-browser \

  --start-fullscreen \

  --no-first-run \

  --noerrdialogs \

  --disable-infobars \

  $(curl -s "https://raw.githubusercontent.com/${ORG}/${REPO}/${BRANCH}/${DASHBOARD}") &
 
---------------------------------------------------------------------------------------------------------------
 
 
## Make this script executable by anyone:
 
sudo chmod a+x /home/admin/Dolphin/dashboard.sh
 
## Go to Google extensions and install TabCarousel. Set to AutoStart and set delay to 30000
## To run from the Terminal:
 
/home/admin/Dolphin/dashboard.sh
 

 
