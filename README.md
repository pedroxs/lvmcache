# lvmcache
tool to cache disk with ram resource

sample code:
```
mount -t tmpfs -o size=1g tmpfs /mnt
dd if=/dev/zero of=/mnt/data bs=1k count=1048576
losetup /dev/loop0 /mnt/data
lvcreate -n meta0 -L 900M ubuntu-vg /dev/loop0
lvcreate -n meta0m -L 100M ubuntu-vg /dev/loop0
lvconvert --type cache-pool --poolmetadata ubuntu-vg/meta0m ubuntu-vg/meta0
lvconvert --type cache --cachepool ubuntu-vg/meta0 ubuntu-vg/damato
lvconvert --splitcache ubuntu-vg/damato
lvremove ubuntu-vg/meta0
losetup -d /dev/loop0
umount /mnt
```
