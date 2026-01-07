# Linux-Storage-Management-Project-Part-1
# Linux Disk Partitioning Project — Creating 6 Partitions on a 20 GB Disk

<img width="1091" height="732" alt="Linux Storage Management - Part 1 pic 20" src="https://github.com/user-attachments/assets/71fcd612-3483-4069-8e3f-c85e62d70fa1" />

## 📝 Overview
## This project demonstrates how to create six partitions on a secondary 20 GB disk (/dev/sdb) using fdisk on CentOS 9 Stream. It walks through identifying the disk, creating primary, extended, and logical partitions, and verifying the final layout using standard Linux storage tools.

## This hands‑on exercise strengthens core Linux system administration skills, including:

• 	Disk provisioning

• 	Partition table management

• 	Understanding primary, extended, and logical partitions

• 	Using lsblk, fdisk, and fdisk -l

• 	Working safely with storage devices in a VM environment

## 🖥️ Environment:

•   OS: CentOS 9 Stream (VirtualBox VM)

•   Disk: /dev/sdb (20GB virtual disk)

•   Tools Used: lsblk, fdisk, fdisk -l

## Create and Attach the 20GB Virtual Disk
## A clean VM is used with no secondary disk attached.

## Steps performed:

• 	Open VirtualBox → Select VM node5

• 	Go to Storage

• 	Click Add Hard Disk

• 	Click Create

• 	Set size to 20GB

• 	Finish and attach the disk

<img width="702" height="410" alt="Linux Storage Management - Part 1 pic 1" src="https://github.com/user-attachments/assets/28ce7553-a98e-4063-abce-986938019be9" />

<img width="570" height="412" alt="Linux Storage Management - Part 1 pic 2" src="https://github.com/user-attachments/assets/7c19ebb8-7560-4f77-9e72-0fd93ecda1a9" />

<img width="712" height="512" alt="Linux Storage Management - Part 1 pic 3" src="https://github.com/user-attachments/assets/3cd5f6c9-c97b-4576-b494-0398ff42cbbe" />

<img width="723" height="513" alt="Linux Storage Management - Part 1 pic 4" src="https://github.com/user-attachments/assets/47ec7739-f93b-4e94-b8c7-01001f85a77c" />

<img width="712" height="536" alt="Linux Storage Management - Part 1 pic 5" src="https://github.com/user-attachments/assets/4e1d4e9d-8380-4f2b-a9f6-870bffc99a88" />

<img width="713" height="542" alt="Linux Storage Management - Part 1 pic 6" src="https://github.com/user-attachments/assets/1fcdf6e9-7207-4f41-95ef-15e928807ca6" />

<img width="708" height="532" alt="Linux Storage Management - Part 1 pic 7" src="https://github.com/user-attachments/assets/dce82bc2-6415-4bbc-8df7-2fa66d091d54" />

<img width="718" height="517" alt="Linux Storage Management - Part 1 pic 8" src="https://github.com/user-attachments/assets/2635398b-f0ba-4407-8eef-2e4752fc7f78" />

## Verifying the new disk using lsblk before partitioning, confirm that /dev/sdb exists and is unpartitioned.

<img width="653" height="487" alt="Linux Storage Management - Part 1 pic 9" src="https://github.com/user-attachments/assets/25b381b5-bd66-4622-bf88-0c0691d091d5" />

## Launch fdisk on /dev/sdb

<img width="566" height="187" alt="Linux Storage Management - Part 1 pic 10" src="https://github.com/user-attachments/assets/8039dbaf-3354-4697-9760-e7217ab7ba5f" />

## 🧱 Partition creation, create primary partitions (sdb1, sdb2, sdb3)

## Creating sdb1

## Inside fdisk:

• 	Type n → new partition

• 	Type p → primary

• 	Accept default partition number

• 	Accept default first sector

• 	Set size: +4.4G

• 	Type t → change type

• 	Enter 8e → Linux LVM

• 	Type p → print table

