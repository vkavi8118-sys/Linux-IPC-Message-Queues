# Linux-IPC-Message-Queues
Linux IPC-Message Queues

# AIM:
To write a C program that receives a message from message queue and display them

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux message queues API 

### Step 3:

Execute the C Program for the desired output. 

# PROGRAM:

## C program that receives a message from message queue and display them
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

struct msg_buffer {
    long msg_type;
    char msg_text[100];
} message;

int main() {
    key_t key = ftok("progfile", 65);
    int msgid = msgget(key, 0666 | IPC_CREAT);
    message.msg_type = 1;

    printf("Enter Message: ");
    fgets(message.msg_text, 100, stdin);

    msgsnd(msgid, &message, sizeof(message), 0);
    printf("Sent: %s", message.msg_text);

    return 0;
}
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

struct msg_buffer {
    long msg_type;
    char msg_text[100];
} message;

int main() {
    key_t key = ftok("progfile", 65);
    int msgid = msgget(key, 0666 | IPC_CREAT);

    printf("Waiting for message...\n");
    msgrcv(msgid, &message, sizeof(message), 1, 0);

    printf("Received: %s", message.msg_text);
    msgctl(msgid, IPC_RMID, NULL); // Deletes the queue after reading

    return 0;
}



## OUTPUT
<img width="489" height="401" alt="VirtualBox_Parrot Security 6 0_15_05_2026_13_37_33" src="https://github.com/user-attachments/assets/7946d2e6-24de-49b6-9584-9dd7e41e7dd1" />

# RESULT:
The programs are executed successfully.
