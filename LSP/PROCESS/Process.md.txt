1.Write a C program to demonstrate the use of fork() system call
 ```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>

int a=10; 

int main(void)
{
  int i;
  pid_t pid;
  printf("this is main function\n");
  pid=fork();
  if(pid < 0)
  {
    printf("Fork() system call is failed\n");
    exit(1);
  } 
  else if(pid == 0) 
  {
    printf("I am child process\n");
    for(i=0; i<10; i++)
    {
      a++;
    }
    printf("child process a value=%d\n",a);
    exit(10);
  }
  else              
  {
    printf("I am parent process\n");
    for(i=0; i<10; i++)
    {
      a--;
    }
    printf("parent process a value=%d\n",a);
    sleep(3);
  }
  printf("with in main=%d\n",a);
  return 0;
} 
```
2.Write a C program to illustrate the use of the execvp() function.
```c
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>

int main(void)
{
    char *args[] = {"ls", "-l", NULL}; 
    printf("Before execvp() call\n");
    // Replace current process image with ls -l
    if (execvp(args[0], args) == -1)
    {
      perror("execvp failed\n");
    }
    // This line will not execute if execvp() is successful
    printf("This will only print if execvp() fails\n");
    return 0;
}
3.Write a program in C to create a child process using fork() and print its PID.
```c
#include <stdio.h>
#include <unistd.h>
#include <sys/types.h>

int main(void)
{
  pid_t pid;
  pid = fork(); 
  if (pid < 0)
  {
    printf("Fork failed.\n");
    return 1;
  }
  else if (pid == 0)
  {
    printf("Child Process:\n");
    printf("Child PID=%d\n", getpid());
    printf("Parent PID=%d\n", getppid());
  }
  else
  {
   
    sleep(1);
    printf("Parent Process:\n");
    printf("Parent PID=%d\n", getpid());
    printf("Child PID=%d\n", pid);
  }
  return 0;
}
```
4. Write a C program to create multiple child processes using fork() and display their PIDs.                        
```c
#include<stdio.h>
#include<unistd.h>
#include<sys/types.h>
#include<sys/wait.h>

int main(void)
{
  int n, i;
  pid_t pid;
  printf("Enter number of child processes to create: ");
  scanf("%d", &n);
  for(i=0;i<n;i++)
  {
    pid = fork();
    if(pid < 0)
    {
      perror("fork failed");
      return 1;
    }
    else if(pid == 0)
    {
      printf("Child %d created with PID: %d : %d\n", i + 1, getpid(),getppid());
      return 0;  
    }
  }
  printf("parent PID: %d\n", getpid());
  for (i = 0; i < n; i++)
  {
    wait(NULL); 
  }
  return 0;
}

5. Write a program in C to create a zombie process and explain how to avoid it
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

#if 1
int main(void)
{
  pid_t pid=fork();
  if(pid < 0)
  {
    // Fork failed
    perror("fork");
    return 1;
  }
  else if(pid == 0)
  {
    // Child process
    printf("Child process (PID: %d) exiting...\n", getpid());
    exit(0);  // Exits immediately
  }
  else
  {
    // Parent process
    printf("Parent process (PID: %d) sleeping, child is now a zombie.\n", getpid());
    sleep(30);  // Keeps parent alive, child becomes zombie
    printf("Parent process exiting.\n");
  }
  return 0;
}
#endif

#if 0

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>  // Required for wait()

