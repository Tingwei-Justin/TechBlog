[toc]

## 1. neuroimage

**Domain**: neuroimage.usc.edu

**IP**: 128.125.20.161

**MAC** **address**: 10:98:36:ac:dd:c7 

**Purpose**: Hosts neuroimage wiki, brainstorm wiki, brainstorm forum



ssh root@neuroimage.usc.edu -p 51729

Password: BigLab!@#Sipi_EE!



generate ssh key: `ssh-keygen`

remote copy server file to local machine:

- scp -P 51729 root@neuroimage.usc.edu:/root/.ssh/id_rsa /Users/luckyjustin

- next time use ssh key login in ssh (don't use password)

  ssh root@neuroimage.usc.edu -p 51729



## 2. neuroiamge2

**Domain**: neuroimage2.usc.edu

**IP**: 128.125.20.168

**MAC** **address**: 00:15:17:ad:c4:10

**Purpose**: Backup server for neuroimage.usc.edu



**Users**:

root - BigLab-Sipi_EE!



## 3. dynamics

**Domain**: dynamics.usc.edu

**IP**: 128.125.20.170

**MAC** **address**: 00:25:90:0b:65:34

**Purpose**: For processing



**Users:**

root - athena71



## 4. recon

**Domain**: recon.usc.edu

**IP**: 128.125.20.71

**MAC** **address**: 00:30:48:fe:6a:a8

**Purpose**: For processing

**Custom Settings**:

SSH port - 57129



**Users:**

root - athena71





## 5. tomo

**Domain**: tomo.usc.edu

**IP**: 128.125.20.24

**MAC** **address**: 1c:1b:0d:8d:8e:ea

**Purpose**: For a new project



**Custom Settings**:

ssh port - 60229



**Users:**

root - s3rv3r@PenGuin



## 6. brainconnectivity

brainconnectivity.usc.edu

Noraml one is production

:3003 is test server (andrew test first)



## 7. SIDEKICK

**Domain**: sidekick.usc.edu

**Location:** RTH – 3rd Floor – BIG Lab

**IP**: 68.181.161.38

**DNS:** 128.125.253.194, 128.125.7.23

**Gateway:** 68.181.161.254

**MAC** **address**: 00:11:32:0D:B5:DB

**DSM: https://sidekick.usc.edu:5001/**

 

**Purpose**: Backup NAS



**Users:**

root

admin

(Reach out to Prof. Anand Joshi for password to these accounts)



## 8.  server neuroimagetest.usc.edu

重点

brainconnectivity:

Anna leahy







Active develop:

features



管理：

分为两块

neuroimage

Computing: 软件更新，disk，空间，维护



IT solution

Leahy 发个邮件的





Backup database for brainconnectivity

选一个backup的server

选择性下载部分file





filter tag:



Bug: 

