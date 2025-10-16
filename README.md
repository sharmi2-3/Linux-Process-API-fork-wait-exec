# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## 1.C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}
```













## OUTPUT

<img width="308" height="128" alt="Screenshot 2025-10-15 211644" src="https://github.com/user-attachments/assets/33aaabab-0ba9-4fdf-92c8-75ce07c005c1" />










## 2.C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
```
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
int main()
{       int status;
        printf("Running ps with execlp\n");
        execl("ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
printf("Running ps with execlp. Now with path specified\n");
        execl("/bin/ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                puts("child did not exit successfully\n");
        printf("Done.\n");
        exit(0);}
```


























## OUTPUT


<img width="404" height="352" alt="Screenshot 2025-10-15 212419" src="https://github.com/user-attachments/assets/e6f465aa-a7a2-4d96-a485-0d1ff79e3e9d" />
<img width="320" height="343" alt="Screenshot 2025-10-15 212656" src="https://github.com/user-attachments/assets/748499ce-b41a-4c13-b5a4-2ad4aa54fc05" />
<img width="398" height="442" alt="Screenshot 2025-10-15 212719" src="https://github.com/user-attachments/assets/3481e50a-0507-4b94-a890-8bf49b235908" />
<img width="543" height="428" alt="Screenshot 2025-10-15 212741" src="https://github.com/user-attachments/assets/28205889-719a-41e7-bd07-a896e3f261f3" />
<img width="538" height="415" alt="Screenshot 2025-10-15 212852" src="https://github.com/user-attachments/assets/442203f5-377e-43a6-bd2f-985580aabaca" />
<img width="456" height="376" alt="Screenshot 2025-10-15 213136" src="https://github.com/user-attachments/assets/dc195e13-02df-42af-8f86-0d91411814b4" />


## 3. C Program to execute Linux system commands using Linux API system calls exec() family

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}
```

## OUTPUT

![WhatsApp Image 2025-10-16 at 08 13 31_f4a56625](https://github.com/user-attachments/assets/63fafe4a-048c-4566-a321-8df11d1050f1)




























# RESULT:
The programs are executed successfully.
