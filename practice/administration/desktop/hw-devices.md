# Системы и технологии железа

<details>
    <summary>Черновой список</summary>

- Linux 5.19.0-35-generic ehci_hcd

- smbios

- dmi

- smp

- vsyscall32

pci upgrade shadowing cdboot bootselect edd int13floppynec int13floppytoshiba int13floppy360 int13floppy1200 int13floppy720 int13floppy2880 int9keyboard int10video acpi usb biosbootspecification uefi

lm fpu fpu_exception wp vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ht tm pbe syscall nx rdtscp x86-64 constant_tsc arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic popcnt tsc_deadline_timer xsave avx lahf_lm epb pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid xsaveopt dtherm arat pln pts md_clear flush_l1d cpufreq

synchronous internal write-through instruction data

msi pm vga_controller bus_master cap_list rom fb

MEI Controller

pm msi ehci bus_master cap_list

EHCI Host Controller

pm msi pciexpress bus_master cap_list

High Definition Audio Controller:

- HDA Intel PCH Mic
- HDA Intel PCH Headphone
- HDA Intel PCH HDMI/DP,pcm=3

PCI bridge

pci pciexpress msi pm normal_decode bus_master cap_list

pm msi msix pciexpress bus_master cap_list rom ethernet physical tp 10bt 10bt-fd 100bt 100bt-fd 1000bt 1000bt-fd autonegotiation

MMC Host

pm msi pciexpress bus_master cap_list

pm msi pciexpress bus_master cap_list ethernet physical wireless

pm msi msix pciexpress xhci bus_master cap_list

xHCI Host Controller

usb-2.00

pm debug ehci bus_master cap_list

bluetooth usb-1.10

ISA bridge

isa bus_master cap_list

PnP device

pnp

6 port Mobile SATA AHCI Controller

sata msi pm ahci_1.0 bus_master cap_list emulated

gpt-1.00 partitioned partitioned:gpt

partitioned partitioned:dos

primary ntfs initialized

journaled extended_attributes large_files huge_files dir_nlink 64bit extents ext4 ext2 initialized recover

primary journaled extended_attributes large_files huge_files dir_nlink recover extents ext4 ext2 initialized

platform

Virtual Battery

Power Button

power

Lid Switch

Acer WMI hotkeys

Video Bus

Sleep Button

AT Translated Set 2 keyboard

i8042

ETPS/2 Elantech Touchpad

</details>
<br/>
Список для данной заметки я выбрал из вывода команды `lshw`

## Мелочи

**Linux x.xx.x-xx-generic**: generic - это ядро без наложения патчей дистрибутива.

## HCD и HCI

Первый раз
