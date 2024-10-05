Create a dashboard.sh file:

sudo nano /home/pi/dashboard.sh
Save this script to the file:

#!/bin/bash

# config options
export ORG=DolphinSolutionsLtd
export REPO=dashboards
export BRANCH=main
export DASHBOARD=DEP001.txt

# don't let this display sleep
export DISPLAY=:0.0
xset s noblank
xset s off
xset -dpms

# hide mouse pointer
unclutter -idle 0.5 -root &

# trick Chromium into believing it shut down successfully last time
sed -i 's/"exited_cleanly":false/"exited_cleanly":true/' /home/Dolphin/.config/chromium/Default/Preferences
sed -i 's/"exit_type":"Crashed"/"exit_type":"Normal"/' /home/Dolphin/.config/chromium/Default/Preferences

# Launch Chromium 
/usr/bin/chromium-browser \
  --start-fullscreen \
  --no-first-run \
  --noerrdialogs \
  --disable-infobars \
  $(curl -s "https://raw.githubusercontent.com/${ORG}/${REPO}/${BRANCH}/${DASHBOARD}") &