int main(void)
{
  pid_t pid = fork();
  if (pid < 0)
  {
    perror("Fork failed");
    return 1;
  }
  if (pid == 0)
  {
    // Child process
    printf("Child process (PID: %d) exiting.\n", getpid());
    exit(0);
  }
  else
  {
    // Parent process
    wait(NULL);  // Wait for child to terminate
    printf("Parent (PID: %d) reaped child. No zombie created.\n", getpid());
  }
  return 0;
}
#endif
```
6. Write a C program to demonstrate the use of the waitpid() function for process synchronization 
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>
int main(void)
{
  pid_t pid, wpid;
  int status;
  pid = fork();
  if(pid < 0)
  {
    perror("fork failed");
    exit(EXIT_FAILURE);
  }
  if (pid == 0)
  {
    // Child process
    printf("Child Process (PID: %d) is running...\n", getpid());
    sleep(3);  // Simulate work
    printf("Child Process (PID: %d) finished.\n", getpid());
    exit(42);  // Exit with custom status
  }
  else
  {
    // Parent process
    printf("Parent Process (PID: %d) is waiting for child (PID: %d)...\n", getpid(), pid);
    wpid = waitpid(pid, &status, 0);  // Wait for specific child
    if(wpid == -1)
    {
      perror("waitpid failed");
      exit(EXIT_FAILURE);
    }
    if (WIFEXITED(status))
    {
      printf("Child exited with status %d\n", WEXITSTATUS(status));
    }
    else
    {
      printf("Child did not terminate normally\n");
    }
    printf("Parent Process (PID: %d) continues...\n", getpid());
  }
  return 0;
}

7. Write a program in C to create a daemon process.
 
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main(void)
{
  pid_t pid, wpid;
  int status;
  pid = fork();
  if(pid < 0)
  {
    perror("fork failed");
    exit(EXIT_FAILURE);
  }
  if (pid == 0)
  {
    // Child process
    printf("Child Process (PID: %d) is running...\n", getpid());
    sleep(3);  // Simulate work
    printf("Child Process (PID: %d) finished.\n", getpid());
    exit(42);  // Exit with custom status
  }
  else
  {
    // Parent process
    printf("Parent Process (PID: %d) is waiting for child (PID: %d)...\n", getpid(), pid);
    wpid = waitpid(pid, &status, 0);  // Wait for specific child
    if(wpid == -1)
    {
      perror("waitpid failed");
      exit(EXIT_FAILURE);
    }
    if (WIFEXITED(status))
    {
      printf("Child exited with status %d\n", WEXITSTATUS(status));
    }
    else
    {
      printf("Child did not terminate normally\n");
    }
    printf("Parent Process (PID: %d) continues...\n", getpid());
  }
  return 0;
}
8. Write a C program to demonstrate the use of the system() function for executing shell  commands.
```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  int choice;
  while (1)
  {
    printf("\n--- Menu ---\n");
    printf("1. List files\n");
    printf("2. Show current directory\n");
    printf("3. Display date and time\n");
    printf("4. Exit\n");
    printf("Enter your choice: ");
    scanf("%d", &choice);
    getchar(); // To consume newline
    switch (choice)
    {
      case 1:
        system("ls -l");
        break;
      case 2:
        system("pwd");
        break;
      case 3:
        system("date");
        break;
      case 4:
        exit(0);
      default:
        printf("Invalid choice!\n");
    }
  }
  return 0;
}
```
9. Write a C program to create a process using fork() and pass arguments to the child process.
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(void) {
    pid_t pid;

    // Fork a child process
    pid = fork();

    if (pid < 0) {
        // Fork failed
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        // Child process
        printf("Child Process: PID = %d\n", getpid());

        // Command to execute
        char *args[] = {"pwd", NULL};

        // Replace the current process image with a new process image
        if (execvp(args[0], args) == -1) {
            perror("execvp failed");
            exit(EXIT_FAILURE);
        }
    } else {
        // Parent process
        printf("Parent Process: PID = %d, Child PID = %d\n", getpid(), pid);

        // Wait for the child process to complete
        int status;
        waitpid(pid, &status, 0);

        if (WIFEXITED(status)) {
            printf("Parent: Child exited with status %d\n", WEXITSTATUS(status));
        } else {
            printf("Parent: Child terminated abnormally.\n");
        }
    }

    return 0;
}
```
10. Write a program in C to demonstrate process synchronization using semaphores.
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/sem.h>
#include <sys/types.h>
#include <sys/wait.h>

// Define union semun if not defined
union semun
{
  int val;
  struct semid_ds *buf;
  unsigned short *array;
};

