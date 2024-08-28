# Hey! I'm Filing Here

In this lab, I successfully implemented a 1 MiB ext2 file system. It has 2 directories (root, lost+found), 1 symbolic link (hello) and 1 regular file (hello-world). 

## Building

make

## Running

Run the executable to create cs111-base.img:

```./ext2-create```

Create directory named 'mnt' to mount filesystem to:
```mkdir mnt```

Mount filesystem:

```sudo mount -o loop cs111 -base.img mnt```
Dump filesystem information:

```dumpe2fs cs111 -base.img```
Result:
```

dumpe2fs 1.46.4 (18-Aug-2021)
Filesystem volume name:   cs111-base
Last mounted on:          <not available>
Filesystem UUID:          5a1eab1e-1337-1337-1337-c0ffeec0ffee
Filesystem magic number:  0xEF53
Filesystem revision #:    0 (original)
Filesystem features:      (none)
Default mount options:    (none)
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              128
Block count:              1024
Reserved block count:     0
Free blocks:              1000
Free inodes:              115
First block:              1
Block size:               1024
Fragment size:            1024
Blocks per group:         8192
Fragments per group:      8192
Inodes per group:         128
Inode blocks per group:   16
Last mount time:          n/a
Last write time:          Wed Aug 28 08:19:21 2024
Mount count:              0
Maximum mount count:      -1
Last checked:             Wed Aug 28 08:19:21 2024
Check interval:           1 (0:00:01)
Next check after:         Wed Aug 28 08:19:22 2024
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)


Group 0: (Blocks 1-1023)
  Primary superblock at 1, Group descriptors at 2-2
  Block bitmap at 3 (+2)
  Inode bitmap at 4 (+3)
  Inode table at 5-20 (+4)
  1000 free blocks, 115 free inodes, 2 directories
  Free blocks: 24-1023
  Free inodes: 14-128
```

Check filesystem is correct:
```fsck.ext2 cs111 -base.img```

Result:
```
e2fsck 1.46.4 (18-Aug-2021)
cs111-base has gone 0 days without being checked, check forced.
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
cs111-base: 13/128 files (0.0% non-contiguous), 24/1024 blocks
```
Result of ```ls -ain mnt```:

```
total 7
     2 drwxr-xr-x 3    0    0 1024 Aug 28 08:19 .
942647 drwxr-xr-x 6 1000 1000 4096 Aug 28 08:20 ..
    13 lrw-r--r-- 1 1000 1000   11 Aug 28 08:19 hello -> hello-world
    12 -rw-r--r-- 1 1000 1000   12 Aug 28 08:19 hello-world
    11 drwxr-xr-x 2    0    0 1024 Aug 28 08:19 lost+found
```
    
## Cleaning up

Unmount file system:

```sudo umount mnt```

Remove the directory named 'mnt' used for mounting:

```rmdir mnt ```

Clean binary files:
```
make clean ```
