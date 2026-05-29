# Buffer Cache
When the data is being written in disk, its not written instantly. Instead, to minimize the writes to the disks, firstly the data is kept as buffer cache. 

# Disk Drive Controller Cache
After writing in buffer cache, the file is again written in cache but of hardware level aka disk drive controller cache. The reason for cache is same as above but here, we have two types of category based on which data is written in disk:

### 1. write-through
as soon as the data arrives on cache, it is written on disks instantly.

### 2. write-back
when buffer reaches certain threshold, then only writes are written on disks or else is written slowly while also acknowledging the operation that the write is successful even though its not.

Most commercial drive are based on write-back because of the speed to complete the operation since the operation doesn't have to wait till every data is written in disk. Te drawback of it is that during the power cut, when energy backups isn't available, the data gets lost since cache is volatile mostly stays in RAM. Enterprise disks contains **Battery Backup Unit(BBU)** which powers the cache so that the data stays until the power comes backs. However, majority of consumer drives doesn't have this. ^9c14c6

# FSync
FSync is a way using which we can notify file system to persist all the data in the disk so that no data gets lost. In the case of consumer disk,  the way it operates is same as [[#1. write-through|Write-Through]] i.e. only sending acknowledgement to file system API initiator after all the data is persistent. Whereas, in the case of enterprises disk, since they have [[#^9c14c6|BBU]], the FSync can send ack directly to API initiator since it knows for certain that the operation will be written in the disk even if the architecture of disk is [[#2. write-back|Write-Back]].