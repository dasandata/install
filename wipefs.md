# LVM mount

## 참조 웹 문서
https://www.osradar.com/fixed-pvcreate-device-dev-mapper-excluded-by-a-filter/

## ZFS 사용 중 LVM 변경 내용 입니다.

```bash
[root@ubuntu:~]#
[root@rubuntu:~]# wipefs  -a /dev/mapper/mpathi
/dev/mapper/mpathi: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54
/dev/mapper/mpathi: 8 bytes were erased at offset 0x2bca5ffbffe00 (gpt): 45 46 49 20 50 41 52 54
/dev/mapper/mpathi: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa
/dev/mapper/mpathi: calling ioctl to re-read partition table: Invalid argument
[root@rubuntu:~]#

[root@rubuntu:~]#
[root@rubuntu:~]# pvcreate /dev/mapper/mpathi
  Physical volume "/dev/mapper/mpathi" successfully created.
[root@rubuntu:~]#

[root@rubuntu:~]#
[root@rubuntu:~]# vgcreate  dxome-data  /dev/mapper/mpathi
  Volume group "dxome-data" successfully created
[root@rubuntu:~]#

[root@rubuntu:~]#
[root@rubuntu:~]# lvcreate  -l 100%FREE dxome-data
WARNING: zfs_member signature detected on /dev/dxome-data/lvol0 at offset 413696. Wipe it? [y/n]: y
  WARNING: Invalid input 'ny'.
WARNING: zfs_member signature detected on /dev/dxome-data/lvol0 at offset 413696. Wipe it? [y/n]: y
  Wiping zfs_member signature on /dev/dxome-data/lvol0.
WARNING: zfs_member signature detected on /dev/dxome-data/lvol0 at offset 409600. Wipe it? [y/n]: y
  Wiping zfs_member signature on /dev/dxome-data/lvol0.
  Logical volume "lvol0" created.
[root@rubuntu:~]#

[root@rubuntu:~]#
[root@rubuntu:~]# lvs
  LV    VG         Attr       LSize    Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  lvol0 dxome-data -wi-a----- <700.65t
[root@rubuntu:~]#
```
