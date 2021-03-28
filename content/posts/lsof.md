---
title: "Lsof"
date: 2020-06-28T11:29:52+01:00
showDate: true
draft: false
tags: ["unix","terminal"]
---

# Life in the Terminal - Volume 1

The terminal is the best friend of an application developer. There are multiple tools that can be piped together to extract meaningful insights for the problem at hand without developing a single line of code. 

Today we will be exploring lsof

# LSOF

## What is it?
`lsof` is a command line tool that can be used for analyzing files in a running system. The defintion of `file` is quite wide in the context of `lsof`e.g directories, text files, sockets or streams

## Display Running Files	
The simplest but not very meaningful exercise that we can do with `lsof` is listing all open files in a running system:

```
$ lsof
COMMAND     PID  USER          FD      TYPE   DEVICE    SIZE/OFF                NODE NAME
loginwind   143  georgios      cwd     DIR    1,5         640                   2 
```
The above command will produce a very long list which is not easy manageable by the human brain. 

We can split the list into multiple pages by leveraging the powerful `more` command:

```
$ lsof | more
COMMAND     PID  USER          FD      TYPE   DEVICE    SIZE/OFF                NODE NAME
loginwind   143  georgios      cwd     DIR    1,5         640                   2
:
```
You can press `:space` to see the next page.

## Understanding Output Columns
The above output contains multiple columns that might not make sense initially. 

By Looking at `man lsof`  it is straightforward to understand what all these magic numbers and acronyms are about. 

* COMMAND
This is the process name managing the open files
* PID
This is the id of the process managing the open files
* USER
This is the user running the current process
* FD
This is a more complex one if you have never come across file descriptors before. `FD` can be a number or a string describing the file descriptor. It can be one of these values:
```
cwd: current working directory;
Lnn: library references (AIX);
err: FD information error (see NAME column);
jld: jail directory (FreeBSD);
ltx: shared library text (code and data);
Mxx: hex memory-mapped type number xx.
m86: DOS Merge mapped file;
mem: memory-mapped file;
mmap: memory-mapped device;
pd: parent directory;
rtd: root directory;
tr: kernel trace file (OpenBSD);
txt: program text (code and data);
v86: VP/ix mapped file;
``` 
It can also be a cryptic number followed by some random characters. It might seem a bit random at the first sight but it is not:
	* The number defines the [file descriptor]([File descriptor - Wikipedia](https://en.wikipedia.org/wiki/File_descriptor)) 
	* The character that follows defines the access:
```
r: read
w: write
u: update
space: unknown
-: unknown locked
``` 
	* The next character that follows defines the lock type:
```
N: Solaris NFS lock of unknown type;
r: read lock on part of the file
R: a read lock on the entire file
w: write lock on part of the file
W: write lock on the entire file
u: read and write lock of any length
U: lock of unknown type
x: SCO OpenServer Xenix lock on part of the file
X: SCO OpenServer Xenix lock on the entire file
space: if there is no lock.
```
It is not very likely that you need these unless your use case is very very specific but just in case the explanation above must be sufficient.
* TYPE
In Unix-based systems everything is a file. Hard-drives, usb sticks, sockets or processing text, everything is backed by a file in our “favourite” Operating System. `TYPE` aims to explain what a listed `FD` is about.  The list here is endless. Use the following hacky command to get to the section of the `lsof` documentation listing all the different types:
`man lsof | grep -A 200 "       TYPE" | less`
* DEVICE
This column represents the device on which the file is attached or a hex address. If `DEVICE` value is a device then you can run `diskutil list`  on a osX machine to get a mapping between the integer you see under this column and the device that it represents. 
* SIZE/OFF
This is the size of the file or file offset in bytes. This is an optional value.
* NODE
Unix-based filesystems use a data structure to store filesystem objects. For typical filesystem files, the `NODE` represents the number of the said object. It can also be the Internet protocol type e.g `TCP` or `UDP` as well `STR` if the open file represents a stream. There are a couple of other available types that you will probably never need. 
* NAME
This is one of the most useful columns for most of the uses cases. It is actually the name/path of the open file.

## Finding Internet related Files using specific ports
So far, we have learnt that everything in UNIX-based systems are getting represented by files. An Internet connection wouldn’t differ. 
In order to find what process has allocated a specific port we can run the following command
```
$ lsof -i :8080
COMMAND   PID USER       FD   TYPE             DEVICE SIZE/OFF NODE NAME
java    39734 georgios  171u  IPv6 0x20964e8e5af3b6db      0t0  TCP *:http-alt (LISTEN)

```

Here, `-i` is being used to only consider internet related files. 

## Finding Open Files Managed by a Specific Executable
```
$ lsof -c java | less
COMMAND   PID USER       FD     TYPE             DEVICE  SIZE/OFF                NODE NAME
java    38866 georgios  cwd      DIR                1,5       672          8617079685 /Users/georgios/projects/...

```

This command aims to capture all the different open files that have been opened by a specific executable, in this particular example, the executable is `java`.
Have in mind that the command above might list open files managed by different processes that have all been started using the `java` executable.

## Finding which process manages an open file
This uses case is the reverse of the one above.  We do list all processes having open files within a certain directory (`+D`)
```
$ lsof +D "/tmp"
COMMAND    PID USER        FD   TYPE             DEVICE SIZE/OFF       NODE NAME
ssh-agent 2720 georgios    3u  unix 0x20964e8e45f0f84b      0t0            /private/tmp/...
``` 

These are some of the typical uses cases that I am using `lsof` for. I might come back with more of those but until then I am hoping that the above explanation is useful enough. 
