# peanuts

Setup of a light-weight raspbery pi nas.

## The idea

This project is inspired by the reddit posts [[1]](https://www.reddit.com/r/raspberry_pi/comments/d1hmop/made_a_raspberry_pi_4_nas_automated_download/)[[2]](https://www.reddit.com/r/raspberry_pi/comments/kdy806/my_pinas_is_growing/) by user [u/Albert_street](https://www.reddit.com/user/Albert_street) where a raspbery pi 4 is connected to a USB hub and many external drives are attached to the USB hub. The hub powers the drives, and the pi has relatively quick read/write via the USB3 ports. This repo aims create something similar using ansible scripts.

## Secure your Raspberry Pi

First things first secure your raspberry pi. You can use the ansible playbooks from [Securing-your-Raspberry-Pi-with-Ansible](https://github.com/tomgelbling/Securing-your-Raspberry-Pi-with-Ansible) repo. This repo automates the [offical security guidance](https://www.raspberrypi.org/documentation/configuration/security.md) which you can do manually if you like.


# Dependencies

```
ansible-galaxy collection install ansible.posix
```

# Disks

Run this to see the disks labels and update vars.yml

```
lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```