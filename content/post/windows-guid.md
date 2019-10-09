---
title: "Windows常见设备类型的GUID"
date: 2016-04-19T16:38:10+08:00
lastmod: 2016-04-19T16:38:10+08:00
draft: false
keywords: [windows, GUID]
description: ""
tags: [it]
categories: [冷知识]

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
# contentCopyright: true
reward: false
mathjax: false

---

### 1394 Host Bus Controller
Class = 1394
ClassGuid = `{6bdd1fc1-810f-11d0-bec7-08002be2092f}`
This class includes system-supplied drivers of 1394 host controllers connected on a PCI bus, but not drivers of 1394 peripherals.

### Battery Devices
Class = Battery
ClassGuid = `{72631e54-78a4-11d0-bcf7-00aa00b7b32a}`
This class includes drivers of battery devices and UPSes.

### CD-ROM Drives
Class = CDROM
ClassGuid = `{4d36e965-e325-11ce-bfc1-08002be10318}`
This class includes drivers of CD-ROM drives, including SCSI CD-ROM drives. By default, the system's CD-ROM class installer also installs a system-supplied CD audio driver and CD-ROM changer driver as PnP filters.

### Disk Drives
Class = DiskDrive
ClassGuid = `{4d36e967-e325-11ce-bfc1-08002be10318}`
This class includes drivers of hard disk drives. See also the HDC and SCSIAdapter classes.

### Display Adapters
Class = Display
ClassGuid = `{4d36e968-e325-11ce-bfc1-08002be10318}`
This class includes drivers of video adapters, including display drivers and video miniports.

### Floppy Disk Controllers
Class = FDC
ClassGuid = `{4d36e969-e325-11ce-bfc1-08002be10318}`
This class includes drivers of floppy disk drive controllers.

### Floppy Disk Drives
Class= FloppyDisk
ClassGuid= `{4d36e980-e325-11ce-bfc1-08002be10318}`
This class includes drivers of floppy drives.

### Hard Disk Controllers
Class = HDC
ClassGuid = `{4d36e96a-e325-11ce-bfc1-08002be10318}`
This class includes drivers of hard disk controllers, including ATA/ATAPI controllers but not SCSI and RAID disk controllers.

### Human Input Devices (HID)
Class = HIDClass
ClassGuid = `{745a17a0-74d3-11d0-b6fe-00a0c90f57da}`
This class includes devices that export interfaces of the HID class, including HID keyboard and mouse devices, which the installed HID device drivers enumerate as their respective "child" devices. (See also the Keyboard or Mouse classes later in this list.)

### Imaging Device
Class = Image
ClassGuid = `{6bdd1fc6-810f-11d0-bec7-08002be2092f}`
This class includes drivers of still-image capture devices, digital cameras, and scanners.

### IrDA Devices
Class = Infrared
ClassGuid = `{6bdd1fc5-810f-11d0-bec7-08002be2092f}`
This class includes Serial-IR and Fast-IR NDIS miniports, but see also the Network Adapter class for other NDIS NIC miniports.

### Keyboard
Class = Keyboard
ClassGuid = `{4d36e96b-e325-11ce-bfc1-08002be10318}`
This class includes all keyboards. That is, it also must be specified in the (secondary) INF for an enumerated "child" HID keyboard device.

### Medium Changers
Class= MediumChanger
ClassGuid= `{ce5939ae-ebde-11d0-b181-0000f8753ec4}`
This class includes drivers of SCSI media changer devices.

### Memory Technology Driver
Class = MTD
ClassGUID = `{4d36e970-e325-11ce-bfc1-08002be10318}`
This class includes drivers for memory devices, such as flash memory cards.

### Multimedia
Class = Media
ClassGuid = `{4d36e96c-e325-11ce-bfc1-08002be10318}`
This class includes Audio and DVD multimedia devices, joystick ports, and full-motion video-capture devices.

### Modem
Class = Modem
ClassGuid = `{4d36e96d-e325-11ce-bfc1-08002be10318}`
This class installs modems. An INF for a device of this class installs no device driver(s), but rather specifies the features and configuration information of a particular modem and stores this information in the registry. See also the Multifunction class.

### Monitor
Class = Monitor
ClassGuid = `{4d36e96e-e325-11ce-bfc1-08002be10318}`
This class includes display monitors. An INF for a device of this class installs no device driver(s), but rather specifies the features of a particular monitor to be stored in the registry for use by drivers of video adapters. (Monitors are enumerated as the child devices of display adapters.)

### Mouse
Class = Mouse
ClassGuid = `{4d36e96f-e325-11ce-bfc1-08002be10318}`
This class includes all mice and other kinds of pointing devices, such as trackballs. That is, it also must be specified in the (secondary) INF for an enumerated "child" HID mouse device.

### Multifunction Devices
Class = Multifunction
ClassGuid = `{4d36e971-e325-11ce-bfc1-08002be10318}`
This class includes combo cards, such as a PCMCIA modem and netcard adapter. The driver for such a PnP multifunction device is installed under this class and enumerates the modem and netcard separately as its "child" devices.

