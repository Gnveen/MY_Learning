# Files

1.Write a C program to create a new text file and write user input to it
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(void)
{
  int fd,ref,len;
  char buf[100];
  printf("Enter a string:\n");
  scanf("%[^\n]",buf);           // be careful while using this format specifier --string length <= size-1
  len=strlen(buf);
  printf("%d\n",len);
  fd=open("file.txt",O_CREAT|O_RDWR|O_TRUNC,0666); 
  printf("%d\n",fd);                                
  if(fd<0){
    printf("open system call failed\n");
    return 0;
  }
  ref=write(fd,buf,strlen(buf));                //write system return number of bytes written
  printf("%d\n",ref);
  if(ref<0)                                    // write system call return -1 write system call is failed
  {
    printf("Write system call is failed\n");
    return 0;
  }
  close(fd);                      //  close fd other than next runtime open system call fails
  return 0;
}
```
2.Develop a C program to open an existing text file and display its contents
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(){}
  int fd,ref,len;
  char buf[100];
  fd=open("file.txt",O_RDWR,0666);
  if(fd<0){
    printf("open system call failed\n");
    return 0;
  }
  while((ref=read(fd, buf, sizeof(buf)-1))>0){
    buf[ref]='\0';
    printf("%s",buf);
  }
  if(ref<0){
    printf("red failed\n");
    close(fd);
    return 1;
 }
close(fd);
return 0;
  }
```
3.Implement a C program to create a new directory named "Test" in the current-dir? 
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <stdio.h>
#include <direct.h>  // For Windows
#include <errno.h>
int main() {
    int status;
    status = _mkdir("Test");  // Create directory named "Test"
    if (status == 0) {
        printf("Directory 'Test' created successfully.\n");
    } else {
        perror("Error creating directory");
    }
    return 0;
}
```
4.Write a C program to check if a file named "sample.txt" exists in the current directory?
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
int main(){
  if(access("Tes",F_OK)==0){
    printf("File is present\n");
  }
  else{
    perror("No such file found");
  }
  return 0;
}
```
5. Develop a C program to rename a file,dir, from "oldname.txt" to "newname.txt"? 
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
int main(){
  if(rename("Test","new")==0){
    printf("File renamed");
  }
  else{
    perror("Error file");
  }
  return 0;
}
```
6. Implement a C program to delete a file named "delete_me.txt"?
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(){
  if(remove("q2.c")==0){
    printf("file removed");
  }
  else{
    printf("fai to remove");
  }
  return 0;
}
```
7. Write a C program to copy the contents of one file to another? 
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main() {
    int src_fd, des_fd, rd_ref, wt_ref;
    char buf[100];
    src_fd = open("file.txt", O_RDONLY);
    printf("src_fd = %d\n", src_fd);
    if (src_fd < 0) {
        perror("Failed to open source file");
        return 1;
    }
    des_fd = open("des_file.txt", O_CREAT | O_WRONLY | O_TRUNC, 0666);
    printf("des_fd = %d\n", des_fd);
    if (des_fd < 0) {
        perror("Failed to open destination file");
        close(src_fd);
        return 1;
    }
    while ((rd_ref = read(src_fd, buf, sizeof(buf))) > 0) {
        wt_ref = write(des_fd, buf, rd_ref);
        if (wt_ref != rd_ref) {
            perror("Write system call failed");
            close(src_fd);
            close(des_fd);
            return 1;
        }
    }
    if (rd_ref == 0) {
        printf("Read completed successfully.\n");
    } else {
        perror("Read system call failed");
        close(src_fd);
        close(des_fd);
        return 1;
    }
    close(src_fd);
    close(des_fd);
    return 0;
}
```
8. Develop a C program to move a file from one directory to another?
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(){
  char *old_path="src_file.txt";
  char *new_path="../destination/des.txt";
  if(rename(old_path,new_path)==0){
    printf("File moved successfully\n");
  }
  else{
    perror("moving failed");
  }
    return 0;
}
```
9. Implement a C program to list all files in the current directory
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <dirent.h>
int main() {
    struct dirent *dir_entry;
    DIR *dir_stream = opendir(".");
    if (dir_stream == NULL) {
        perror("Could not open current directory");
        return 1;
    }
    printf("Files in the current directory:\n");
    while ((dir_entry = readdir(dir_stream)) != NULL) {
        printf("%s\n", dir_entry->d_name);
    }
    closedir(dir_stream);
    return 0;
}
```
10. Write a C program to get the size of a file named "file.txt"?     
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <stdlib.h>
#include <sys/stat.h> //The stat() function in C is used to retrieve information about a file or directory details like file size, permissions, timestamps, and type
int main() {
    struct stat file_stat;
    if (stat("file.txt", &file_stat) == -1) {
        perror("stat failed");
        return 1;
    }
    printf("Size of file = %ld bytes\n", file_stat.st_size);
    return 0;
}
```
11.program to check if a directory named exist in the current directory
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <sys/stat.h>
#include <sys/types.h>
int main(){
  struct stat st;
  if(stat("new",&st)==0 && S_ISDIR(st.st_mode)){ //S_ISDIR(st.st_mode) is a macro in C that checks whether a given file mode corresponds to a directory.
    printf("Directory Existed\n");
  }
  else{
    printf("Directory not existed\n");
  }
  return 0;
}
```
12.creat a new dir named "Backup"
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <direct.h>
int main() {
    int status = _mkdir("Backup"); // for creating in pwd, if like to creat in previous dir use ../file_name
  
    if (status == 0) {
        printf("Directory created successfully\n");
    } else {
        perror("Failed to create directory");
    }

    return 0;
}
```
13. Write a C program to recursively list all files and directories in a given directory? 
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <dirent.h>
#include <sys/stat.h>
void listfl(const char *basepath) {
    char path[1000];
    struct dirent *dp;
    DIR *dir = opendir(basepath); // DIR is data type for file handling
    if (!dir) {
        perror("Failed to open directory"); // Handle error
        return;
    }
    while ((dp = readdir(dir)) != NULL) { // Read directory contents
        if (strcmp(dp->d_name, ".") == 0 || strcmp(dp->d_name, "..") == 0)
            continue;
        snprintf(path, sizeof(path), "%s/%s", basepath, dp->d_name);
        printf("%s\n", path);
        struct stat statbuf;
        if (stat(path, &statbuf) == 0 && S_ISDIR(statbuf.st_mode)) {
            listfl(path); // Recursive call for subdirectory
        }
    }
    closedir(dir); // Close directory
}
int main() {
    const char *path = ".";
    printf("Listing files in: %s\n", path);
    listfl(path);
    return 0;
}
```
14. Develop a C program to delete all files in a directory named "Temp"?
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <dirent.h>
int main() {
    const char *dir_path = "./new";
    DIR *dir = opendir(dir_path);
    struct dirent *entry;
    char filepath[1024];
    struct stat statbuf;
    if (!dir) {
        perror("Unable to open directory");
        return 1;
    }
    while ((entry = readdir(dir)) != NULL) {
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;
        snprintf(filepath, sizeof(filepath), "%s/%s", dir_path, entry->d_name);
        if (stat(filepath, &statbuf) == 0 && S_ISREG(statbuf.st_mode)) {  // Correct field name
            if (remove(filepath) == 0)
                printf("Deleted file: %s\n", filepath);
            else
                perror("Failed to delete");
        }
    }
    closedir(dir);
    return 0;
}
```
15. prg to count the number of lines in a file
```
int main(){
  FILE *fp;
  char ch;
  int ln_count=0;
  fp=fopen("file.txt","r");
  if(fp==NULL){
    perror("Error to open");
    return 1;
  }
  while((ch=fgetc(fp))!=EOF){
      if(ch=='\n'){
      ln_count++;
    }
  }
  fclose(fp);
  printf("Total num:%d\n", ln_count+1);
  return 0;
}
```
16. c prg to append "Goodbye" to the end of an existing file,
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(){
  FILE *fd;
  fd=fopen("file.txt","a");
  if(fd==NULL){
    perror("Error to open");
    return 1;
  }
  fprintf(fd,"Good bye\n");
  fclose(fd);
  printf("Text appended\n");
  return 0;
}
```
17. c program to change the permission of a file,
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(){
  const char *fnam="file.txt";
  if(chmod(fnam,0444)==0)
  printf("permission changed to read only\n");
  else{
    perror("Failed to change permissions");
    return 1;
  }
  return 1;
}
```
18 Write a C program to change the ownership of a file named "file.txt"  to the user "user1"?   
```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <unistd.h>
#include <pwd.h>

int main(void) 
{
  const char *filename = "hi.txt";
  const char *username = "user1";
  struct passwd *pw = getpwnam(username); //user account information
  if (pw == NULL) 
  {
    perror("User not found");
    return 1;
  }
  // Change owner to user1, keep group unchanged (-1)
  if (chown(filename, pw->pw_uid, -1) == 0)   //pw_uid
  {
    printf("Ownership changed to '%s' successfully.\n", username);
  }
  else
  {
    perror("Failed to change file ownership");
     return 1;
  }
  return 0;
}
```
19. Develop a C program to get the last modified timestamp of a file named "file.txt"?
```
#include<sys/stat.h>
#include<time.h>
int main(){
  const char *filename="file.txt";
  struct stat file_stat;
  if(stat(filename,&file_stat)==-1){
    perror("stat");
    return 0;
  }
  printf("last modified time of %s:%s",filename,ctime(&file_stat.st_mtime));
  return 0;
}
```
20. creat a temporary file and write some data to it?
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
int main(){
  FILE *temp_file=tmpfile();
  if(temp_file==NULL){
    perror("Failed to create temp file");
    return 1;
  }
  const char *data ="This is temp \n";
  fputs(data,temp_file);
  char buffer[100];
  printf("Reading from temp:\n");
  while(fgets(buffer,sizeof(buffer),temp_file)!=NULL){
    printf("%s",buffer);
  }
  sleep(100);
fclose(temp_file);
return 0;
}
```
21. Write a C program to check if a given path refers to a file or a directory? 
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <sys/stat.h>
int main() {
    const char *path = "file.txt"; // Change this path as needed
    struct stat st;
    int fd = open(path, O_RDONLY);
    if (fd == -1) {
        perror("Failed to open path");
        return 1;
    }
    if (fstat(fd, &st) == -1) {
        perror("fstat failed");
        close(fd);
        return 1;
    }
    if (S_ISREG(st.st_mode)) {
        printf("'%s' is a regular file.\n", path);
    } else if (S_ISDIR(st.st_mode)) {
        printf("'%s' is a directory.\n", path);
    } else {
        printf("'%s' is neither a regular file nor a directory.\n", path);
    }
    close(fd);
    return 0;
}
```
22. Develop a C program to create a hard link named "hardlink.txt" to a file named "source.txt"? 
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <windows.h>
int main() {
    const char *source = "file.txt";
    const char *hardlink = "des_file.txt";
      if (CreateHardLinkA("file.txt", "des_file.txt", NULL)) {     //(in linux use)=if (link(source, hardlink) == 0) {
        printf("Hard link created: '%s' → '%s'\n", hardlink, source);
    } else {
        perror("Error creating hard link");
        return 1;
    }
    return 0;
}
```
23. Implement a C program to read and display the contents of a CSV file named "data.csv"?                                   
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#define FILE_NAME "data.csv"
#define BUFFER_SIZE 1024

int main() {
    int fd;
    ssize_t bytes_read;
    char buffer[BUFFER_SIZE];
    //Create and write to the file
    fd = open(FILE_NAME, O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (fd < 0) {
        perror("Error creating file");
        return 1;
    }
    const char *data =
        "Name,Age,City\n"
        "Naveen,24,Hyderabad\n"
        "Anya,22,Bengaluru\n"
        "Rahul,28,Chennai\n";

    write(fd, data, strlen(data));
    close(fd);
    write(STDOUT_FILENO, "File created and data written successfully.\n\n", 46);
    //Read and display the contents
    fd = open(FILE_NAME, O_RDONLY);
    if (fd < 0) {
        perror("Error opening file");
        return 1;
    }
    write(STDOUT_FILENO, "Contents of data.csv:\n\n", 24);
    while ((bytes_read = read(fd, buffer, sizeof(buffer))) > 0) {
        write(STDOUT_FILENO, buffer, bytes_read);
    }
    close(fd);
    return 0;
}
```
24. Write a C program to get the absolute path of the current working directory?
```
#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
#include <limits.h>
#include <fcntl.h>
int main() {
    char path[PATH_MAX];
    if (getcwd(path, sizeof(path)) == NULL) {
        const char *err = "getcwd() error\n";
        write(STDERR_FILENO, err, 14);
        return 1;
    }
    const char *msg = "Current working directory: ";
    write(STDOUT_FILENO, msg, 28);
    // Find length of path manually (no strlen)
    int len = 0;
    while (path[len] != '\0') len++;
    write(STDOUT_FILENO, path, len);
    write(STDOUT_FILENO, "\n", 1);
    return 0;
}
```
25. Develop a C program to get the size of a directory named "Documents"? 
```
#include<fcntl.h>
#include<unistd.h>
#include<dirent.h>
#include<sys/stat.h>
#include<string.h>
#include<stdio.h>

long get_directory_size(const char *path); 
int main(void) 

{
  const char *dirname = "all";
  long size = get_directory_size(dirname);
  printf("Total size of directory '%s': %ld bytes\n", dirname, size);
  return 0;
}

long get_directory_size(const char *path) 
{
  struct dirent *entry;
  struct stat statbuf;
  char fullpath[1024];
  long total_size = 0;
  DIR *dir = opendir(path);
  if (!dir) 
  {
    perror("opendir failed");
    return 0;
  }
  while ((entry = readdir(dir)) != NULL) 
  {
    // Skip "." and ".."
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);
    if (stat(fullpath, &statbuf) == -1) 
    {
      perror("stat failed");
      continue;
    }
    if (S_ISDIR(statbuf.st_mode)) 
    {
      // Recursively get size of subdirectories
      total_size += get_directory_size(fullpath);
    }
    else if (S_ISREG(statbuf.st_mode)) 
    {
      // Add size of regular file
      total_size += statbuf.st_size;
    }
  }
  closedir(dir);
  return total_size;
}
```
26. Implement a C program to recursively copy all files and directories from one directory to another?
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/stat.h>
#include <unistd.h>
#include <fcntl.h>
#include <dirent.h>
#include <errno.h>

