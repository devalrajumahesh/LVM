========Logical Volume Creations(lvm)==========

1) Add the volumes to instance ( take 20gb )

2) by using lsblk we can check dick is attached or not

		fdisk -l it will show clarity

3) give the command fdisk /dev/xvdf and make the partition

pressing n    and press the p( primary partition) and ive the memory like +500MB or 1000GB

4) create the physcical volumes by using pvcreate command

	pvcreate /dev/xvdf1 /dev/xvdf2 /dev/xvdf3 ............

5) cretae the volume groups by using vgcretae command

	vgcretae vgname /dev/xvdf1 /dev/xvdf2 /dev/xvdf3 ............

once we create the volumegroups by using vgextend command we can extend the volume gropus

	vgextend  vgname /dev/xvdf5 /dev/xvdf6 /dev/xvdf7 ............

6) creat ethe logical volumes by using lvcreate command

	lvcreate -L+1G -n newlv vgname


-L =By using L means whatever we are gving memory that only cane take liker we are giving 1GB that only can take 
-l = by using l means whaterver remaing space in volumegroup that only can take

7) make file system by using mkfs command

	mkfs.ext4 /dev/vganme/newlv

8) create directory this dirctory is used for mounting


	mkdir /lvm

9) mount the filesystem by using mount

	mount /dev/vgname/newlv /lvm

10) permanently mount in fstab

/dev/vgname/newlv  	/lvm  	ext4  default(mount option)    		0(backup operation)   0(file systemc check order)
				      userquota/acl/group quota

11) Extending  the file system:


	only three steps to increase the filesystem 

	lvextend  -L+1G  /dev/vgname/lvname

	resize2fs /dev/vgname/lvname
	
	df-Th 


12) Reduce the filesystem:


	there are seven steps to reduce the lv

	unmount the filesystem          umount   /dev/vgname/lvname

	check the filesystem            e2fsck  -f  /dev/vgname/lvname

	lvreduce  -L-1G  /dev/vgname/lvname

	resize2fs  /dev/vgname/lvname

	mkfs.ext4   /dev/vgname/lvname

	mount /dev/vgname/lvname

	df-Th

13) any possibility to change the name of volume group and logical volume 

ans: yes its possible to change the vg and lv

vgrename  oldvgname  newvgname

lvrename /dev/vgname/oldlv  /dev/vgname/newlv
