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