void copy_file(const char *src, const char *dst);
void copy_directory(const char *src_dir, const char *dst_dir);

int main(void)
{
  const char *source = "source_dir";
  const char *destination = "destination_dir";
  copy_directory(source, destination);
  printf("All contents copied from '%s' to '%s'\n", source, destination);
  return 0;
}

void copy_file(const char *src, const char *dst)
{
  int in, out;
  char buffer[4096];
  ssize_t bytes;
  in = open(src, O_RDONLY);
  if (in < 0)
  {
    perror("open src");
    return;
  }
  out = open(dst, O_WRONLY | O_CREAT | O_TRUNC, 0644);
  if (out < 0)
  {
    perror("open dst");
    close(in);
    return;
  }
  while ((bytes = read(in, buffer, sizeof(buffer))) > 0)
  {
    write(out, buffer, bytes);
  }
  close(in);
  close(out);
}

void copy_directory(const char *src_dir, const char *dst_dir)
{
  struct dirent *entry;
  DIR *dir = opendir(src_dir);
  if (!dir)
  {
    perror("opendir");
    return;
  }
  mkdir(dst_dir, 0755); // Create destination directory if not exists
  while ((entry = readdir(dir)) != NULL)
  {
    char src_path[1024];
    char dst_path[1024];
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
       continue;
    snprintf(src_path, sizeof(src_path), "%s/%s", src_dir, entry->d_name);
    snprintf(dst_path, sizeof(dst_path), "%s/%s", dst_dir, entry->d_name);
    struct stat statbuf;
    stat(src_path, &statbuf);
    if (S_ISDIR(statbuf.st_mode))
    {
      copy_directory(src_path, dst_path);  // Recursive call
    }
    else if (S_ISREG(statbuf.st_mode))
    {
      copy_file(src_path, dst_path);       // Copy file
    }
  }
  closedir(dir);
}
```
27. write a c program to get the number of files in a directory 
```
#include <stdio.h>
#include <stdlib.h>
#include <dirent.h>
#include <sys/stat.h>
#include <string.h>

