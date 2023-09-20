# Steps to Create Partitions with LVM

1. If you have a large amount of disk space, consider using `gdisk`:
   ```
   gdisk /dev/sda
   lsblk
   sfdisk -d /dev/sda
   ```

2. Print the partition details and apply them to another disk:
   ```
   sfdisk -d /dev/sda > partition.txt
   sfdisk /dev/sdb < partition.txt
   ```

   2.1. If you have multiple disks, repeat the following step for each disk (replace {a..j} with your disk identifiers):
   ```
   for i in {a..j}; do sfdisk /dev/sd${i} < partition.txt; done
   ```

3. Now, you need to create physical volumes (PVs):
   ```
   for i in {a..j}; do pvcreate /dev/sd${i}1; done
   pvdisplay
   ```

4. Create a volume group (VG):
   - Print all partitions:
     ```
     for i in {a..j}; do echo -n "/dev/sd${i}1 "; done
     ```
   - Create the VG with all the PVs (replace `/dev/sda1`, `/dev/sdb1`, etc., with your PVs):
     ```
     vgcreate vg0 /dev/sda1 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1 /dev/sdf1 /dev/sdg1 /dev/sdh1 /dev/sdi1 /dev/sdj1
     ```

5. Create a logical volume (LV) within the VG:
   ```
   lvcreate -l 100%FREE -n data vg0
   lvdisplay
   ```

6. Format the LV:
   ```
   mkfs.ext4 /dev/vg0/data
   ```

7. Get the UUID of the LV:
   ```
   blkid | grep data
   ```

8. Add the LV to `/etc/fstab` for automatic mounting:
   - Edit the `/etc/fstab` file using your preferred text editor (e.g., `vim /etc/fstab`).
   - Add the following line, replacing `UUID=6abaec30-0eb0-4b00-8af8-cd3bee6a0410` with the actual UUID from step 7:
     ```
     UUID=6abaec30-0eb0-4b00-8af8-cd3bee6a0410 /data ext4 defaults 0 2
     ```

9. Create a directory for mounting the LV and mount it:
   ```
   mkdir /data
   mount -a
   ```