void sem_wait(int semid);
void sem_signal(int semid);

int main(void)
{
  key_t key = ftok("semfile", 65); // Unique key
  int semid = semget(key, 1, 0666 | IPC_CREAT); // Create semaphore

  union semun sem_union;
  sem_union.val = 1; // Initial value = 1
  semctl(semid, 0, SETVAL, sem_union);

  pid_t pid = fork();

  if (pid == 0)
  {
    // Child process
    sem_wait(semid);
    printf("Child entering critical section...\n");
    sleep(2); // Simulate critical section work
    printf("Child leaving critical section.\n");
    sem_signal(semid);
  }
  else
  {
    // Parent process
    sem_wait(semid);
    printf("Parent entering critical section...\n");
    sleep(2);
    printf("Parent leaving critical section.\n");
    sem_signal(semid);
    wait(NULL); // Wait for child to finish
    semctl(semid, 0, IPC_RMID); // Remove the semaphore
  }
  return 0;
}

void sem_wait(int semid)
{
  struct sembuf sb = {0, -1, 0}; // Decrement operation (P)
  semop(semid, &sb, 1);
}
void sem_signal(int semid)
{
  struct sembuf sb = {0, 1, 0}; // Increment operation (V)
  semop(semid, &sb, 1);
}

11. Write a C program to demonstraate the use of the execvpe() function
```c
#define _GNU_SOURCE  // Enable GNU extensions

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(void) {
    pid_t pid;

    pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } else if (pid == 0) {
        // Child process
        printf("Child Process: PID = %d\n", getpid());

        // Command and arguments
        char *args[] = {"env", NULL};

        // Custom environment
        char *envp[] = {
            "MY_VAR=HelloWorld",
            "USER=CustomUser",
            NULL
        };

        // Use execvpe (GNU-specific) to pass args and custom environment
        if (execvpe("env", args, envp) == -1) {
            perror("execvpe failed");
            exit(EXIT_FAILURE);
        }
    } else {
        // Parent process
        int status;
        waitpid(pid, &status, 0);

        if (WIFEXITED(status)) {
            printf("Parent: Child exited with status %d\n", WEXITSTATUS(status));
        } else {
            printf("Parent: Child terminated abnormally.\n");
        }
    }

    return 0;
}

```
12. Write a C program to create a process group and change its process group ID(PGID)
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/wait.h>

int main(void) {
    pid_t pid;

    pid = fork();

    if (pid < 0) {
        perror("Fork failed");
        exit(EXIT_FAILURE);
    } 
    else if (pid == 0) {
        // Child process
        printf("\n[Child] PID: %d, Original PGID: %d\n", getpid(), getpgrp());

        // Change PGID to its own PID, effectively creating a new process group
        if (setpgid(0, 0) == -1) {
            perror("setpgid failed");
            exit(EXIT_FAILURE);
        }

        printf("[Child] New PGID: %d\n", getpgrp());

        // Keep child alive for observation (optional)
        sleep(2);
        exit(EXIT_SUCCESS);
    } 
    else {
        // Parent process
        printf("\n[Parent] PID: %d, PGID: %d\n", getpid(), getpgrp());

        // Wait for child to complete
        wait(NULL);
        printf("[Parent] Child process finished.\n");
    }

    return 0;
}
```
13. Write a program in c to demonstrate inter-process communication using shared memory.
```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<sys/shm.h>
#include<sys/ipc.h>
#include<unistd.h>
#include<sys/wait.h>