int main() {
    DIR *dir;
    struct dirent *entry;
    struct stat file_stat;
    int count = 0;
    const char *dirname = "Arr"; // Directory to scan

    dir = opendir(dirname);
    if (dir == NULL) {
        perror("opendir failed");
        return 1;
    }

    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".." entries
        if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
            continue;

        char path[1024];
        snprintf(path, sizeof(path), "%s/%s", dirname, entry->d_name);

        // Check if it's a regular file
        if (stat(path, &file_stat) == 0 && S_ISREG(file_stat.st_mode)) {
            count++;
        }
    }

    closedir(dir);
    printf("Number of regular files in '%s': %d\n", dirname, count);
    return 0;
}
```
28. Develop a C program to create a FIFO (named pipe) named "myfifo" in the current directory? 
```
#include<stdio.h>
#include<stdlib.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<errno.h>
#include<string.h>

int main(void){
	const char *fifo="myfifo";
	int ret=mkfifo("fifo",0666);
	if(ret<0){
		if(errno==EEXIST){
	printf("FIFO '%s' already exists\n",fifo);
		}
		else{
			fprintf(stderr,"Error creating FIFO '%s' : '%s'\n",fifo,strerror(errno));
	return EXIT_FAILURE;
	}
	}else{
	printf("fifo '%s' created\n",fifo);
	}
	return EXIT_SUCCESS;
}
```
29.Implement a C program to read data from a FIFO named "myfifo"? 
``` 
#include<stdio.h>
#include<stdlib.h>
#include<fcntl.h>
#include<unistd.h>

