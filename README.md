## Basic Commands | QEMU

****To **create an image file** with the **size of 10GB** and **qcow2 format** (default format for QEMU images), run:****
```powershell
C:\User> qemu-img create -f qcow2 testing-image.img 10G
```
* Note that a new file called “**testing-image.img**” is now created at your home folder (**or the place where you run the terminal**). Note also that the size of this file is **not 10 Gigabytes**, it’s around **150KB** only; QEMU won’t use any space unless needed by the virtual operating system, but it will set the **maximum allowed space for that image** to 10 Gigabytes only.

**if you have an ISO file for a Linux distribution or any other operating system and want to test it using QEMU and use the new image file that was created as a hard drive, you can run:**
```powershell
C:\User> qemu-system-x86_64 -m 1024  -boot d -enable-kvm -smp 3  -net nic -net user -hda testing-image.img -cdrom ubuntu-16.04.iso
```
**Breakdown**:

**`-m 1024`**: Here we chose the RAM amount that we want to provide for QEMU when running the ISO file. We chose 1024MB here. You can change it if you like according to your needs.

-**`boot -d`**: The boot option allows us to specify the boot order, which device should be booted first? 

**`-d`** means that the CD-ROM will be the first, then QEMU will boot normally to the hard drive image. We have used the **-cdrom** option as you can see at the end of the command. You can use **-c** if you want to boot the hard drive image first.

**`-enable-kvm`**: This is a very important option. It allows us to use the KVM technology to emulate the architecture we want. Without it, QEMU will use software rendering which is very slow. That’s why we must use this option, just make sure that the virtualization options are enabled from your computer BIOS.

**`-smp 3:`**  If we want to use more than 1 core for the emulated operating system, we can use this option. We chose to use **3 cores** to run the virtual image which will make it faster. You should change this number according to your computer’s CPU.

**`-net nic`** **`-net user`**: By using these options, we will enable an Ethernet Internet connection to be available in the running virtual machine by default.

**`-hda testing-image.img`**: Here we specified the path for the hard drive which will be used. In our case, it was the testing-image.img file which we created before.

**`-cdrom ubuntu-16.04.iso`**: Finally we told QEMU that we want to boot our ISO file “ubuntu-16.04.iso”.
