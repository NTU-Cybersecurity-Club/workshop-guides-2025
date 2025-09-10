# Workshop 1 Guide (Kali Linux Installation)

*Author: Tay Jovan*  
*Last Updated: 2025/09/08*

## 0. Outline

## 1. Windows

### 1.1. VirtualBox

Download VirtualBox from their [official website](https://www.virtualbox.org/wiki/Downloads).

![](workshop-1-images/virtualbox-windows.png)

Locate the VirtualBox installer in your File Explorer and double-click on it to launch:

![](workshop-1-images/virtualbox-installer-file-explorer.png)

Click on `Next`:

![](workshop-1-images/virtualbox-installer-page-1.png)

Click on `Next`:

![](workshop-1-images/virtualbox-installer-page-2.png)

Click on `Next`:

![](workshop-1-images/virtualbox-installer-page-3.png)

Click on `Yes`:

![](workshop-1-images/virtualbox-installer-page-4.png)

Click on `Yes`:

![](workshop-1-images/virtualbox-installer-page-5.png)

Click on `Next`:

![](workshop-1-images/virtualbox-installer-page-6.png)

Click on `Install`:

![](workshop-1-images/virtualbox-installer-page-7.png)

When the installation completes, you should see the homepage:

![](workshop-1-images/virtualbox-installer-page-8.png)

### 1.2. Kali Linux Pre-Built VirtualBox Image

Download the Kali Linux Pre-Built VirtualBox Image from Kali Linux [official website](https://www.kali.org/get-kali/#kali-virtual-machines)

![](workshop-1-images/kali-linux-prebuilt-image-windows.png)

Right-click on the `.7z` file and extract it:  
*(Note: If extraction fails, retry with [7-Zip](https://www.7-zip.org/))*

![](workshop-1-images/kali-linux-extract-7z-file.png)

Click on the plus icon in VirtualBox:

![](workshop-1-images/virtualbox-add-vm.png)

Select the extract Kali Linux Pre-built Virtual Machine and click on `open`:

![](workshop-1-images/kali-linux-prebuilt-vm.png)

The Kali Linux virtual machine should appear in VirtualBox:

![](workshop-1-images/kali-linux-added.png)

Click on the `start` button to launch Kali Linux:

![](workshop-1-images/kali-linux-start-button.png)

Login with username `kali` and password `kali`.

## 2. Mac

For our club, we will be using VirtualBox to standardise the virtual platform for both Windows and MacOS users. However, other options such as VMWare and UTM exist. If you wish to use those platforms instead, you may follow the official guides by OffSec:

VMWare: https://www.kali.org/docs/virtualization/install-vmware-guest-vm/  
UTM: https://www.kali.org/docs/virtualization/install-utm-guest-vm/

### 2.1. VirtualBox

Download VirtualBox from their [official website](https://www.virtualbox.org/wiki/Downloads).

![](workshop-1-images/virtualbox-windows.png)

Locate VirtualBox in your downloads and install it (Screenshots TBA)

### 2.2. Kali Linux ISO

Download the Kali Linux ISO from Kali Linux [official website](https://www.kali.org/get-kali/#kali-installer-images)

![](workshop-1-images/kali-installer-mac.png)

Click on the `new` button to create a new vm:

![](workshop-1-images/virtualbox-open.png)  
In the `VM Name` field, type `kali`:

![](workshop-1-images/photo_6152344947496438371_y.jpg)

Under `ISO Image`, click on the dropdown button and open your Finder. Locate the downloaded Kali Linux iso image from earlier and click `open`:

![](workshop-1-images/photo_6152344947496438372_y.jpg)

Leave the rest of the fields as it is and click on `next`. For the following options, set it as following:
- `Base Memory`: 4096 MB
- `Number of CPUs`: 2
- `Disk Size`: 80.00 GB

![](workshop-1-images/photo_6152344947496438373_y.jpg)

![](workshop-1-images/photo_6152344947496438374_y (1).jpg)

Click on `Next` and then `Finish`.

![](workshop-1-images/photo_6152344947496438375_y.jpg)

Click on the `Settings` button.

![](workshop-1-images/photo_6152344947496438376_y.jpg)

Under `Expert` > `Display` > `Scale Factor`, set it to `300%`. Click on `OK` to save it:  
![](workshop-1-images/photo_6152344947496438377_y.jpg)

Click on the `Start` button:

![](workshop-1-images/photo_6152344947496438376_y.jpg)

In the installation page, press `enter`:

![](workshop-1-images/photo_6152344947496438367_x 1.jpg)

Select `English` and press `enter`:

![](workshop-1-images/photo_6152344947496438351_x.jpg)

Select `United States` and press `enter`:

![](workshop-1-images/photo_6152344947496438352_x.jpg)

Select `American English` and press `Enter`:

![](workshop-1-images/photo_6152344947496438353_x.jpg)

Under hostname, type `Kali` and press `Enter`:

![](workshop-1-images/photo_6152344947496438354_x.jpg)

Leave the domain name field empty, press `Enter`:

![](workshop-1-images/photo_6152344947496438355_x.jpg)

For full name, type `kali` and press `Enter`:

![](workshop-1-images/photo_6152344947496438356_x.jpg)

For username, type `kali` and press `Enter`:

![](workshop-1-images/photo_6152344947496438357_x.jpg)

For password, type `kali` and press `Enter`:

![](workshop-1-images/photo_6152344947496438358_x.jpg)

Retype `kali` and press `Enter`:

![](workshop-1-images/photo_6152344947496438359_x.jpg)

For time zone, select `Eastern` and press `Enter`:  
![](workshop-1-images/photo_6152344947496438360_x.jpg)

For disk partitions, select `use entire disk` and press `Enter`:

![](workshop-1-images/photo_6152344947496438361_x.jpg)

For disk selection, select `VBOX HARDDISK` and press `Enter`:

![](workshop-1-images/photo_6152344947496438362_x.jpg)

For partitioning scheme, select `All files in one partition` and press `Enter`:

![](workshop-1-images/photo_6152344947496438363_x.jpg)

Select Finish partitioning and press `Enter`:

![](workshop-1-images/photo_6152344947496438364_x.jpg)

Select `Yes` and press `Enter`:

![](workshop-1-images/photo_6152344947496438365_x.jpg)

For software selection, leave the default options and press `Enter`:

![](workshop-1-images/photo_6152344947496438366_x.jpg)

When installation completes, press `Enter`:

![](workshop-1-images/photo_6152344947496438368_x.jpg)

Your Kali VM should start booting:

![](workshop-1-images/photo_6152344947496438369_y.jpg)

When brought to the installation page, enter your credentials `kali : kali`.