int main(){
	key_t key=ftok("shmfile",65); // genertaing a key with ftok,( 65 is for projrct ID it may chuse between 1 t0 255
	int shmid = shmget(key, 1024, 0666|IPC_CREAT);
	pid_t pid = fork();
	if(pid>0){
		char *data=(char*)shmat(shmid,(void*)0,0);
		strcpy(data, "Hello Child");
		printf("Parent wrote: %s\n",data);
		shmdt(data);
		wait(NULL);
	}
	else if(pid ==0){
		sleep(1);
		char *data=(char*)shmat(shmid,(void*)0,0);
		printf("Child read: %s\n",data);
		shmctl(shmid, IPC_RMID,NULL);
	}
	else{
		printf("Fork failed \n");
	}
	return 0;
}
```
14. Develop a C program to copy the contents of all text files in a directory into a single file named "combined.txt"? 
```c
#include <stdio.h>
#include <dirent.h>
#include <string.h>
#include <stdlib.h>

int main(void) 
{
  DIR *dir;
  struct dirent *entry;
  FILE *src, *dest;
  char buffer[1024];
  dir = opendir(".");
  if (dir == NULL)
  {
    perror("Failed to open current directory");
    return 1;
  }
  dest = fopen("combined.txt", "w");
  if (dest == NULL)
  {
    perror("Failed to open combined.txt");
    closedir(dir);
    return 1;
  }
  while ((entry = readdir(dir)) != NULL)
  {
    if (strstr(entry->d_name, ".c") != NULL && strcmp(entry->d_name, "combined.txt") != 0)
    {
      src = fopen(entry->d_name, "r");
      if (src == NULL) 
      {
        perror("Failed to open source file");
        continue;
      }
      size_t n;
      while ((n = fread(buffer, 1, sizeof(buffer), src)) > 0)
      {	      
	fwrite(buffer, 1, n, dest);    
      }
      fclose(src);
    }
  }
  fclose(dest);
  closedir(dir);
  printf("All text files have been combined into combined.txt\n");
  return 0;
}
```
15. write a c program to create a child process using vfork() and demonstrate its usage.
```c
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>

int main(){
	pid_t pid;
	int x=5;
	printf("Before vfork, x=%d\n",x);

	pid=vfork();
	if(pid<0){
		perror("vfork failed");
		exit(1);
	}
	else if(pid == 0){
		x+=5;
		printf("Chind process: x=%d\n",x);
		_exit(0);
	}else{
		printf("Parent process: x=%d\n",x);
	}
	return 0;
}
```
16. Write a c program to create a pipeline between two process using the pipe() system call.
```c
#include<stdio.h>
#include<unistd.h>
#include<string.h>
#include<stdlib.h>

int main()
{
	int pipefd[2];
	pid_t pid;
	char buffer[100];

	if(pipe(pipefd)==-1){
		perror("Pipes failed");
		return 1;
	}
	pid=fork();
	if(pid<0){
		perror("Forl failed");
		return 1;
	}else if(pid>0){
		close(pipefd[0]);
		char message[]="Hello from parent";
		write(pipefd[1],message,strlen(message)+1);
		close(pipefd[1]);
	}else{
		close(pipefd[1]);
		read(pipefd[0],buffer,sizeof(buffer));
		printf("Child recevied: %s\n", buffer);
	}
	return 0;
}

```
17. Write a c program to demonstrate the use of the nice() system call for adjusting process priority.
```c
#include<stdio.h>
#include<unistd.h>
#include<sys/time.h>
#include<sys/resource.h>
#include<stdlib.h>
#include<errno.h>
int main(){
	int priority;
	printf("Original priority:%d\n", getpriority(PRIO_PROCESS,0));
	priority=nice(5);
	if(priority==-1&&errno!=0){
		perror("nice");
		exit(EXIT_FAILURE);
	}
	printf("New priority after nice(5): %d\n", getpriority(PRIO_PROCESS,0));

		for(int i=0;i<5;i++){
	printf("Running at priority: %d\n",getpriority(PRIO_PROCESS,0));
		sleep(1);
	}
  return 0;
}
```
18. write a c program to demonstrate the use of the clone() system call to create a thread
```c
#define _GNU_SOURCE //to unlock GNU-specific extensions
#include<sched.h>
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/wait.h>

//#define _GNU_SOURCE

int thread_func(void *arg){
	printf("Child thread: Received argument: %s\n",(char*)arg);
	printf("Child thread: PID=%d, PPID= %d\n",getpid(),getppid());
	return 0;
}

