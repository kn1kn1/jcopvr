This driver is a Windows version of the JCOP Simulation ifdhandler (see [JPCSC](http://www.musclecard.com/middle.html) for more information). It enables a PC/SC client software on Windows 2000 to talk with the JCOP simulator.

### Files ###
  1. jcop\_vr.sys: kernel-mode driver.
  1. jcop\_proxy.exe: user-mode application.

As it seems to be difficult for me to invoke socket functions (or TDI functions) from a kernel-mode driver, the user-mode application invokes Winsock functions to mediate interaction between the kernel-mode driver and the JCOP simulator.

### Notice ###
  * **Works only for Windows 2000**: This driver is developed as a legacy smart card driver and needs a help of Smart Card Helper service which has been deprecated from Windows XP SP2.
  * **T=1 is not fully supported**: As this driver is a virtual driver, it has minimal error free operations. No error detection and correction is implemented.
  * **No warranty**: This software is provided on an "AS IS" basis and without any warranty. This software includes a kernel-mode driver and may induce a Blue Screen of Death (and damage your system), but you are solely responsible for determining the appropriateness of using this software.

### Installation & usage (or how to debug your JavaCard Applet) ###

  1. Install **jcop\_vr.sys**. I use DIP.exe provided at http://ruffnex.oc.to/kenji/windriver/.
[![](http://lh4.google.com/kanai.kenichi/R6beVBFF7AI/AAAAAAAAAI8/AeyFmGjIdIk/s144/dip01.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5163058475475266562)

> 2. Execute Eclipse or JCOP Tools.

> 3. Set some break points in your JavaCard Applet and invoke the JCOP debugger.
[![](http://lh6.google.com/kanai.kenichi/R6aoyhFF6-I/AAAAAAAAAHo/8SQNp8Vu14k/s144/eclipse01_01.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162999608653507554)  [![](http://lh3.google.com/kanai.kenichi/R6ajNxFF68I/AAAAAAAAAGg/VErrewryh2Y/s144/eclipse02.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162993479735176130)

> 4. Type "/close" in the JCOP Shell window to close the JCOP Shell session. Otherwise, you can not connect to the JCOP simulation socket server.
[![](http://lh5.google.com/kanai.kenichi/R6ajORFF69I/AAAAAAAAAGo/6l4XIHz8PAw/s144/eclipse03_01.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162993488325110738)

> 5. Execute **jcop\_proxy.exe**. Type **"jcop\_proxy start"** in command prompt.
[![](http://lh3.google.com/kanai.kenichi/R6aHWxFF62I/AAAAAAAAAEk/AEMRRvnBeXE/s144/jcop_vr01.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162962848028420962)

> After you have successfully started jcop\_proxy.exe, you will see the following dialog. Press "OK".
[![](http://lh3.google.com/kanai.kenichi/R6mlCBFF7BI/AAAAAAAAAJk/wVTIZS6Ez68/s144/jcop_vr06.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5163839901825100818)

> 6. Open service in control panel, select "Smart Card" service (not "Smart Card Helper" service) and restart it.
[![](http://lh4.google.com/kanai.kenichi/R6aozBFF6_I/AAAAAAAAAHw/8VGXjMJtY8Y/s144/jcop_vr03_01.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162999617243442162)

> 7. Execute your PC/SC application and invoke some commands.

> 8. To stop jcop\_proxy.exe, type **"jcop\_proxy stop"** in command prompt.
[![](http://lh3.google.com/kanai.kenichi/R6aMRxFF66I/AAAAAAAAAF4/Z0hlkZqUZEk/s144/jcop_vr04.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162968259687213986)

> After you have successfully stopped jcop\_proxy.exe, you will see the following dialog.
[![](http://lh6.google.com/kanai.kenichi/R6aMRhFF65I/AAAAAAAAAFw/qjnDX_W5HBk/s144/jcop_vr05.jpg)](http://picasaweb.google.com/kanai.kenichi/Jcop_vrScreenShot/photo#5162968255392246674)


  * You may need some reboot to make this driver work properly. For example, if you have uninstalled this driver, you need to restart your pc before the next installation.

### Compilation ###

> #### jcop\_vr.sys ####
> > You need "Windows Server 2003 SP1 DDK" to build jcop\_vr.sys.

  1. Invoke "Windows 2000 Checked Build Environment". After you have successfully installed DDK, you can find it "_start->programs->Development Kits->Windows DDK 3790.1830->Build Environments->Windows 2000->Windows 2000 Checked Build Environment_".
  1. Change directory to (somewhere you download source)\jcop\_vr\kernel.
  1. Input "build".
  1. You will find a newly built jcop\_vr.sys under (somewhere you download source)\jcop\_vr\kernel\objchk\_w2k\_x86\i386 directory.


> #### jcop\_proxy.exe ####
> > It is a Visual Studio .NET 2002 solution. Open the solution with your Visual Studio and build it.

### Reference ###

> #### Device Driver development ####
    * [Windows Device Driver Programming Part 1](http://ruffnex.oc.to/kenji/windriver/) (Japanese)
    * [Driver Development Part 1: Introduction to Drivers](http://www.codeproject.com/KB/system/driverdev.aspx)

> #### Device Driver architecture ####
    * [SoftEther の内部構造](http://softether.com/jp/company/media/academic/data/softetherpaper002.pdf) (Japanese)

> #### PC/SC Driver ####
    * [Development of PC/SC compatible driver for WINDOWS](http://www.bds.dogma.net/pc_sc.htm)
    * [TTFN PC/SC DumbMouse Driver](http://www.ttfn.net/techno/dm.html)

> #### Tools ####
    * [Windows Server 2003 SP1 DDK](http://www.microsoft.com/whdc/DevTools/ddk/default.mspx)
    * [DebugView for Windows](http://technet.microsoft.com/ja-jp/sysinternals/bb896647(en-us).aspx)