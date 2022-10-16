# Build
## Ubuntu 22.04 x64
1. sudo apt install qemu-system-x86
2. make
3. make qemu
4. If get the following error:
```
gcc -fno-pic -static -fno-builtin -fno-strict-aliasing -O2 -Wall -MD -ggdb -m32 -Werror -fno-omit-frame-pointer -fno-stack-protector -fno-pie -no-pie   -c -o usertests.o
usertests.c

usertests.c: In function ‘sbrktest’:
usertests.c:1461:13: error: writing 1 byte into a region of size 0 [-Werror=stringop-overflow=]
 1461 |   *lastaddr = 99;
 ```
 compiler again by remove ```-Werror```:
 ```
 gcc -fno-pic -static -fno-builtin -fno-strict-aliasing -O2 -Wall -MD -ggdb -m32 -fno-omit-frame-pointer -fno-stack-protector -fno-pie -no-pie   -c -o usertests.o usertests.c
 make qemu
 ```
 
 # Run on VirtualBox
 ## Windows 11
 1. change .img to .vdi
 ```
 C:\Program' 'Files\Oracle\VirtualBox\VBoxManage convertfromraw --format VDI .\xv6.img .\xv6.vdi
 C:\Program' 'Files\Oracle\VirtualBox\VBoxManage convertfromraw --format VDI .\fs.img .\fs.vdi
 ```
 2. Create Virtual Machine, choose ```type: Linux and version: Other Linux (32 bit)```

 <img src="picture/virtualbox_xv6.png"></img>

 3. In Settings, enable ```I/O APIC```
 
 <img src="picture/enable_APIC.png"></img>
 
 4. In Settings, add xv6.vdi and fs.vdi in IDE
 
 <img src="picture/add_IDE.png"></img>
 
 System call Description:
 ```
fork() Create a process
exit() Terminate the current process
wait() Wait for a child process to exit
kill(pid) Terminate process pid
getpid() Return the current process’s pid
sleep(n) Sleep for n clock ticks
exec(filename, *argv) Load a file and execute it
sbrk(n) Grow process’s memory by n bytes
open(filename, flags) Open a file; the flags indicate read/write
read(fd, buf, n) Read n bytes from an open file into buf
write(fd, buf, n) Write n bytes to an open file
close(fd) Release open file fd
dup(fd) Duplicate fd
pipe(p) Create a pipe and return fd’s in p
chdir(dirname) Change the current directory
mkdir(dirname) Create a new directory
mknod(name, major, minor) Create a device file
fstat(fd) Return info about an open file
link(f1, f2) Create another name (f2) for the file f1
unlink(filename) Remove a file
```
Figure 0-2. Xv6 system calls
