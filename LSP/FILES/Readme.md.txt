#include<stdio.h>
#include<unistd.h>
#include<fcntl.h>
#include<string.h>
//1.Write a C program to create a new text file and write user input to it
/*int main(void)
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
}*/

// 2.Develop a C program to open an existing text file and display its contents
/*int main(){}
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
  }*/
//3.Implement a C program to create a new directory named "Test" in the current-dir? 
/*#include <stdio.h>
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
}*/
//4.Write a C program to check if a file named "sample.txt" exists in the current directory?
/*int main(){
  if(access("Tes",F_OK)==0){
    printf("File is present\n");
  }
  else{
    perror("No such file found");
  }
  return 0;
}*/
//5. Develop a C program to rename a file,dir, from "oldname.txt" to "newname.txt"? 
/*int main(){
  if(rename("Test","new")==0){
    printf("File renamed");
  }
  else{
    perror("Error file");
  }
  return 0;
}*/
//6. Implement a C program to delete a file named "delete_me.txt"?
/*int main(){
  if(remove("q2.c")==0){
    printf("file removed");
  }
  else{
    printf("fai to remove");
  }
  return 0;
}*/
//7. Write a C program to copy the contents of one file to another? 
/*int main() {
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
}*/
//8. Develop a C program to move a file from one directory to another?
/*int main(){
  char *old_path="src_file.txt";
  char *new_path="../destination/des.txt";
  if(rename(old_path,new_path)==0){
    printf("File moved successfully\n");
  }
  else{
    perror("moving failed");
  }
    return 0;
}*/
// 9. Implement a C program to list all files in the current directory
/*#include <dirent.h>
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
}*/
//10. Write a C program to get the size of a file named "file.txt"?     
/*#include <stdlib.h>
#include <sys/stat.h> //The stat() function in C is used to retrieve information about a file or directory details like file size, permissions, timestamps, and type
int main() {
    struct stat file_stat;
    if (stat("file.txt", &file_stat) == -1) {
        perror("stat failed");
        return 1;
    }
    printf("Size of file = %ld bytes\n", file_stat.st_size);
    return 0;
}*/
//11.prg to check if a directory named exist in the current directory
/*#include <sys/stat.h>
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
}*/
//12.creat a new dir named "Backup"
/*#include <direct.h>
int main() {
    int status = _mkdir("Backup"); // for creating in pwd, if like to creat in previous dir use ../file_name
  
    if (status == 0) {
        printf("Directory created successfully\n");
    } else {
        perror("Failed to create directory");
    }

    return 0;
}*/
/*13. Write a C program to recursively list all files and directories in a given directory? 
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
}*/

//14. Develop a C program to delete all files in a directory named "Temp"?
/*#include <sys/types.h>
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
}*/
//15. prg to count the number of lines in a file
/*int main(){
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
}*/
//16. c prg to append "Goodbye" to the end of an existing file,
/*int main(){
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
}*/
//17. c program to change the permission of a file,
/*int main(){
  const char *fnam="file.txt";
  if(chmod(fnam,0444)==0)
  printf("permission changed to read only\n");
  else{
    perror("Failed to change permissions");
    return 1;
  }
  return 1;
}*/
//18. c prg to change the ownership of a file to user

//19. Develop a C program to get the last modified timestamp of a file named "file.txt"?
/*#include<sys/stat.h>
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
}*/
//20. creat a temporary file and write some data to it?
/*int main(){
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
}*/
//21. Write a C program to check if a given path refers to a file or a directory? 
/*#include <sys/stat.h>
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
}*/
// * 22. Develop a C program to create a hard link named "hardlink.txt" to a file named "source.txt"? 
/*#include <windows.h>
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
}*/
//23. Implement a C program to read and display the contents of a CSV file named "data.csv"?                                   
/*#define FILE_NAME "data.csv"
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
}*/
//24. Write a C program to get the absolute path of the current working directory?
/*#include <limits.h>
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
}*/
