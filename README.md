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
<img width="1380" height="768" alt="WhatsApp Image 2026-05-15 at 1 54 22 PM" src="https://github.com/user-attachments/assets/d5125c40-9e01-45c1-b102-8ad56c946bfc" />

# RESULT:
The programs are executed successfully.