int main(){
	int fd;
	char buffer[1024];
	ssize_t bytesRead;
	fd=open("myfifo",O_RDONLY);
	if(fd<0){
		perror("Failed to open FIFO for reading");
		exit(EXIT_FAILURE);
	}
	printf("Reading data from FIFO\n");
	while((bytesRead = read(fd,buffer,sizeof(buffer)-1))>0){
		buffer[bytesRead]='\0';
		printf("Received:%s",buffer);
	}
	if(bytesRead==-1){
		perror("read");
	}
	close(fd);
	return 0;
}

```
30. Write a C program to truncate a file named "file.txt" to a specified length?  
```
#include<stdio.h>
#include<unistd.h>
#include<stdlib.h>

int main(){
	const char *filename = "hi.txt";
	off_t new_length = 10;
	if(truncate(filename, new_length)==0)
	{
		printf("File '%s' truncated to %ld bytes successfully\n", filename, (long)new_length);
}
else{
	perror("truncate failed");
	exit(EXIT_FAILURE);
}
return 0;
}
```
31. Develop a C program to search for a specific string in a file  named "data.txt" and display the line number(s) where it occurs?  
```
#include<stdio.h>
#include<string.h>
int main(){
	FILE *fp;
	char line[1024];
	char keyword[100];
	int line_num = 0;
	int found = 0;
	printf("Enter Stinrg to search:");
	scanf("%99s",keyword);
	fp=fopen("hi.txt","r");
	if(fp==NULL){
		perror("Failed to open file");
		return 1;
	}
	while(fgets(line,sizeof(line),fp)!=NULL){
		line_num++;
		if(strstr(line,keyword)!=NULL){
			line_num++;
			if(strstr(line,keyword)!=NULL){
				printf("Found '%s' on line %d:%s",keyword, line_num, line);
				found=1;
			}
		}
		fclose(fp);
		if(!found){
			printf("'%s' not found in file\n",keyword);
		}
		return 0;
	}
}
```
32. Implement a C program to get the file type (regular file, directory, symbolic link, etc.) of a given path?
```
#include<stdio.h>
#include<sys/stat.h>
#include<unistd.h>

