For Windows:
extract Vagrant.zip to your desktop (this file)
download and install gitbash: https://gitforwindows.org/
download and install virtualbox: https://www.virtualbox.org/wiki/Downloads
download and install vagrant: https://www.vagrantup.com/downloads
reboot

run gitbash

run the following commands (replace <your username> with your windows username)
cd Onedrive/desktop/Vagrant
    OR
cd Desktop/Vagrant
vagrant up

For Mac:
Open terminal
run the following commands:
cd ~/Desktop/Vagrant
vagrant up

Troubleshooting:
On Terminal OR Git Bash:
1) use 
    a) cd (change directory)
    b) ls (list)
    c) pwd (print working directoryu)
    d) to navigate to where your vagrant file is

In general:
1) reboot
2) disable antivirus
3
))
3) uninstall virtualbox and vagrant
    a) reboot
    b) reinstall
    c) reboot again

Windows:
4) hold ctrl+shift+escape to open task manager
    a) go to the Services tab
    b) find VDbox* and right click
    c) click start


USE
Username: 	sysadmin
Password: 	cybersecurity

VAGRANT COMMANDS
vagrant update (to update the machine)
vagrant prune (delete old or unused VMs)
vagrant destroy (USE WITH CAUTION - deletes everything)