# Hey! I'm Filing Here

In this lab I created a 1 MiB ext2 file system with 2 directories, 1 regular file, and 1 symbolic link. I created a root directory that contains another directory called "lost+found", a regular file called "hello-world", and a symbolic link called "hello" that points to "hello-world". The "hello-world" file is a 12 byte file that contains the string "Hello world\n".

Each of the directories created points to any child files, and contains hard links to itself and its parent. The project implements a block group, which contains a superblock, group descriptors, data block bitmap, inode bitmap, inode table, and data blocks. The code also writes "Hello world\n" to the "hello-world" file.

The superblock contains information about the whole file system, the group descriptors provide an overview of how the volume is split into block groups and where to find the inode bitmap, the block bitmap, and the inode table for each block group. The inode and block bitmaps state which blocks are free and used. The inode table contains information about the particular file (including user permissions and size allocation) and they point to the actual data blocks which are stored in the data region. In the case of the superblock, the path to the "hello-world" file is stored in the inode itself (with no data blocks).


## Building

To build a "ext2-create" executable, simply run the "make" command. Then run "./ext2-create" to create cs111-base.img (the file system). To mount the filesystem, create a directory called "mnt" with the command "mkdir mnt", then run "sudo mount -o loop cs111 -base.img mnt" to mount the file system.


## Running

Once the file system is created, run "dumpe2fs cs111 -base.img" to display all the information about the file system. The command "fsck.ext2 cs111 -base.img" can also be run to check that the file system is correct.

Once the file system is mounted, you can run the "ls -ain mnt/" command to output all the files, and their information, in the file system.

The command "python -m unittest" can also be run to check the file system against test cases specified in "test_lab4.py".


## Cleaning up

To unmount the file system, run "sudo umount mnt". Then remove the "mnt" directory with "rmdir mnt". To clean up the executable, run the "make clean" command.