int main(){
	struct stat filestat;
	char path[256];
	printf("Enter the path:");
	scanf("%s",path);
	if(lstat(path,&filestat)==-1){
		perror("lstat failed");
		return 1;
	}
	if(S_ISREG(filestat.st_mode))
		printf("It is a regular file\n");
	else if(S_ISLNK(filestat.st_mode))
		printf("It is a directory\n");
	else if(S_ISCHR(filestat.st_mode))
		printf("It is a character device file\n");
	else if(S_ISBLK(filestat.st_mode))
		printf("It is a block device file\n");
	else if(S_ISFIFO(filestat.st_mode))
		printf("It is a FIFO\n");
	else if(S_ISSOCK(filestat.st_mode))
		printf("It is a Socket\n");
	else
		printf("Unknown file type\n");
	return 0;
}
```
34. Develop a C program to get the permissions (mode) of a file named "file.txt"? 
```
#include<stdio.h>
#include<stdlib.h>
#include<sys/stat.h>
#include<sys/types.h>

int main(){
	const char *filename="Q_26.c";
	struct stat fileStat;
	if(stat(filename,&fileStat)<0){
		perror("stat failed");
		return 1;
	}
	printf("Permissions for '%s':\n",filename);	
	printf(S_ISDIR(fileStat.st_mode)?"d":"_");
	// owner per
	printf((fileStat.st_mode&S_IRUSR)?"r":"_");
	printf((fileStat.st_mode&S_IWUSR)?"w":"_");
	printf((fileStat.st_mode&S_IXUSR)?"x":"_");
	// group perm
	printf((fileStat.st_mode&S_IRGRP)?"r":"_");
	printf((fileStat.st_mode&S_IWGRP)?"w":"_");
	printf((fileStat.st_mode&S_IXGRP)?"x":"_");
	// OTHER PER
	printf((fileStat.st_mode&S_IROTH)?"r":"_");
	printf((fileStat.st_mode&S_IWOTH)?"w":"_");
	printf((fileStat.st_mode&S_IXOTH)?"x":"_");
	printf("\n");
	return 0;
}
```
35. Implement a C program to recursively delete a directory named "Temp" and all its contents?

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <errno.h>

int del_dir(const char *path) {
    DIR *dir = opendir(path);
    if (!dir) {
        perror("opendir");
        return -1;
    }

    struct dirent *entry;
    while ((entry = readdir(dir)) != NULL) {
        // Skip "." and ".."
        if (strcmp(entry->d_name, ".") == 0 ||
            strcmp(entry->d_name, "..") == 0)
            continue;

        char full_path[PATH_MAX];
        snprintf(full_path, sizeof(full_path), "%s/%s", path, entry->d_name);

        struct stat st;
        if (stat(full_path, &st) == -1) {
            perror("stat");
            closedir(dir);
            return -1;
        }

        if (S_ISDIR(st.st_mode)) {
            // Recursively delete subdirectory
            if (del_dir(full_path) == -1) {
                closedir(dir);
                return -1;
            }
        } else {
            // Delete file
            if (unlink(full_path) == -1) {
                perror("unlink");
                closedir(dir);
                return -1;
            }
        }
    }

    closedir(dir);

    // Finally, delete the (now empty) directory itself
    if (rmdir(path) == -1) {
        perror("rmdir");
        return -1;
    }

    return 0;
}

int main(void) {
    const char *target_dir = "all";
    if (del_dir(target_dir) == 0) {
        printf("Directory '%s' deleted successfully\n", target_dir);
    } else {
        printf("Failed to delete directory '%s'\n", target_dir);
    }
    return 0;
}
```
36. Write a C program to read and display the first 10 lines of a file named "log.txt"? 
```
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    FILE *fp = fopen("hi.txt", "r");
    if (fp == NULL) {
        perror("Failed to open file");
        return EXIT_FAILURE;
    }

    char buffer[1024];
    int line_count = 0;

    // Read up to 10 lines or until EOF
    while (line_count < 10 && fgets(buffer, sizeof(buffer), fp) != NULL) {
        printf("%s", buffer);
        line_count++;
    }

    if (ferror(fp)) {
        perror("Error reading file");
        fclose(fp);
        return EXIT_FAILURE;
    }

    fclose(fp);
    return EXIT_SUCCESS;
}
```
37. Develop a C program to read data from a text file named "input.txt" and write it to another file named "output.txt" in reverse order? 
```
#include <stdio.h>
#include <stdlib.h>
int main(void) {
    FILE *in_fp = fopen("hi.txt", "r");
    if (in_fp == NULL) {
        perror("Failed to open des_file.txt");
        return EXIT_FAILURE;
    }

    FILE *out_fp = fopen("output.txt", "w");
    if (out_fp == NULL) {
        perror("Failed to open output.txt");
        fclose(in_fp);
        return EXIT_FAILURE;
    }

    // Move to end of file to determine its size
    if (fseek(in_fp, 0, SEEK_END) != 0) {
        perror("fseek failed");
        fclose(in_fp);
        fclose(out_fp);
        return EXIT_FAILURE;
    }

    long file_size = ftell(in_fp);
    if (file_size == -1L) {
        perror("ftell failed");
        fclose(in_fp);
        fclose(out_fp);
        return EXIT_FAILURE;
    }

    // Read the file backwards character by character
    for (long i = file_size - 1; i >= 0; --i) {
        if (fseek(in_fp, i, SEEK_SET) != 0) {
            perror("fseek failed");
            fclose(in_fp);
            fclose(out_fp);
            return EXIT_FAILURE;
        }
        int ch = fgetc(in_fp);
        if (ch == EOF) {
            perror("fgetc failed");
            fclose(in_fp);
            fclose(out_fp);
            return EXIT_FAILURE;
        }
        if (fputc(ch, out_fp) == EOF) {
            perror("fputc failed");
            fclose(in_fp);
            fclose(out_fp);
            return EXIT_FAILURE;
        }
    }

    printf("Data written in reverse order to output.txt\n");

    fclose(in_fp);
    fclose(out_fp);
    return EXIT_SUCCESS;
}
```
38. Implement a C program to create a new directory named with the current date in the format "YYYY-MM-DD"? 
```
#include<stdio.h>
#include<time.h>
#include<sys/stat.h>
#include<string.h>
#include<errno.h>

int main(){
	time_t now;
	struct tm *timeinfo;
	char dirname[20];
	time(&now);
	timeinfo=localtime(&now);
	strftime(dirname,sizeof(dirname),"%y-%m-%d",timeinfo);
	if(mkdir(dirname,0755)==0){
		printf("Dir '%s' created\n",dirname);
	}
	else{
		perror("faied to creat dir");
	}
	return 0;
}
```
39. Write a C program to read and display the contents of a binary file named "binary.bin"?
```
#include<stdio.h>
#include<stdlib.h>
int main(){
	FILE *file;
	unsigned char buffer[16];
	size_t bytesRead;
	int offset=0;
	file=fopen("binary.bin","rb");
	if(file==NULL){
		perror("Error opening binary file");
		return 1;
	}
	printf("Contents of binary.bin in hexadecimal:\n\n");
	while((bytesRead=fread(buffer,sizeof(unsigned char),sizeof(buffer),file))>0){
			printf("0x%04X:",offset);
	for(size_t i=0;i<bytesRead;i++){
	printf("%20X",buffer[i]);
	}
	printf("\n");
	offset+=bytesRead;
	}
	fclose(file);
	return 0;
}
```
40. Develop a C program to get the size of the largest file in a directory?
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>
#include <limits.h>
#include <errno.h>

