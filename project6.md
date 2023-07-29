# Web Solution With Wordpress

## Step 1 — Prepare a Web Server


#### We will launch an EC2 instance that will serve as “Web Server”. And we will create 3 volumes in the same AZ as our Web Server EC2, each of 10 GiB.

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/6d726249-72b8-4e95-b601-b918ced4c13a)

#### We will Open up the Linux terminal to begin configuration

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/a00af53d-9fe7-4d69-8d19-54b66a81cd19)

#### We will run command to inspect what block devices are attached to the server and also see the names of our newly created devices. 
`lsblk`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/423ee9ce-4fe4-42b3-aed8-4ffe9acb21c5)


#### We will run `df -h` command to see all mounts and free space on our server.

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/6c21c0cc-c125-4820-939e-b0f5fbb942f5)


#### We will Use gdisk utility to create a single partition on each of the 3 disks
`sudo gdisk /dev/nvme1n1`

`sudo gdisk /dev/nvme2n1`

`sudo gdisk /dev/nvme3n1`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/0290b998-e988-4f0b-965f-999202a54582)

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/b84eaf29-2eac-4a6d-a464-ccf4bc1967bd)

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/a1d1fb92-9cc5-41f6-8b5b-082aea151e21)


#### We will use `lsblk` utility to view the newly configured partition on each of the 3 disks.

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/dc0f8a82-da1f-4d54-a922-082d264b3ba0)


#### We will install lvm2 package.
`sudo yum install lvm2`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/857f79c5-d11b-48a5-9418-6deb5dde5efd)


![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/7b70bd7b-80a6-48e1-a73c-c260eba1af96)


#### We will run sudo `lvmdiskscan` command to check for available partitions.

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/9007b6f0-c14b-46fc-b476-a13b8c776184)


#### We will use `pvcreate` utility to mark each of 3 disks as physical volumes (PVs) to be used by LVM.
`sudo pvcreate /dev/nvme1n1p1`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/b13dd19b-5c11-4e76-af95-fedacb83a6c1)


`sudo pvcreate /dev/nvme2n1p1`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/c27dfbc8-a93b-492b-ad1f-1052b55a23a1)


`sudo pvcreate /dev/nvme3n1p1`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/9e6bbd73-72aa-4471-960c-70d315382dba)


#### We will verify that our Physical volume has been created successfully by running `sudo pvs`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/9607d577-d914-45f4-af9b-a4d19d1968d9)


#### We will use vgcreate utility to add all 3 PVs to a volume group (VG). Name the VG webdata-vg.

`sudo vgcreate webdata-vg /dev/nvme3n1p1 /dev/nvme2n1p1 /dev/nvme1n1p1`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/5e15c725-0e2b-4af4-adbd-cbf074ab482e)


#### We will verify that our VG has been created successfully by running `sudo vgs`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/6f68d426-1ca1-4724-a297-172e7b19ad33)


#### We will use `lvcreate` utility to create 2 logical volumes. apps-lv (Use half of the PV size), and logs-lv.

`sudo lvcreate -n apps-lv -L 14G webdata-vg`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/d1f6e35c-e05d-4aca-8a14-d68d79f6a2f1)


`sudo lvcreate -n logs-lv -L 14G webdata-vg`

![image](https://github.com/richardolat/PBL-1.LAMP/assets/134428528/c6b2e8fc-6bcc-4910-8e06-38d782e5cbba)











