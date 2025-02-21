Create a .txt file with a list of Grow dashboards URL's for the host Pi
Name it accordingly

Upload to Git


Create a dashboard.sh file:

Open a terminal

sudo mdir Dolphin # create in terminal in home folder #

sudo nano /home/Dolphin/dashboard.sh


Save this script to the file:

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
sed -i 's/"exited_cleanly":false/"exited_cleanly":true/' #/home/Dolphin/dashboard.sh/home/Dolphin/.config/chromium/Default/Preferences
sed -i 's/"exit_type":"Crashed"/"exit_type":"Normal"/' /home/Dolphin/.config/chromium/Default/Preferences

# Launch Chromium 
/usr/bin/chromium-browser \
  --start-fullscreen \
  --no-first-run \
  --noerrdialogs \
  --disable-infobars \
  $(curl -s "https://raw.githubusercontent.com/${ORG}/${REPO}/${BRANCH}/${DASHBOARD}") &


Make this script executable by anyone:

sudo chmod a+x /home/Dolphin/dashboard.sh

Go to Google extensions and install TabCarousel. Set to AutoStart and set delay to 30000

To run from Terminal:

/home/Dolphin/dashboard.sh