off_t get_largest_file_size(const char *path, char *largest_file_path) {
    DIR *dir = opendir(path);
    if (!dir) {
        fprintf(stderr, "opendir('%s') failed: %s\n", path, strerror(errno));
        return -1;
    }

    struct dirent *entry;
    off_t max_size = 0;
    char full_path[PATH_MAX];

    while ((entry = readdir(dir)) != NULL) {
        if (strcmp(entry->d_name, ".") == 0 ||
            strcmp(entry->d_name, "..") == 0)
            continue;

        snprintf(full_path, sizeof(full_path), "%s/%s", path, entry->d_name);

        struct stat st;
        if (stat(full_path, &st) == -1) {
            fprintf(stderr, "stat '%s' failed: %s\n", full_path, strerror(errno));
            continue;
        }

        if (S_ISDIR(st.st_mode)) {
            off_t sub_max = get_largest_file_size(full_path, largest_file_path);
            if (sub_max > max_size) {
                max_size = sub_max;
            }
        }
        else if (S_ISREG(st.st_mode)) {
            if (st.st_size > max_size) {
                max_size = st.st_size;
                strncpy(largest_file_path, full_path, PATH_MAX - 1);
                largest_file_path[PATH_MAX - 1] = '\0';
            }
        }
    }

    closedir(dir);
    return max_size;
}

