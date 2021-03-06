
Synthetic Audio Library (SEAL) Development Kit
Copyright (C) 1995, 1996, 1997, 1998, 1999 Carlos Hasan
All Rights Reserved

OS/2 Sound Driver Copyright (C) 1998 Martin Amodeo


This 1.0.7 release of the Synthetic Audio Library (SEAL) lets you write
applications that conform to the 1.0 SEAL API which is able to play
digital audio waveforms and music modules on many platforms.


What's New
----------

    - Source code released under the GNU Lesser General Public License (LGPL)

Features
--------
    - simple and powerful API interface
    - 32 simultaneous digital audio channels
    - smooth pitch shifting, volume and panning controllers per channel
    - smart digital filtering for improved sound quality
    - efficient digital audio waveform mixing algorithms combined with 
      uncompromising low-level optimizations
    - importing of wave and music file formats such as Protracker 1.1,
      MultiTracker 1.0, Scream Tracker 3.0 and FastTracker 2.0 modules
    - performance tuned for the i486 and Pentium processors
    - native support in DOS for hardware wavetable accelerators such
      as the Sound Blaster AWE32, Gravis Forte's UltraSound, and normal 
      digital audio devices such as the Sound Blaster 1.5/2.0/Pro/16, 
      Pro Audio Spectrum 16, Windows Sound System, Ensoniq Soundscape 
      and Aria soundcards


Supported platforms
-------------------
The SEAL SDK is available for DOS, Extended DOS, Windows 95, Windows NT,
OS/2, BeOS and Linux platforms. FreeBSD, SPARC SunOS, SPARC Solaris and
SGI Indigo ports are in progress. The following compilers were used to
build the library files:

    - Borland C++ 4.5 compiler for DOS and Win32s
    - WATCOM C/C++ 10.0 compiler for DOS and Windows
    - Microsoft Visual C++ 4.1 compiler for Windows 95
    - DJGPP 2.0 port of GNU C/C++ compiler for DOS
    - GNU C/C++ 2.7.0 for Linux (a.out and ELF)
    - Metrowerks CodeWarrior C++ for Intel BeOS Release 3
    - EMX port of GNU CC 2.7.x for OS/2 platforms


The SEAL SDK contains
---------------------
    - SEAL API header and library files
    - SEAL audio library source code files (GPL license)
    - set of example source code files


---------------------------------------------------------------------
IMPORTANT: Please make sure you understand the Copyright and License
information (in the file named LICENSE.TXT) before using this release.
---------------------------------------------------------------------


Installing the Software
-----------------------
The SEAL SDK can be installed unpacking the distribution archive
in your hard disk. For example,

    C:\>PKUNZIP -d SEAL107.ZIP

The SEAL SDK include and library directories can be installed in 
your C programming environment modifying the header and library 
directory paths. Here are some examples to compile and link
the SEAL audio system library with your own programs:

    - WATCOM C/C++32 10.0 and DOS4GW DOS Extender:
      wcl386 -I\audio\include example.c \audio\lib\dos\audiowcf.lib

    - DJGPP 2.0 port of GNU CC for DOS/DPMI32:
      gcc -I\audio\include -o example example.c \audio\lib\dos\audiodjf.a

    - Visual C/C++ 4.1 for Windows 95 and Windows NT:
      cl -DWIN32 -I\audio\include example.c \audio\lib\Win32\audw32vc.lib

    - Borland C++ 4.5 for Win32s:
      bcc32a -WC -I\audio\include example.c \audio\lib\Win32\audw32bc.lib

    - GNU CC 2.7.0 for Linux (ELF binaries):
      gcc -Iaudio/include -o example example.c audio/lib/Linux/libaudio.a

    - Metrowerks CodeWarrior C++ for BeOS R3:
      mwcc -Iaudio/include -o example example.c audio/lib/BeOS/libaudio.a

The above examples assume that the audio system was installed at the 
root directory of the current drive. For Windows 95 and Windows NT 
applications you must copy the AUDIOW32.DLL dynamic-link library into 
the Windows system directory, usually located at C:\WINDOWS\SYSTEM in
your hard disk.


Notes about DOS Drivers
-----------------------
For applications running in DOS, the audio system will try to detect
the hardware sound devices installed on your system. Since there can
be problems to autodetect your sound hardware, your application should
provide a way to force the use of a particular audio device driver.

