# Linux Cheatsheet

## File System

### Navigation

| Command | Description                                                |
|---------|------------------------------------------------------------|
| ls      | List all the files in a directory                          |
| ls -l   | List all files and their details (owner, mtime, size, etc) |
| ls -a   | List all the files in a directory (including hidden files) |
| pwd     | Show the present working directory                         |
| cd      | Change directory to some other location                    |
| file    | View the type of any file                                  |

### Manage

| Command     | Description                                                              |
|-------------|--------------------------------------------------------------------------|
| mkdir       | Create a new directory                                                   |
| touch       | Create a new, empty file, or update the modified time of an existing one |
| cat > file  | Create a new file with the text you type after                           |
| cat file    | View the contents of a file                                              |
| grep        | View the contents of a file that match a pattern                         |
| nano file   | Open a file (or create new one) in nano text editor                      |
| vim file    | Open a file (or create new one) in vim text editor                       |
| rm or rmdir | Remove a file or empty directory                                         |
| rm -r       | Remove a directory that isn’t empty                                      |
| mv          | Move or rename a file or directory                                       |
| cp          | Copy a file or directory                                                 |
| rsync       | Synchronize the changes of one directory to another                      |

### Search

| Command     | Description                                                              |
|-------------|--------------------------------------------------------------------------|
| locate      | Quickly find a file or directory that has been cached                    |
| find        | Seach for a file or directory based on name and other parameters         |

### Hard Drive and Storage Commands

| Command          | Description                                            |
|------------------|--------------------------------------------------------|
| df or df -h      | See the current storage usage of mounted partitions    |
| sudo fdisk -l    | See information for all attached storage devices       |
| du               | See disk usage of a directory’s contents               |
| tree             | View the directory structure for a path                |
| mount and umount | Mount and unmount a storage device or ISO file         |

### Compression Commands

| Command                   | Description                                     |
|---------------------------|-------------------------------------------------|
| tar cf my_dir.tar my_dir  | Create an uncompressed tar archive              |
| tar cfz my_dir.tar my_dir | Create a tar archive with gzip compression      |
| gzip file                 | Compress a file with gzip compression           |
| tar xf file               | Extract the contents of any type of tar archive |
| gunzip file.gz            | Decompress a file that has gzip compression     |

### Networking Commands

| Command              | Description                                                     |
|----------------------|-----------------------------------------------------------------|
| ip a                 | Show IP address and other information for all active interfaces |
| ip r                 | Show IP address of default gateway                              |
| cat /etc/resolv.conf | See what DNS servers your system is configured to use           |
| ping                 | Send a ping request to a network device                         |
| traceroute           | Trace the network path taken to a device                        |
| ssh                  | Login to a remote device with SSH                               |

