## Disable sleepmode

Instructions to do this from terminal on a Mac (as of Oct 2024)
(1) Download the standalone Android SDK Platform Tools package for Mac here: https://developer.android.com/tools/releases/platform-tools
(2) Open Terminal and run the following commands --
cd ~/Downloads/platform-tools

./adp connect [IP ADDRESS OF YOUR FIRESTICK] (you can usually find this out from the admin / control panel of your router)

./adp shell settings put system screen_off_timeout 2073600000

./adp shell settings put secure sleep_timeout 0

exit
