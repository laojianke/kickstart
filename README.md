# kickstart
kickstart configuration for rhel6/centos6 install automatically

1. Copy the whole content of DVD or ISO to harddisk.
mkdir /mnt/iso
mount -t iso9660 -o loop /data/workdir/centos6.x.iso /mnt/iso
cd /mnt/iso
mkdir /var/tmp/iso_tmp
cp -rf * /var/tmp/iso_tmp/

2. Copy isolinux.cfg to /var/tmp/iso_tmp/isolinux and overwithe old one.

3. Copy ks.cfg to /var/tmp/iso_tmp/isolinux

4. Repack iso file.
cd /var/tmp/iso_tmp
genisoimage -U -r -v -T -J -joliet-long -V "centos-6.x" -volset "centos-6.x" -A "centos-6.x" -b isolinux/isolinux.bin -c isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table -eltorito-alt-boot -e images/efiboot.img -no-emul-boot -o ../centos-6.x_auto_install.iso .
implantisomd5 ../centos-6.x_auto_install.iso
