# HW1 Report
Author: Steven Chen
Time: Aug. 28th, 2024


## SEED in Mac
Platform: Mac M3
System: Sonoma 14.4.1

### Pre-req
The setup.docx announce that the environment and setup should only be done in x86 platform, however, when I enter into the official website of [SEEDLAB](https://seedsecuritylabs.org/labsetup.html), it provides a newest [document](https://github.com/seed-labs/seed-labs/blob/master/lab-setup/apple-arm/seedvm-fusion.md) about how to set up an environment in Apple, so I think I can have a try based on the document.


### 1. Install Homebrew and docker
In fact, it is also no need for me to follow these instructions since I have had one months ago. Just follow the [document](https://github.com/seed-labs/seed-labs/blob/master/lab-setup/apple-arm/seedvm-fusion.md) in the github.

You should install homebrew in cli and remember to add it into the system environment. For Mac M, the default address of homebrew install is in `/opt`. And the easiest way I know is to add `:/opt/homebrew/bin` to your `.bash_profile`.

![alt text](<截屏2024-08-28 14.46.12.png>)

I meet an error when I run `brew install chipmk/tap/docker-mac-net-connect`. But we can jump this procedure first.

![alt text](<截屏2024-08-28 14.51.54.png>)

### 2. Install VMware Fusion
In fact, I don't need to install VMware Fusion since I already have one. After Broadcom owns VMware Company, it is always hard to access the download link about VMware Fusion though it is free to download now. 
[VMware Fusion Download Link](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware+Fusion)
Click the link and we need to register an account and apply for a license to free download. It always needs minutes to hours to wait for the account check.

![alt text](<截屏2024-08-28 14.28.53.png>)
Finally, you can find this page which means that you are allowed to download the software.

### 3. Create Virtual Machine
 (I won't provide procedure one by one since there is no need to talk about each procedure so detail.)
Download [Ubuntu22.04.3](https://cdimage.ubuntu.com/jammy/daily-live/current/) iso file.

Aftering downloading, open vmware fusion. 

Create a new Virtual Machine named SEED.  Just select disk or img and find the iso file you download and nothing special you need to configure.

And then click continue and finish button. Then a new virtual machine is created.

Open the Virtual machine and install the ubuntu. When you can see this page, it means that you are successfully entering the installation page.

![alt text](<截屏2024-08-28 21.18.10.png>)

Just select install Ubuntu22.04.4LTS, and install based on minimal installation.

Configure the user message as the following picture and then continue to install required components.
![alt text](<截屏2024-08-28 21.24.24.png>)

After installation, click restart now and follow the instructions on the screen.

Finally, run the command.
```
sudo apt update
sudo apt install open-vm-tools-desktop
sudo reboot
```

### 4. Install software and configure
Use wget to download `src-arm.zip` file.
```
wget https://seedsecuritylabs.org/setup/src-arm.zip
```

Unzip the file.
```
unzip src-arm.zip
```

cd into src-arm and run `./install.sh` script.

After the installation of require files, just run `sudo su seed` to change the user.

Now the setup is over!

### 5. prompt display
Configure the prompt as the following.
```
export PS1='[$(date +"%m/%d/%y")]\u@VM:Steven$ '
```

So the result is  as following.
![alt text](<截屏2024-08-28 22.36.41.png>)


## SEED in Windows11
Platform: Lenovo Xiaoxin 14pro
System: Windows11

### 1. Download & Install Virtual Box
Download Virtual Box in [offical website](https://www.virtualbox.org/wiki/Downloads)

Virtual Box is a famous free virtual machine platform. VMware Workstation is anothre one.(I think they have little difference when we use in this lab)

After downloading the package, run it and just click next step, nothing special we need to configure while installing.

### 2. Create a VM
Open Virtual Box and create a new virtual machine.

#### Name and Version
Name: CSE523Lab
Type: Linux
Version: Ubuntu (64-bit)
![Create a VM](<截屏2024-08-31 15.55.47.png>)

#### Memory & Hard Disk
Choose 4GB memory(2GB at least) and 4 CPU(one CPU at least)

Chose 80GB as a space of virtual hardware to make sure you have enough space.
#### Settings
Based on the [document](https://github.com/seed-labs/seed-labs/blob/master/manuals/vm/seedvm-from-scratch.md) to configure.

```
  General 
     Advanced Tab:
        Shared Clipboard: Bidirectional
        Drag'nDrop: Bidirectional

  System:
     Motherboard Tab:
        Base Memory: 4GB
        Extended Feature:  Enable I/O APIC
     Processor Tab:
        Processors(s): 4 CPU
        Extended Features:
            Enable PAE/Nx
     Acceleration Tab:
        Hardware Virtualization:
            Enable Hyper-V
            Enable Nested Paging

  Display:
     Screen Tab:
        Video Memory: 28 MB
        Graphic Controller: VMSVGA
        Acceleration: Enable 3D Acceleration

  Network:
     Adapter 1:
        Attached to: NAT Network
        Advanced:
           Promiscuous Mode: Allow All
           MAC Address: (click generate new MAC)
```

Warn: If you cannot configure NAT Network, maybe it is because you didn't create a NAT Network in Virtual Box. According to [document](https://web.ecs.syr.edu/~wedu/seed/Documentation/VirtualBox/VirtualBox_NATNetwork.pdf), we find the internet operator or just use Ctrl+H to find the operator.

![alt text](<截屏2024-08-31 16.24.52.png>)

In NAT Network, click to create a new Network, and just use the default configure.

### 3 Download Ubuntu
In the [offical website](https://releases.ubuntu.com/focal/), download 64bit PC(AMD64) desktop image.

After downloading ubuntu .iso file. Use it as a virtual disk of the VM, then we start the VM and install ubuntu.

![alt text](<截屏2024-08-31 21.05.25.png>)

![alt text](<截屏2024-08-31 21.08.18.png>)

### prompt display
Add the following in .bashrc file.
```bash
export PS1='[$(date +"%m/%d/%y")]\u@VM:Steven$ '
```

![alt text](<截屏2024-09-02 12.19.56.png>)