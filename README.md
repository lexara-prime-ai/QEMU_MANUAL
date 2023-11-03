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

* After you run the previous command, QEMU will start for you as a standalone window:

Now, if you want to **just boot from the image file without the ISO file** (for example ***if you have finished installing and now you always want to boot the installed system***), you can just **remove** the **`-cdrom`** option:

```powershell
C:\User> qemu-system-x86_64 -m 1024  -boot d -enable-kvm -smp 3  -net nic -net user -hda testing-image.img
```

* If you want, you can choose from a lot of other **available architectures** to test your systems on:

**On Linux :**
```bash
$ ls /usr/bin | grep qemu-system*
```
**Output :**
```bash
qemu-system-aarch64
qemu-system-alpha
qemu-system-arm
qemu-system-cris
qemu-system-i386
qemu-system-lm32
qemu-system-m68k
qemu-system-microblaze
qemu-system-microblazeel
qemu-system-mips
qemu-system-mips64
qemu-system-mips64el
qemu-system-mipsel
qemu-system-moxie
qemu-system-or32
qemu-system-ppc
qemu-system-ppc64
qemu-system-ppc64le
qemu-system-ppcemb
qemu-system-sh4
qemu-system-sh4eb
qemu-system-sparc
qemu-system-sparc64
qemu-system-tricore
qemu-system-unicore32
qemu-system-x86_64
qemu-system-x86_64-spice
qemu-system-xtensa
qemu-system-xtensaeb
```
**For example**, if you want to emulate the **i386 architecture**, you should run the following command:
```powershell
C:\User> qemu-system-i386 -m 1024  -boot d -enable-kvm -smp 3  -net nic -net user -hda testing-image.img
```
Just make sure that the ISO file for Linux distributions and other operating systems you use are for the same architecture that you use on QEMU. If they are different, you may not be able to boot it up or install it.

If you want to use QEMU to boot from a CD / DVD inserted at your disk drive, then you can easily do:
```powershell
C:\User> qemu-system-x86_64 -m 1024  -boot d -enable-kvm -smp 3  -net nic -net user -hda testing-image.img -cdrom /dev/cdrom
```