int main(void) {
    const char *directory = ".";
    char largest_file[PATH_MAX] = {0};

    off_t size = get_largest_file_size(directory, largest_file);
    if (size >= 0) {
        if (largest_file[0]) {
            printf("Largest file: %s\nSize: %ld bytes\n", largest_file, size);
        } else {
            printf("No regular files found in directory '%s'.\n", directory);
        }
        return EXIT_SUCCESS;
    } else {
        fprintf(stderr, "Failed to determine largest file in '%s'.\n", directory);
        return EXIT_FAILURE;
    }
}
```
41. Implement a C program to check if a file named "data.txt" is readable?
```
#include <stdio.h>
#include <unistd.h>

int main(void)
{
  const char *filename = "hi.txt";
  if (access(filename, R_OK) == 0)
  {
     printf("The file \"%s\" is readable.\n", filename);
  }
  else
  {
    perror("File check failed");
  }
  return 0;
}
```
42. Write a C program to create a new directory named "Logs" and move all files with the ".log" extension into it? 
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>  
#include <errno.h>

int main(void) {
    DIR *d;
    struct dirent *dir;
    char src_path[512], dest_path[512];

    // Step 1: Create "Logs" if it doesn't already exist
    if (mkdir("Logs", 0777) == 0) {
        printf("Directory 'Logs' created successfully.\n");
    } else if (errno != EEXIST) {
        perror("mkdir");
        // If it exists, continue; else exit on real error
    }

    // Step 2: Open current directory
    d = opendir(".");
    if (d == NULL) {
        perror("opendir");
        return EXIT_FAILURE;
    }

    // Step 3: Read directory entries
    while ((dir = readdir(d)) != NULL) {
        // Skip current and parent entries
        if (strcmp(dir->d_name, ".") == 0 ||
            strcmp(dir->d_name, "..") == 0)
            continue;

        // Check if the filename ends with ".log"
        size_t len = strlen(dir->d_name);
        if (len > 4 && strcmp(dir->d_name + len - 4, ".log") == 0) {
            // Build full paths for rename()
            snprintf(src_path, sizeof(src_path), "./%s", dir->d_name);
            snprintf(dest_path, sizeof(dest_path), "./Logs/%s", dir->d_name);

            // Move file
            if (rename(src_path, dest_path) == 0) {
                printf("Moved: %s → Logs/\n", dir->d_name);
            } else {
                perror("rename");
            }
        }
    }

    closedir(d);
    return EXIT_SUCCESS;
}
```
44. Implement a C program to read the contents of a text file named "instructions.txt" and execute the instructions as shell commands? 
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <errno.h>
#include <sys/wait.h>

#define MAX_LINE 1024

int main(void) {
    // Part 1: Create instructions.txt with shell commands
    FILE *wf = fopen("instructions.txt", "w");
    if (!wf) {
        perror("Unable to create instructions.txt");
        return EXIT_FAILURE;
    }
    fprintf(wf, "echo \"Hello from shell command\"\n");
    fprintf(wf, "pwd\n");
    fprintf(wf, "ls -l\n");
    fprintf(wf, "date\n");
    fprintf(wf, "whoami\n");
    fclose(wf);
    printf("instructions.txt created successfully.\n");

    // Part 2: Read and execute the commands
    FILE *rf = fopen("instructions.txt", "r");
    if (!rf) {
        perror("Error opening instructions.txt");
        return EXIT_FAILURE;
    }

    char line[MAX_LINE];
    while (fgets(line, sizeof(line), rf)) {
        // Remove trailing newline
        size_t len = strlen(line);
        if (len && line[len - 1] == '\n')
            line[len - 1] = '\0';

        if (line[0] == '\0') // Skip empty lines
            continue;

        printf("\nExecuting: %s\n", line);
        int status = system(line);  // run via shell :contentReference[oaicite:3]{index=3}

        if (status == -1) {
            perror("system()");
            break;
        } else if (WIFEXITED(status) && WEXITSTATUS(status) != 0) {
            fprintf(stderr, "Warning: command \"%s\" exited with status %d\n",
                    line, WEXITSTATUS(status));
        }
    }

    if (ferror(rf)) {
        perror("Error reading instructions.txt");
    }

    fclose(rf);
    return EXIT_SUCCESS;
}
```
45. Write a C program to get the number of hard links to a file named "file.txt"?
```
#include<stdio.h>
#include<stdlib.h>
#include<sys/stat.h>

int main(){
	struct stat fileStat;
	if(stat("hi.txt",&fileStat)<0){
		perror("stat()failed");
		return 1;
	}
	printf("Number of hard links to file%lu\n",(unsigned long)fileStat.st_nlink);
	return 0;
}
```
46. Develop a C program to copy the contents of all text files in a directory into a single file named "combined.txt"? 
```
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
47. Implement a C program to recursively calculate the total size of all files in a directory and its subdirectories? 
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <dirent.h>
#include <sys/stat.h>
#include <unistd.h>

