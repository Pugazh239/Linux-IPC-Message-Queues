# Name : Pugazh sozhan.A

# Reg No : 212224240121


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

# Writer.c
```
#include <stdio.h> 
#include <sys/ipc.h> 
#include <sys/msg.h> 

struct mesg_buffer { 
	long mesg_type; 
	char mesg_text[100]; 
} message; 
int main() 
{ 	key_t key; 
	int msgid;
	key = ftok("progfile", 65); 
	msgid = msgget(key, 0666 | IPC_CREAT); 
	message.mesg_type = 1; 
	printf("Write Data : "); 
	gets(message.mesg_text); 
	msgsnd(msgid, &message, sizeof(message), 0); 
	printf("Data send is : %s \n", message.mesg_text); 
	return 0; 
}
```

# Reader.c
```
#include <stdio.h>
#include <sys/ipc.h>
#include <sys/msg.h>

struct mesg_buffer {
	long mesg_type;
	char mesg_text[100];
} message;
int main()
{
	key_t key;
	int msgid;
	key = ftok("progfile", 65);
	msgid = msgget(key, 0666 | IPC_CREAT);
	msgrcv(msgid, &message, sizeof(message), 1, 0);
	printf("Data Received is : %s \n",
			message.mesg_text);

	msgctl(msgid, IPC_RMID, NULL);
	return 0;
}
```

## OUTPUT

<img width="682" height="708" alt="image" src="https://github.com/user-attachments/assets/7e3a1523-016b-44a6-85cf-29c3bcd7a9d3" />


# RESULT:
The programs are executed successfully.