int main(){
	char *stack;
	char *stackTop;
	const int stackSize=1024*1024;//1MB stack
	char *message = "Hello from clone";

	stack = malloc(stackSize);
	if(!stack){
		perror("malloc");
		exit(1);
	}
	stackTop=stack+stackSize;

	pid_t pid=clone(thread_func,stackTop,SIGCHLD,message);
	if(pid==-1){
		perror("clone");
		free(stack);
		exit(1);
	}
	waitpid(pid,NULL,0);
	printf("Parent process: Child has terminated\n");
	free(stack);
	return 0;
}
```
19. Write a c program to create a child process using fork() and communicate between parent and child pipes
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<string.h>
#include<sys/types.h>
#include<sys/wait.h>

int main(){
	int pipe1[2]; //Parent -> Child
	int pipe2[2]; //Child -> Parent
	int child;
	char parent_msg[]=" Hi this is parent";
	char child_msg[]=" Hi this is child";
	char buffer[100];

	if(pipe(pipe1)==-1||pipe(pipe2)==-1){
		perror("Pipe creation failed");
		return 1;
	}

	pid_t pid=fork();

	if(pid<0){
		printf("Child creaction failes\n");
		return 1;
	}
	else if(pid==0){
		close(pipe1[1]);
		close(pipe2[0]);
		printf("child created\n");
		read(pipe1[0],buffer,sizeof(buffer));
		printf("child resived data from parent: %s\n",buffer);
		write(pipe2[1],child_msg,strlen(child_msg)+1);
		close(pipe1[0]);
		close(pipe2[1]);
		return 0;
	}
	else{
		close(pipe1[0]);
		close(pipe2[1]);
		write(pipe1[1],parent_msg,strlen(parent_msg)+1);
		close(pipe1[1]);
		memset(buffer, 0, sizeof(buffer));
		read(pipe2[0],buffer,sizeof(buffer));
		printf("Parent received: %s\n", buffer);
		//close(pipe1[1]);
		close(pipe2[0]);
		wait(NULL);
	}
	return 0;
}
```
20. Write a C program to create a process using fork() and change its scheduling policy using sched_setscheduler()
```c
#define _GNU_SOURCE
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sched.h>
#include<sys/types.h>
#include<sys/wait.h>
#include<errno.h>
#include<string.h>

int main(){
	pid_t pid;
	struct sched_param schedParm;

	pid = fork();

	if(pid<0){
		perror("fork failed\n");
		return 1;
	}
	else if(pid==0){
		printf("Child PID=%d\n",getpid());

		schedParm.sched_priority=20;

		if(sched_setscheduler(0, SCHED_RR,&schedParm)==-1){
			perror("sched_setscheduler failed");
		}else{
			printf("Child: Scheduling policy changes to SCHED_RR\n");
		}

		for(int i=0;i<5;i++){
			printf("Child: working...[%d]\n",1);
			sleep(1);
		}
		_exit(0);
	}	
		else{
			wait(NULL);
			printf("parent: Child finished\n");
	
	}
	return 0;
}
```
21. write a C program to create a child process using fork() and demonstrate IPC using shared memory
```c
#include<stdio.h>
#include<stdlib.h>
#include<sys/ipc.h>
#include<sys/shm.h>
#include<string.h>
#include<unistd.h>
#include<sys/wait.h>

int main(){
	key_t key = ftok("shmfile",65);

	int shmid=shmget(key,1024,0666|IPC_CREAT);

	pid_t pid=fork();

	if(pid<0){
		perror("Fork failed");
		return 1;
	}else if(pid==0){
		sleep(1);
		char *data = (char *)shmat(shmid,(void *)0,0);
		printf("Child read: %s\n", data);
		shmdt(data);
	}else{
		char *data =(char *)shmat(shmid,(void *)0,0);
		strcpy(data, "Hello from parent");
		printf("Parent wrote to shared memory\n");
		shmdt(data);
		wait(NULL);
		shmctl(shmid, IPC_RMID,NULL);
	}
	return 0;
}
```
23. Write a C program to demonstrate the use of the prctl() system call to change process attributes
```c
#define _GNU_SOURCE
#include<stdlib.h>
#include<stdlib.h>
#include<stdio.h>
#include<sys/prctl.h>
#include<string.h>
#include<unistd.h>

int main(){
	const char *new_name ="MyProcess";
	char name[17];

	if(prctl(PR_SET_NAME,(unsigned long)new_name, 0, 0, 0)==-1){
		strerror("prctl(PR_SET_NAME) failed");
		return 1;
	}

	printf("Process name set to: %s\n", new_name);

	if(prctl(PR_GET_NAME,(unsigned long)name, 0,0,0)==-1){
		perror("prctl(PR_GET_NAME) failed");
		return 1;
	}
	printf("Process name retrived: %s\n", name);
	sleep(10);
	return 0;
}
```        
24. Write a C program to create a child process using fork() and demonstrate process synchronization using semaphores
```c
#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<sys/ipc.h>
#include<sys/sem.h>
#include<sys/wait.h>

union semun{
	int val;
	struct semid_ds *buf;
	unsigned short *array;
};

void wait_semaphore(int semid){
	struct sembuf sb={0, -1, 0};
	semop(semid, &sb,1);
}

void signal_semaphore(int semid){
	struct sembuf sb={0,1,0};
	semop(semid, &sb, 1);
}

int main(){
	key_t key = ftok("semfile", 65);
	int semid=semget(key,1, 0666|IPC_CREAT);

	if(semid==-1){
		perror("semget failed");
		exit(1);
	}
union semun u;
u.val=1;
semctl(semid, 0, SETVAL, u);

pid_t pid=fork();

if(pid<0){
	perror("fork failed");
	exit(1);
}
else if(pid==0){
	for(int i=0;i<5;i++){
		wait_semaphore(semid);
		printf("Child: iteration %d\n",i+1);
		sleep(1);
		signal_semaphore(semid);
	}
	exit(0);
}else{
	for(int i= 0;i<5;i++){
		wait_semaphore(semid);
		printf("Parent: iteration %d\n",i+1);
		sleep(1);
		signal_semaphore(semid);
	}
	wait(NULL);
	semctl(semid,0,IPC_RMID);
}
return 0;
}
```
25. Wrirte a c program to creat a child process using fork() and demonstrate process communication using message queues
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/ipc.h>
#include <sys/msg.h>
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>

