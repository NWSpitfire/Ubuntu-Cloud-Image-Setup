# Ubuntu Cloud Image Setup
 Quick start guide for deploying Ubuntu Server Cloud Images on ESXI

 ---- INSTRUCTIONS ----

1) Deploy .ova in ESXI
2) Load seed.iso into the virtual CD Drive and connect to VM
3) Boot VM
4) Login with creds; user1 - amazon

-- Set root password and VM Hostname --

5) Switch to root with - sudo -i -
6) Set root password - passwd root -

[optional]

7) Add new user with non-root privellages and sudo rights - adduser EXAMPLEUSER - 
8) Add new user to the sudo group - usermod -aG sudo EXAMPLEUSER - 

9) Set new device hostname (default is amazonlinux) - hostnamectl set-hostname NEW-HOSTNAME

-- Commit changes and reboot server --

10) Remove disk from virtual CD Drive
11) The OS will lock the CD Drive as it is being used so force unmount will have to be used.
12) Reboot VM either through reboot button on ESXI or through - sudo reboot -

-- Fix SSH to allow connections and not fail on Public KEY --

[Untested] 

13) Change ownership and directory permissions for authorized keys - sudo chmod 700 ~/.ssh sudo chmod 600 authorized_keys -

[Currently used - easy but somewhat insecure]

14) Edit SSH Configurations - sudo nano /etc/ssh/sshd_config - 
15) Uncomment and change [#PermitRootLogin prohibit-password] to [PermitRootLogin yes]
16) Uncomment [PasswordAuthentication yes]
17) Comment out [PubkeyAuthentication yes]
18) Uncomment [PasswordAuthentication yes]
19) To add minimal extra security uncomment [MaxAuthTries 6] and change to [MaxAuthTries 1]
20) Restart sshd service - sudo systemctl restart sshd.service -





--- LINKS ---

Seed.iso (created by AWS for Amazon Linux 2 but works on Ubuntu CI);
https://cdn.amazonlinux.com/os-images/2.0.20190612/Seed.iso


Ubuntu Cloud Images (from 10.04 up until lates release server builds);
https://cloud-images.ubuntu.com/releases/