### Multi-port Serial Adapters
Class = MultiportSerial
ClassGuid = `{50906cb8-ba12-11d1-bf5d-0000f805f530}`
This class includes intelligent multiport serial cards, but not peripheral devices that connect to its ports. It does not include unintelligent (16550-type) mutiport serial controllers or single-port serial controllers (see the Ports class).

### Network Adapter
Class = Net
ClassGuid = `{4d36e972-e325-11ce-bfc1-08002be10318}`
This class includes NDIS NIC miniports excluding Fast-IR miniports, NDIS intermediate drivers (of "virtual adapters"), and CoNDIS MCM miniports.

### Network Client
Class = NetClient
ClassGuid = `{4d36e973-e325-11ce-bfc1-08002be10318}`
This class includes network and/or print providers.

### Network Service
Class = NetService
ClassGuid = `{4d36e974-e325-11ce-bfc1-08002be10318}`
This class includes network services, such as redirectors and servers.

### Network Transport
Class = NetTrans
ClassGuid = `{4d36e975-e325-11ce-bfc1-08002be10318}`
This class includes NDIS protocols, CoNDIS stand-alone call managers, and CoNDIS clients, as well as higher level drivers in transport stacks.

### PCMCIA Adapters
Class = PCMCIA
ClassGuid = `{4d36e977-e325-11ce-bfc1-08002be10318}`
This class includes system-supplied drivers of PCMCIA and CardBus host controllers, but not drivers of PCMCIA or CardBus peripherals.

### Ports (COM & LPT serial ports)
Class = Ports
ClassGuid = `{4d36e978-e325-11ce-bfc1-08002be10318}`
This class includes drivers of serial or parallel port devices, but see also the MultiportSerial class.

### Printer
Class = Printer
ClassGuid = `{4d36e979-e325-11ce-bfc1-08002be10318}`
This class includes printers.

### SCSI and RAID Controllers
Class = SCSIAdapter
ClassGuid = `{4d36e97b-e325-11ce-bfc1-08002be10318}`
This class includes SCSI HBA miniports and disk-array controller drivers.

### Smart Card Readers
Class = SmartCardReader
ClassGuid = `{50dd5230-ba8a-11d1-bf5d-0000f805f530}`
This class includes drivers for smart card readers.

### Storage Volumes
Class = Volume
ClassGuid = `{71a27cdd-812a-11d0-bec7-08002be2092f}`
This class includes storage volumes as defined by the system-supplied logical volume manager and class drivers that create device objects to represent storage volumes, such as the system disk class driver.

### System Devices
Class = System
ClassGuid = `{4d36e97d-e325-11ce-bfc1-08002be10318}`
This class includes the Windows® 2000 HALs, system bus drivers, the system ACPI driver, and the system volume-manager driver. It also includes battery drivers and UPS drivers.

### Tape Drives
Class = TapeDrive
ClassGuid = `{6d807884-7d21-11cf-801c-08002be10318}`
This class includes drivers of tape drives, including all tape miniclass drivers.

### USB
Class = USB
ClassGuid = `{36fc9e60-c465-11cf-8056-444553540000}`
This class includes system-supplied (bus) drivers of USB host controllers and drivers of USB hubs, but not drivers of USB peripherals.

## The following classes and GUIDs should not be used to install devices (or drivers) on Windows 2000 platforms:

### Adapter
Class = Adapter
ClassGUID = `{4d36e964-e325-11ce-bfc1-08002be10318}`
This class is obsolete.

### APM
Class = APMSupport
ClassGUID = `{d45b1c18-c8fa-11d1-9f77-0000f805f530}`
This class is reserved for system use.

### Computer
Class = Computer
ClassGUID = `{4d36e966-e325-11ce-bfc1-08002be10318}`
This class is reserved for system use.

### Decoders
Class = Decoder
ClassGUID = `{6bdd1fc2-810f-11d0-bec7-08002be2092f}`
This class is reserved for future use.

### Global Positioning System
Class = GPS
ClassGUID = `{6bdd1fc3-810f-11d0-bec7-08002be2092f}`
This class is reserved for future use.

### No driver
Class = NoDriver
ClassGUID = `{4d36e976-e325-11ce-bfc1-08002be10318}`
This class is obsolete.

### Non-Plug and Play Drivers
Class = LegacyDriver
ClassGUID = `{8ecc055d-047f-11d1-a537-0000f8753ed1}`
This class is reserved for system use.

### Other Devices
Class = Unknown
ClassGUID = `{4d36e97e-e325-11ce-bfc1-08002be10318}`
This class is reserved for system use. Enumerated devices for which the system cannot determine the type are installed under this class. Do not use this class if you're unsure in which class your device belongs; either determine the correct device setup class or create a new class.

### Printer Upgrade
Class = Printer Upgrade
ClassGUID = `{4d36e97a-e325-11ce-bfc1-08002be10318}`
This class is reserved for system use.

### Sound
Class = Sound
ClassGUID = `{4d36e97c-e325-11ce-bfc1-08002be10318}`
This class is obsolete.

### USB Mass Storage Device
ClassGUID = `{a5dcbf10-6530-11d2-901f-00c04fb951ed}`