struct msg_buffer {
    long msg_type;
    char msg_text[100];
};

int main() {
    key_t key;
    int msgid;
    struct msg_buffer message;

    key = ftok("msgfile", 65);

    msgid = msgget(key, 0666 | IPC_CREAT);
    if (msgid == -1) {
        perror("msgget failed");
        exit(1);
    }

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    } else if (pid == 0) {

        msgrcv(msgid, &message, sizeof(message.msg_text), 1, 0);
        printf("Child received: %s\n", message.msg_text);


        msgctl(msgid, IPC_RMID, NULL);
    } else {

        message.msg_type = 1;
        strcpy(message.msg_text, "Hello from parent!");
        msgsnd(msgid, &message, sizeof(message.msg_text), 0);
        wait(NULL);
    }

    return 0;
}
```

26 Write a C program to create a child process using fork() and demonstrate process synchronization using condition variables
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <pthread.h>
#include <sys/mman.h>
#include <sys/wait.h>

typedef struct {
    pthread_mutex_t mutex;
    pthread_cond_t cond;
    int flag;
} shared_t;

int main() {
   
    shared_t *data = mmap(NULL, sizeof(shared_t),
                          PROT_READ | PROT_WRITE,
                          MAP_SHARED | MAP_ANONYMOUS,
                          -1, 0);

    
    pthread_mutexattr_t mattr;
    pthread_condattr_t cattr;
    pthread_mutexattr_init(&mattr);
    pthread_condattr_init(&cattr);
    pthread_mutexattr_setpshared(&mattr, PTHREAD_PROCESS_SHARED);
    pthread_condattr_setpshared(&cattr, PTHREAD_PROCESS_SHARED);
    pthread_mutex_init(&data->mutex, &mattr);
    pthread_cond_init(&data->cond, &cattr);
    data->flag = 0;

    pid_t pid = fork();

    if (pid == 0) {
        sleep(1);
        pthread_mutex_lock(&data->mutex);
        data->flag = 1;
        printf("Child: sending signal to parent\n");
        pthread_cond_signal(&data->cond);
        pthread_mutex_unlock(&data->mutex);
        exit(0);
    } else {

        pthread_mutex_lock(&data->mutex);
        while (data->flag == 0) {
            printf("Parent: waiting for signal...\n");
            pthread_cond_wait(&data->cond, &data->mutex);
        }
        pthread_mutex_unlock(&data->mutex);
        printf("Parent: received signal from child\n");
        wait(NULL);
    }

    return 0;
}
```