• 	Type w → write changes

## Repeat the same process for sdb2 and sdb3.

<img width="637" height="708" alt="Linux Storage Management - Part 1 pic 11" src="https://github.com/user-attachments/assets/1d7379de-0615-4fe7-b8c6-12aa0f1369d2" />

<img width="682" height="652" alt="Linux Storage Management - Part 1 pic 12" src="https://github.com/user-attachments/assets/f602f2fa-1e65-4690-98a1-3c890fc3fac3" />

<img width="652" height="646" alt="Linux Storage Management - Part 1 pic 13" src="https://github.com/user-attachments/assets/6b54b0b1-69e4-4f85-aa69-fa12e9ae0375" />

## Create the Extended Partition (sdb4)

## Inside fdisk:

• 	Type n → new partition

• 	Type e → extended

• 	Accept defaults

• 	Do not specify a size (uses all remaining space)

• 	Type t → change type

• 	Enter 05 → Linux extended

## Important: The extended partition shows 1K in lsblk because it is a container, not a filesystem.

<img width="810" height="723" alt="Linux Storage Management - Part 1 pic 14" src="https://github.com/user-attachments/assets/bf31d452-27e9-4029-9bdf-944ead404fc8" />

<img width="697" height="340" alt="Linux Storage Management - Part 1 pic 15" src="https://github.com/user-attachments/assets/a86a39a9-ec48-4b1b-b419-d8ad2b35e0ea" />

## Create Logical Partitions (sdb5, sdb6)

## Logical partitions are created inside the extended partition.

## Inside fdisk:

• 	Type n → new partition

• 	Accept defaults

• 	Assign size (if needed)

• 	Type w → write changes

## Repeat for sdb6.

<img width="567" height="617" alt="Linux Storage Management - Part 1 pic 16" src="https://github.com/user-attachments/assets/35f3e7a5-d5f4-41a2-a796-51dedc771488" />

## 🔍 Verification

## Verify All Partitions Using 

<img width="710" height="386" alt="Linux Storage Management - Part 1 pic 17" src="https://github.com/user-attachments/assets/92e8a44f-925c-40bc-a55d-096203980a1d" />

## View Partition Table Using fdisk -l 

## This shows:

• 	True physical sizes

• 	Sector boundaries

• 	Partition types

• 	Extended partition container details

<img width="782" height="746" alt="Linux Storage Management - Part 1 pic 18" src="https://github.com/user-attachments/assets/71f889e4-aa41-4a9f-bbc2-f108b9922a05" />

## 📘 Partitioning Concepts (Summary)

## Primary Partitions

• 	A disk can have up to 3 primary partitions.

• 	One primary partition can be marked active for booting.

• 	Typically used for OS installations.

## Extended Partition

• 	Special type of primary partition.

• 	Allows creation of multiple logical partitions.

• 	Only one extended partition is allowed per disk.

## Logical Partitions

• 	Created inside the extended partition.

• 	Used when more than 3 partitions are needed.

• 	Linux numbers logical partitions starting at sdb5.

<img width="932" height="712" alt="Linux Storage Management - Part 1 pic 19" src="https://github.com/user-attachments/assets/323b2a0d-00ac-41ed-a70f-a2c2479bacb9" />

## 🎯 What I Learned

• 	How to safely create and manage partitions using fdisk

• 	Differences between primary, extended, and logical partitions

• 	Why logical partitions start at 5

• 	How Linux represents extended partitions as containers

• 	How to verify disk layouts using lsblk and fdisk -l

• 	How storage provisioning works in real Linux/DevOps environments

## 🌐 Why This Project Matter 

## This project builds foundational skills used in:

• 	Linux system administration

• 	Cloud engineering (AWS, Azure, GCP)

• 	DevOps pipelines

• 	LVM, RAID, and filesystem management

• 	Virtualization and infrastructure provisioning

## Understanding disk partitioning is essential for managing servers, configuring storage, and troubleshooting real‑world systems.