long long get_directory_size(const char *path);

int main(void)
{
  const char *target_directory = ".";  
  long long total_size = get_directory_size(target_directory);
  printf("Total size of all files: %lld bytes\n", total_size);
  return 0;
}

long long get_directory_size(const char *path)
{
  struct dirent *entry;
  struct stat statbuf;
  DIR *dir = opendir(path);
  long long total_size = 0;
  if (!dir)
  {
    perror("Failed to open directory");
    return 0;
  }
  while ((entry = readdir(dir)) != NULL)
  {
    char fullpath[1024];
    if (strcmp(entry->d_name, ".") == 0 || strcmp(entry->d_name, "..") == 0)
        continue;
    snprintf(fullpath, sizeof(fullpath), "%s/%s", path, entry->d_name);
    if (stat(fullpath, &statbuf) == -1)
    {
      perror("stat failed");
      continue;
    }
    if (S_ISDIR(statbuf.st_mode))
    {
      total_size += get_directory_size(fullpath); // Recurse into subdirectory
    }
    else if (S_ISREG(statbuf.st_mode))
    {
      total_size += statbuf.st_size; // Add file size
    }
  }
  closedir(dir);
  return total_size;
}
```
48. Write a C program to get the number of bytes in a file named "data.bin"?
```
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  FILE *file = fopen("binary.bin", "rb");  // Open in binary read mode
  if (file == NULL)
  {
    perror("Error opening file");
    return 1;
  }

  fseek(file, 0, SEEK_END);

  long size = ftell(file);
  fclose(file);
  if (size < 0)
  {
    perror("ftell failed");
    return 1;
  }
  printf("Size of data.bin: %ld bytes\n", size);
  return 0;
}
```
49. Develop a C program to create a new directory named with the current timestamp in the format "YYYY-MM-DD-HH-MM-SS"?
```
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
#include<sys/stat.h>
#include<string.h>

int main(){
	time_t now;
	struct tm *timeinfo;
       char dir_name[100];
  time(&now);
  timeinfo=localtime(&now);
  strftime(dir_name,sizeof(dir_name),"%y-%m-%d-%H-%M-%s",timeinfo);
  if(mkdir(dir_name,0777)==0){
    printf("Directoty '%s' created successfully\n",dir_name);
   }
   else{
	perror("mkdir failed");
	return 1;
  }
} 
```
50. Implement a C program to open a file named "data.txt" in read mode and display its contents? 
```
#include<stdio.h>
int main(){
	FILE *fp;
	char ch;
	fp=fopen("hi.txt","r");
	if(fp==NULL){
		perror("Failed to open");
		return 1;
	}
	while((ch=fgetc(fp))!=EOF){
		putchar(ch);
	}
	fclose(fp);
	return 0;
}
```
51. Write a C program to create a symbolic link(soft like) named "link.txt" to a file named "target.txt"? 
```
#include <stdio.h>
#include <unistd.h>

int main(void)
{
  const char *target = "target.txt";
  const char *symlink_name = "link.txt";
  if (symlink(target, symlink_name) == 0)
  {
    printf("Symbolic link '%s' created to '%s'\n", symlink_name, target);
  }
  else
  {
    perror("Error creating symbolic link");
  }
  return 0;
}
```
52. Implement a C program to read and display the contents of a binary file named "binary.bin"? 
```
#include <stdio.h>
#include <stdlib.h>

int main(void) 
{
  FILE *file;
  unsigned char buffer[1024];
  size_t bytesRead, i;
  // Open the binary file for reading
  file = fopen("binary.bin", "rb");
  if (file == NULL) 
  {
    perror("Error opening file");
    return 1;
  }
  // Read and display the contents
  while ((bytesRead = fread(buffer, 1, sizeof(buffer), file)) > 0) 
  {
    for (i = 0; i < bytesRead; i++) 
    {
      printf("%c", buffer[i]);  // Prints as characters (might not be readable)
    }
  }
  fclose(file);
  return 0;
}
```
53. Develop a C program to read data from a binary file named "data.bin" and display it in hexadecimal format? 
```
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
  FILE *fp = fopen("binary.bin", "rb");  // Open file in binary read mode
  if (fp == NULL)
  {
    perror("Failed to open data.bin");
    return 1;
  }
  unsigned char buffer[16];  // Buffer to read 16 bytes at a time
  size_t bytesRead;
  int offset = 0;
  while ((bytesRead = fread(buffer, sizeof(unsigned char), sizeof(buffer), fp)) > 0)
  {
    printf("%08x  ", offset);  // Print offset in hexadecimal
    for (size_t i = 0; i < bytesRead; i++)
    {
      printf("%02x ", buffer[i]);  // Print byte in hex
    }
    printf("\n");
    offset += bytesRead;
  }
  fclose(fp);
  return 0;
}
```