27. write a C program to creat a child process using fork() and demonstrate process communication using named pipes(FIFOs)
```c
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <fcntl.h>
#include <sys/stat.h>
#include <sys/types.h>
#include <string.h>
#include <sys/wait.h>

#define FIFO_PATH "/tmp/myfifo"

int main() {
    pid_t pid;
    char message[] = "Hello from parent via FIFO!";
    char buffer[100];

    if (mkfifo(FIFO_PATH, 0666) == -1) {
        perror("mkfifo");
    }

    pid = fork();

    if (pid < 0) {
        perror("fork failed");
        exit(1);
    } else if (pid == 0) {
        int fd = open(FIFO_PATH, O_RDONLY);
        if (fd == -1) {
            perror("Child: open FIFO for reading");
            exit(1);
        }
        read(fd, buffer, sizeof(buffer));
        printf("Child received: %s\n", buffer);
        close(fd);
        exit(0);
    } else {
        int fd = open(FIFO_PATH, O_WRONLY);
        if (fd == -1) {
            perror("Parent: open FIFO for writing");
            exit(1);
        }
        write(fd, message, strlen(message) + 1);
        close(fd);
        wait(NULL);
        unlink(FIFO_PATH);
    }

    return 0;
}
```
29. Write a C program to create a child process using fork() and demonstrate process communication using shared memory and semaphores
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/ipc.h>
#include <sys/shm.h>
#include <sys/sem.h>
#include <sys/wait.h>


union semun {
    int val;
    struct semid_ds *buf;
    unsigned short *array;
};

int main() {
    key_t shm_key = ftok("shmfile", 65);
    key_t sem_key = ftok("semfile", 75);

    int shmid = shmget(shm_key, 1024, 0666 | IPC_CREAT);
    if (shmid == -1) {
        perror("shmget");
        exit(1);
    }

    int semid = semget(sem_key, 1, 0666 | IPC_CREAT);
    if (semid == -1) {
        perror("semget");
        exit(1);
    }

    union semun sem_arg;
    sem_arg.val = 0;
    semctl(semid, 0, SETVAL, sem_arg);

    pid_t pid = fork();

    if (pid < 0) {
        perror("fork");
        exit(1);
    } else if (pid == 0) {
        struct sembuf sb = {0, -1, 0};
        semop(semid, &sb, 1);

        char *data = (char *)shmat(shmid, NULL, 0);
        printf("Child read from shared memory: %s\n", data);
        shmdt(data);
        exit(0);
    } else {
        char *data = (char *)shmat(shmid, NULL, 0);
        strcpy(data, "Hello from parent!");
        shmdt(data);

        struct sembuf sb = {0, 1, 0};
        semop(semid, &sb, 1);

        wait(NULL);
	// cleanup
        shmctl(shmid, IPC_RMID, NULL);
        semctl(semid, 0, IPC_RMID);
        printf("Parent: communication complete.\n");
    }

    return 0;
}
```
