# Initial Setup

First off, lets start with a fresh install of raspian. I am going with raspian lite, which is headless. The raspbery pi website gives loads of instructions how to do this. I am using their "raspbery pi imager" for this job.

## SSH

We will need ssh access to our raspbery. See (here)[https://www.raspberrypi.org/documentation/remote-access/ssh/README.md] for how its done. Essentially, you drop an empty `ssh` file in the microsd card, and thats a signal for raspbery pi to expose ssh.

Find the ip address of your raspbery pi by logging into your router. Log into your raspbery pi by

```
ssh pi@<IP-ADDRESS>
```
You should be able to log into your raspber pi! Make a note of this ip address and add it to ansible hosts file:

```
sudo vim /etc/ansible/hosts
```

## Securing your raspbery pi

I would reccomend moving away from username/password to ssh key based authentication.

```
ssh-copy-id pi@<IP-ADDRESS>
```

From this point onwards, we should do everything with the ansible scripts provided.



