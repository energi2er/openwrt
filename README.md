# openwrt
setup openwrt with 1 gig hard and 2 interface
1-from openwrt site follow this guide:
https://openwrt.org/docs/guide-user/virtualization/vmware
2- download centos minimal  linux from this link( using finix for configuration hdd for openwrt):
http://ftp.funet.fi/pub/mirrors/centos.org/7.9.2009/isos/x86_64/CentOS-7-x86_64-Minimal-2207-02.iso
3- 

create a ide hard disk for vm of openwrt with 1 gig space
run the vm with centos minimal in rescue mode 
doing this 
Disk Size Issues

Disk size and problems with veeam backup and enlarging the disk Veeam backup and VMware will complain about the size of the virtual disk provided by the OpenWrt download because the disk is not multiple of 1KB. (this means: no backups available, and could be crucial in production environments)

VMware won't let you enlarge the disk in the normal way, so one simple way is:

    make a snapshot of the vm, for possible rollback
    move the original disk (from OpenWrt downloads) on ide 0:1
    add a new disk, with a whole size, like 128 MB , on ide 0:0
    use sysrescuecdiso
    start the vm with the iso
    with dd copy the disc on ide 0:1 to ide 0:0 like dd if=/dev/sdb of=/dev/sda
    enter fdisk /dev/sda and write the partition table (without making changes, this helps sysrescuecd to see the partitions properly)
    do fsck -f on the sda2 partition
    with fdisk resize the sda2 partition to occupy all the space available (but still starting with the same sector of before, normally 9135)
    use resize2fs /dev/sda2
    do fsck -f /dev/sda2
    restart the machine and boot with OpenWrt check that the system uses the new partition
    stop the machine, delete the previous hd (with less than 128MB)
    restart the machine and verify that everything is ok.


install v2raya from the gui of openwrt and the 
# For advanced usage, please see /etc/config/v2raya
uci set v2raya.config.enabled='1'
uci commit v2raya




Visit v2rayA webUI and enjoy

http://<your_router_ip>:2017


