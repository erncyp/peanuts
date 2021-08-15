# peanuts

Light-weight raspbery pi nas

*This repo is still in development.* Feel free to contribute. See the [roadmap](ROADMAP.md) for what has been done and what is yet to be done.

## The idea

This project is inspired by the reddit posts [[1]](https://www.reddit.com/r/raspberry_pi/comments/d1hmop/made_a_raspberry_pi_4_nas_automated_download/)[[2]](https://www.reddit.com/r/raspberry_pi/comments/kdy806/my_pinas_is_growing/) by user [u/Albert_street](https://www.reddit.com/user/Albert_street) where a raspbery pi 4 is connected to a USB hub and many external drives are attached to the USB hub. The hub powers the drives, and the pi has relatively quick read/write via the USB3 ports. This repo aims create something similar using ansible scripts.

![peanuts physical setup](docs/peanuts.png)


## Installation


First off, lets start with a fresh install of raspian. I am going with raspian lite, which is headless. The raspbery pi website gives loads of instructions how to do this. I am using their "raspbery pi imager" for this job.


(optional) I am running my pi headless. To enable ssh access straight away, you need to create an empty file called ssh in the boot partition.


### (optional)Secure your Raspberry Pi

First things first secure your raspberry pi. You can use the ansible playbooks from [Securing-your-Raspberry-Pi-with-Ansible](https://github.com/tomgelbling/Securing-your-Raspberry-Pi-with-Ansible) repo. This repo automates the [offical security guidance](https://www.raspberrypi.org/documentation/configuration/security.md) which you can do manually if you like.


### Dependencies

Install ansible dependencies with

```
ansible-galaxy collection install ansible.posix
```


## Create vars.yml

Copy the example over so we can start populating it:

```
cp vars/vars.yml.example vars/vars.yml
```

This file has two sections. The first section contains the information on which drives to mount, and the second section contains information on which drives to join up using mergerfs.

We need to know the labels of the disks we want to mount. To do this, ssh onto your pi and run this to see the disks labels and fstype.

```
lsblk -o NAME,FSTYPE,SIZE,MOUNTPOINT,LABEL
```

Note that in the example, we name one drive with the prefix `pd-` for parity drive. Snapraid requires at least one parity drive and two data drives. In mergerfs, we merge only the data drives, not the parity one. Snapraid requires that the parity should be as large as the largest drive in the pool.