Here is a list of notes for the autodetection methods used by the audio
device drivers under the DOS operating system:

    - Sound Blaster 1.0/1.5/2.0/Pro/16 device drivers:
      These drivers use the BLASTER environment variable to determine
      the hardware I/O base port address, IRQ interrupt line and DMA
      channels. The model of the card is then determined by hardware
      reading the DSP version number. If you do not get sound, try
      forcing other SB model by using the "T" parameter of the BLASTER
      environment variable:

                  T1 = Sound Blaster 1.0
                  T2 = Sound Blaster 1.5
                  T3 = Sound Blaster 2.0
                  T4 = Sound Blaster Pro
                  T6 = Sound Blaster 16

    - Sound Blaster AWE32 and Sound Blaster 32 device drivers:
      The driver uses the BLASTER environment variable, you must
      specify the EMU8000 I/O base port address parameter. If your
      card does not have DRAM local sound memory, you must use the
      card as a Sound Blaster 16 or earlier.

    - Pro Audio Spectrum, Pro Audio Spectrum Plus/16 device drivers:
      These drivers need to have the MVSOUND.SYS driver installed
      in your CONFIG.SYS configuration file. The model of the card
      is determined by hardware checking the card features bits.

    - Gravis Ultrasound, Ultrasound MAX device drivers:
      This driver uses the ULTRASND environment variable to determine
      the hardware configuration of your card. For applications using
      the DOS4GW extender, the GF1-IRQ number must be less than 8 to
      work correctly.

    - Gravis Ultrasound Daughterboard / MAX (CS4231) device drivers:
      This driver uses the CS4231 codec of your GUS DB/MAX card, so
      you must have the ULTRASND and ULTRA16 environment variables.

    - Gravis Ultrasound PnP (Pro), InterWave-based device drivers:
      This driver uses the ULTRASND and INTERWAVE environment variables
      to determine the hardware configuration of your sound board.
      
    - Windows Sound System device driver:
      This driver automatically detect WSS sound devices installed
      at the 530, E80, F40 or 604 I/O base port addresses and uses
      by default the IRQ line #7 and DMA channel #1 for playback.
      Since there can be hardware conflicts, the driver first check
      for the WSSCFG environment variable which has the following
      format:
                  SET WSSCFG=Annn In Dn
                              |    |  |
                              |    |  +-- DMA channel (0,1,3)
                              |    +---- IRQ number (7,9,10,11)
                              +----- I/O port (530,E80,F40,604)

      You must write the above command in your AUTOEXEC.BAT start-up
      batch file. Also, some WSS clone devices need to run an utility
      to put the card in WSS mode (ie. MAD16 OPTi-based cards).

    - Ensoniq Soundscape, Soundscape Elite device drivers:
      These drivers uses the SNDSCAPE environment variable to read
      the SNDSCAPE.INI configuration file.

    - Sierra Semoconductors' Aria sound card driver:
      This driver uses the ARIA environment variable to read the
      hardware configuration parameters.

    - Ensoniq AudioPCI and Creative PCI64 sound cards:
      These cards have to be configured in Legacy emulation mode
      under DOS. The library will use these cards as Ensoniq
      SoundScape ISA cards.

If you experience any problems, please try avoiding autodetection and
tell your application what device driver to use. Also, ensure your
system has no TSR's loaded in memory (such as SBOS for GUS cards).


Notes about Windows 95
----------------------
The SEAL audio system for DOS and Extended DOS has been sucessfully 
tested under Windows 95 DOS boxes running in foreground. However,
some Windows 95 sound drivers might not be able to share the sound
hardware with DOS sessions (such as the Ultrasound drivers). In such
cases, you must either remove the Windows 95 drivers or exit to DOS
to run your DOS programs.


Notes about Linux
-----------------
The SEAL audio system for Linux uses the UNIX Sound System interface,
also known as the VoxWare Kit. The audio system can be easily ported
to other UNIX operating system running in Intel x86 platforms where
the UNIX Sound System interface is also available, such as FreeBSD, 
386bsd, SCO and SVR4.2 operating systems.


Notes about BeOS
----------------
The SEAL audio library for Intel BeOS Release 3 also works with
New MediaKit sound drivers found on BeOS R4. The SEAL 1.06 library
comes with ELF binaries for Intel BeOS Release 4. 


Contacting the Author
---------------------
If you have questions, problems or comments you can contact the author 
at the following email address: chasan@dcc.uchile.cl.


Closing Words
-------------
I would like to thank all the beta testers and specially to Jon L. 
for the music module file used by the example programs, and to all
the IRC friends at the #coders channel.

