# Ex-07: Linux-File-IO-Systems-locking
## AIM:
To Write a C program that illustrates files copying and locking

## DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux IO Systems locking

### Step 3:

Execute the C Program for the desired output. 

## PROGRAM:

### 1.To Write a C program that illustrates files copying 

~~~
#include <sys/stat.h>
#include <fcntl.h>
#include <stdlib.h>
int main()
{
char block[1024];
int in, out;
int nread;
in = open("filecopy.c", O_RDONLY);
out = open("file.out", O_WRONLY|O_CREAT, S_IRUSR|S_IWUSR);
while((nread = read(in,block,sizeof(block))) > 0)
write(out,block,nread);
exit(0);}
~~~
</br>

### OUTPUT
### C program that illustrates files copying

![326678919-bebfc9f4-d20f-46e1-bf0b-7d5a439b2eea](https://github.com/04Varsha/Linux-File-IO-Systems-locking/assets/149035374/f1fb0ce0-260d-4b95-baa4-15b33f30cdcc)

## 2.To Write a C program that illustrates files locking

~~~
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/file.h>
int main (int argc, char* argv[])
{ char* file = argv[1];
 int fd;
 struct flock lock;
 printf ("opening %s\n", file);
 /* Open a file descriptor to the file. */
 fd = open (file, O_WRONLY);
// acquire shared lock
if (flock(fd, LOCK_SH) == -1) {
    printf("error");
}else
{printf("Acquiring shared lock using flock");
}
getchar();
// non-atomically upgrade to exclusive lock
// do it in non-blocking mode, i.e. fail if can't upgrade immediately
if (flock(fd, LOCK_EX | LOCK_NB) == -1) {
    printf("error");
}else
{printf("Acquiring exclusive lock using flock");}
getchar();

if (flock(fd, LOCK_UN) == -1) {
    printf("error");
}else{
printf("unlocking");
}
getchar();
close (fd);
return 0;
}
~~~

</br>
</br>
</br>
</br>
</br>
</br>


### OUTPUT
### C program that illustrates files locking

![326678949-46738263-a92d-48e1-84ed-2fd056f31c5c](https://github.com/04Varsha/Linux-File-IO-Systems-locking/assets/149035374/8136f67c-a8a3-4523-aa73-a53988156cd5)


## RESULT:
The programs are executed successfully.
