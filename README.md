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

## Cleaning up

Unmount file system:

```sudo umount mnt```

Remove the directory named 'mnt' used for mounting:

```rmdir mnt ```
Clean binary files:
```
make clean ```
