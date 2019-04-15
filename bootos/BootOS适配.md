# BootOS适配

BootOS精简了大部分驱动程序，只保留系统核心和硬件支持必备的驱动。当前支持的驱动程序列表如下，如果遇到不支持的设备，请按照文档里面的说明及时反馈给我们。

## 支持的硬件设备

| 驱动名称 | 驱动程序 | 驱动版本 |
| -------- | -------- | ---- |
| Exar Serial Driver | 8250_exar |  |
| Intel LPSS UART driver | 8250_lpss |  |
| MOXA SmartIO MUE driver | 8250_moxa |  |
| Dell PERC2, 2/Si, 3/Si, 3/Di, Adaptec Advanced Raid Products, HP NetRAID-4M, IBM ServeRAID & ICP SCSI driver | aacraid | 1.2.1[50877]-custom |
| Altera University Program PS2 controller driver | altera_ps2 |  |
| ARC PS/2 Driver | arc_ps2 |  |
| ARC(Synopsys) On-Chip(fpga) serial driver | arc_uart |  |
| Broadcom 44xx/47xx 10/100 PCI ethernet driver | b44 | 2.0 |
| QLogic BCM5706/5708/5709/5716 Driver | bnx2 | 2.2.6 |
| QLogic BCM57710/57711/57711E/57712/57712_MF/57800/57800_MF/57810/57810_MF/57840/57840_MF Driver | bnx2x | 1.712.30-0 |
| Broadcom BCM573xx network driver | bnxt_en | 1.9.2 |
|  | bridge | 2.3 |
| QLogic cnic Driver | cnic | 2.5.22 |
| CRC32c (Castagnoli) optimization using Intel Hardware. | crc32c-intel |  |
|  | dca | 1.12.1 |
| Network physical device Netlink interface | devlink |  |
| Intel(R) PRO/1000 Network Driver | e1000e | 3.2.6-k |
| Intel(R) PRO/1000 Network Driver | e1000 | 7.3.21-k8-NAPI |
| Intel(R) PRO/100 Network Driver | e100 | 3.5.24-k2-NAPI |
| Generic failover infrastructure/interface | failover |  |
| Force feedback support for memoryless devices | ff-memless |  |
| Intel(R) Ethernet Switch Host Interface Driver | fm10k | 0.23.4-k |
| Broadcom GENET Ethernet controller driver | genet |  |
| Keyboard driver for GPIOs | gpio_keys |  |
|  | hid-a4tech |  |
| Elo Accutouch HID TouchScreen driver | hid-accutouch |  |
| ALPS HID driver | hid-alps |  |
| HID Apple IR remote controls | hid-appleir |  |
|  | hid-apple |  |
| Asus HID Keyboard and TouchPad | hid-asus |  |
|  | hid-aureal |  |
| Force feedback support for ACRUX game controllers | hid-axff |  |
|  | hid-belkin |  |
|  | hid-betopff |  |
|  | hid-cherry |  |
|  | hid-chicony |  |
| CM6533 HID jack controls | hid-cmedia |  |
| HID driver for Corsair devices | hid-corsair |  |
| Cougar 500k Gaming Keyboard | hid-cougar |  |
| Silicon Labs HID USB to SMBus master bridge | hid-cp2112 |  |
|  | hid-cypress |  |
|  | hid-dr |  |
| Driver for HID ELAN Touchpads | hid-elan |  |
|  | hid-elecom |  |
|  | hid-elo |  |
|  | hid-emsff |  |
|  | hid-ezkey |  |
|  | hid-gaff |  |
| HID Gembird joypad driver | hid-gembird |  |
| Google Fiber TV Box remote control driver | hid-gfrm |  |
| MSI GT683R led driver | hid-gt683r |  |
|  | hid-gyration |  |
| Force feedback support for Holtek On Line Grip based devices | hid-holtekff |  |
|  | hid-holtek-kbd |  |
|  | hid-holtek-mouse |  |
|  | hid-hyperv |  |
| ION iCade input driver | hid-icade |  |
|  | hid-ite |  |
| Jabra USB HID Driver | hid-jabra |  |
|  | hid-kensington |  |
|  | hid-keytouch |  |
|  | hid-kye |  |
|  | hid-lcpower |  |
| Simple USB RGB LED driver | hid-led |  |
|  | hid-lenovo |  |
|  | hid-logitech-dj |  |
|  | hid-logitech-hidpp |  |
|  | hid-logitech |  |
|  | hid-mf |  |
|  | hid-microsoft |  |
|  | hid-monterey |  |
| HID multitouch panels | hid-multitouch |  |
| HID driver for Network Technologies USB-SUN keyboard adapter | hid-nti |  |
|  | hid-ortek |  |
| PenMount HID TouchScreen driver | hid-penmount |  |
|  | hid-petalynx |  |
| Minibox graphics PicoLCD Driver | hid-picolcd |  |
| Plantronics USB HID Driver | hid-plantronics |  |
|  | hid-pl |  |
|  | hid-primax |  |
|  | hid-prodikeys |  |
|  | hid-retrode |  |
| RMI HID driver | hid-rmi |  |
| USB Roccat Arvo driver | hid-roccat-arvo |  |
| USB Roccat common driver | hid-roccat-common |  |
| USB Roccat Isku/FX driver | hid-roccat-isku |  |
| USB Roccat char device | hid-roccat |  |
| USB Roccat Kone driver | hid-roccat-kone |  |
| USB Roccat Kone[+]/XTD driver | hid-roccat-koneplus |  |
| USB Roccat KonePure/Optical driver | hid-roccat-konepure |  |
| USB Roccat Kova[+] driver | hid-roccat-kovaplus |  |
| USB Roccat Lua driver | hid-roccat-lua |  |
| USB Roccat Pyra driver | hid-roccat-pyra |  |
| USB Roccat Ryos MK/Glow/Pro driver | hid-roccat-ryos |  |
| USB Roccat Savu driver | hid-roccat-savu |  |
|  | hid-saitek |  |
|  | hid-samsung |  |
| HID Sensor Hub driver | hid-sensor-hub |  |
|  | hid-sjoy |  |
|  | hid-sony |  |
|  | hid-speedlink |  |
|  | hid-steam |  |
|  | hid-steelseries |  |
|  | hid-sunplus |  |
|  | hid-tivo |  |
|  | hid-tmff |  |
|  | hid-topseed |  |
|  | hid-twinhan |  |
|  | hid-uclogic |  |
| PS3 uDraw tablet driver | hid-udraw-ps3 |  |
|  | hid-waltop |  |
| Driver for Nintendo Wii / Wii U peripherals | hid-wiimote |  |
|  | hid-xinmo |  |
|  | hid-zpff |  |
|  | hid-zydacron |  |
| Driver for HP Smart Array Controller version 3.4.20-125 | hpsa | 3.4.20-125 |
|  | hv_vmbus |  |
|  | hyperv-keyboard |  |
| I2C-Bus bit-banging algorithm | i2c-algo-bit |  |
| HID over I2C core driver | i2c-hid |  |
| Intel(R) Ethernet Connection XL710 Network Driver | i40e | 2.3.2-k |
| Intel(R) XL710 X710 Virtual Function Network Driver | i40evf | 3.2.2-k |
| Intel(R) Ethernet Connection E800 Series Linux Driver | ice | ice-0.7.0-k |
| Intel(R) Gigabit Ethernet Network Driver | igb | 5.4.0-k |
| Intel(R) Gigabit Virtual Function Network Driver | igbvf | 2.4.0-k |
| Intel(R) Integrated Sensor Hub PCI Device Driver | intel-ish-ipc |  |
| ISH ISHTP HID client driver | intel-ishtp-hid |  |
|  | intel-ishtp |  |
| Linux device interface for the IPMI message handler. | ipmi_devintf |  |
| Incoming and outgoing message routing for an IPMI interface. | ipmi_msghandler | 39.2 |
| Interface to the IPMI driver for the KCS, SMIC, and BT system interfaces. | ipmi_si |  |
| sysfs interface and helpers to export iSCSI boot information | iscsi_boot_sysfs |  |
| sysfs interface to BIOS iBFT information | iscsi_ibft | 0.5.0 |
| Intel(R) 10 Gigabit PCI Express Network Driver | ixgbe | 5.1.0-k |
| Intel(R) 10 Gigabit Virtual Function Network Driver | ixgbevf | 4.1.0-k |
| Intel(R) PRO/10GbE Network Driver | ixgb | 1.0.135-k2-NAPI |
| Driver for the Digi International Neo and Classic PCI based product line | jsm |  |
| LCD Lowlevel Control Abstraction | lcd |  |
| CRC32c (Castagnoli) calculations | libcrc32c |  |
| SAS Transport Layer | libsas |  |
| LLC IEEE 802.2 core support | llc |  |
| Software async multibuffer crypto daemon | mcryptd |  |
| Generic support for MDIO-compatible transceivers | mdio |  |
| LSI Logic MegaRAID legacy driver | megaraid | 2.00.4 |
| Avago MegaRAID SAS Driver | megaraid_sas | 07.706.03.00-rc1 |
| MII hardware support library | mii |  |
|  | mmc_core |  |
| LSI MPT Fusion SAS 3.0 Device Driver | mpt3sas | 26.100.00.00 |
| Fusion MPT base driver | mptbase | 3.04.20 |
| Fusion MPT SAS Host driver | mptsas | 3.04.20 |
| Fusion MPT SCSI Host driver | mptscsih | 3.04.20 |
| Failover driver for Paravirtual drivers | net_failover |  |
| PMC-Sierra PM8001/8006/8081/8088/8089/8074/8076/8077/8070/8072 SAS/SATA controller driver | pm80xx | 0.1.38 |
| Driver for AT42QT1070 QTouch sensor | qt1070 |  |
| RAID device class | raid_class |  |
|  | rc-core |  |
| RMI bus RMI F03 module | rmi_core |  |
| SAS Transport Attributes | scsi_transport_sas |  |
|  | serial_cs |  |
| Raw serio driver | serio_raw |  |
| SHA256 Secure Hash Algorithm, multi buffer accelerated | sha256-mb |  |
| SHA256 Secure Hash Algorithm, Supplemental SSE3 accelerated | sha256-ssse3 |  |
| Advanced Linux Sound Architecture driver for soundcards. | snd |  |
| Midlevel RawMidi code for ALSA. | snd-rawmidi |  |
| ALSA sequencer device management | snd-seq-device |  |
| Core sound module | soundcore |  |
| Sonics Silicon Backplane driver | ssb |  |
|  | stp |  |
| Broadcom Tigon3 ethernet driver | tg3 | 3.137 |
| Samsung touchkey driver | tm2-touchkey |  |
|  | uas |  |
| User-space I/O driver support for HID subsystem | uhid |  |
|  | uio |  |
| Driver for Alauda-based card readers | ums-alauda |  |
| SAT support for Cypress USB/ATA bridges with ATACB | ums-cypress |  |
| Driver for Datafab USB Compact Flash reader | ums-datafab |  |
| Driver for ENE UB6250 reader | ums-eneub6250 |  |
| Driver for Freecom USB/IDE adaptor | ums-freecom |  |
| Driver for In-System Design, Inc. ISD200 ASIC | ums-isd200 |  |
| Driver for Lexar Jumpshot Compact Flash reader | ums-jumpshot |  |
| Driver for Rio Karma | ums-karma |  |
| Maxtor USB OneTouch hard drive button driver | ums-onetouch |  |
| Driver for Realtek USB Card Reader | ums-realtek |  |
| Driver for SanDisk SDDR-09 SmartMedia reader | ums-sddr09 |  |
| Driver for SanDisk SDDR-55 SmartMedia reader | ums-sddr55 |  |
| Driver for SCM Microsystems (a.k.a. Shuttle) USB-ATAPI cable | ums-usbat |  |
| USB Mass Storage driver for Linux | usb-storage |  |
| Virtio block driver | virtio_blk |  |
| Virtio network driver | virtio_net |  |
| VMware vmxnet3 virtual NIC driver | vmxnet3 | 1.4.16.0-k |
| USB Wacom tablet driver | wacom | v2.00 |
| SGI XFS with ACLs, security attributes, scrub, no debug enabled | xfs |  |
| xHCI Platform Host Controller Driver | xhci-plat-hcd |  |

## 新硬件适配

如果遇到不能支持的硬件，请联系我们，在 GitHub 上面提交 issue，我们会优先处理 GitHub 上面的硬件适配需求。反馈地址：https://github.com/idcos/osinstall-server/issues