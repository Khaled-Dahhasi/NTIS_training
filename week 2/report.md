


**Training Schedule - Week 2**

**Sunday:**
- Started the Udemy course "Linux Mastery" focused on learning essential concepts like pipelines, aliases, and common Linux commands.
- Gained insights into the Linux shell and its functionalities, along with various other topics.

**Monday:**
- Worked on and completed assignments related to pipelines:
**Monday Assignment - Shell Script Explanation**

The shell script provided is a simple script written in the Bourne shell (#!/bin/sh) and consists of several tasks. Let's break down each task and explain what the script does:

```bash
#!/bin/sh

##task 1:
ls /etc > ./file1.txt
echo file1 created
ls /run > ./file2.txt
echo file2 created
```

**Task 1 Explanation:**
- The script starts by listing the contents of the `/etc` directory and saves the output to a file called `file1.txt` using the `>` redirection operator.
- The `echo` command is then used to print the message "file1 created" to the terminal, informing the user that the file has been created.
- Next, the script lists the contents of the `/run` directory and saves the output to another file named `file2.txt`.
- The `echo` command is used again to print the message "file2 created" to the terminal, indicating that the second file has been created.

```bash
##task2:
cat file1.txt file2.txt | tee  unsorted.txt | sort -r > reversed.txt
echo file unsorted and reversed created
```

**Task 2 Explanation:**
- In Task 2, the script reads the contents of both `file1.txt` and `file2.txt` using the `cat` command. The `cat` command concatenates the contents of the two files and sends the combined output to the next command in the pipeline.
- The `tee` command is then used with the `|` (pipe) operator to both display the combined output on the terminal and save it to a new file called `unsorted.txt`. The `tee` command allows you to split the output of a command and send it to multiple places simultaneously.
- The `sort -r` command is applied to the combined output. The `sort` command is used to sort the lines of text in alphabetical order by default. The `-r` option reverses the sorting order, creating a reversed (descending) alphabetical order.
- Finally, the sorted and reversed output is redirected to a new file named `reversed.txt` using the `>` redirection operator.

```bash
echo the program is done
exit 0
```

- After completing all tasks, the script prints the message "the program is done" to the terminal using the `echo` command.
- The `exit 0` command is used to explicitly specify that the script has executed successfully, and it returns a status code of 0 upon completion.

In summary, this shell script performs various tasks such as listing directories, creating files, and sorting and reversing the contents of those files. The script demonstrates basic shell scripting concepts and file handling operations using standard Linux commands.


**Tuesday:**
- Explored common Linux commands using the following websites:
  - [Kali Linux Beginner Guide](https://linuxhint.com/kali_linux_-beginner_guide/)
  - [Linux Command Line](https://infinite.education/view/TpiRKhW9K0aIKJo2pwvq9mPL?new&e=xdkXxYqQmhyJTYQNzHBwqWrR)
- Gathered knowledge on the practical applications and usage of these commands.

**Wednesday:**
- Focused on understanding the Linux file system structure, which is based on EXT4 and follows a tree-like hierarchy.
- Explored the purpose and functionalities of key directories, including:
  - / (Root): The primary directory that contains all other directories and files.
  - /bin: Holds essential user binaries (executable programs) accessible to all users.
  - /boot: Contains files required for system boot, such as the Linux kernel and boot loader configuration files.
  - /etc: Stores system-wide configuration files that control various applications and services.
  - /home: Each user has a dedicated subdirectory within /home for personal files and settings.
  - /lib and /lib64: These directories contain shared library files utilized by the system and applications.
  - /opt: Typically used for installing optional or third-party software packages.
  - /sbin: Contains system binaries used for system administration tasks.
  - /tmp: A temporary directory for applications to store temporary files.
  - /usr: Holds the majority of user-related data, including application files, libraries, and documentation.
  - /var: Contains variable data that frequently changes, such as log files, spool directories, and temporary files.
  
- Completed assignment 2, which involved practical exercises on the "locate," "updatedb ," "find," and "sort" commands:
  
**Wednesday Assignment 2 - Shell Script Explanation**
**Spoiler warning for harry potter**

Let's explain each task in the shell script provided:

```bash
#!/usr/bin/bash

sudo echo "thanks for the password ;)"
```

- The script starts with a shebang (`#!/usr/bin/bash`), specifying that the script should be interpreted and executed using the bash shell.
- The script uses `sudo` to elevate privileges and then echoes the message "thanks for the password ;)" to the terminal. This is used to prompt the user to enter their password for sudo execution.

```bash
##task1_1
mkdir ./super_secret_stuff | touch ./super_secret_stuff/top_secret.txt
echo snape kills dumbeldore | cat > ./super_secret_stuff/top_secret.txt
echo secret made...
```

**Task 1.1 Explanation:**
- The script creates a new directory named `super_secret_stuff` using the `mkdir` command. The `./` specifies the current directory as the location to create the directory.
- The script then uses the pipe (`|`) operator to run multiple commands in sequence.
- The `touch` command is used to create a new empty file named `top_secret.txt` inside the `super_secret_stuff` directory.
- The `echo` command with a message "snape kills dumbeldore" is then used, and its output is redirected (via `|`) to the `cat` command. The `cat` command reads the input from the echo command and writes it to the `top_secret.txt` file.
- Finally, the script prints the message "secret made..." to the terminal using the `echo` command.

```bash
##task1_2
sudo updatedb
locate top_secret.txt > ~/secret_place.txt
echo location revealed, look in your home
echo task 1 finished
```

**Task 1.2 Explanation:**
- The script begins with another `sudo` command to elevate privileges.
- The `updatedb` command is executed, which updates the search database used by the `locate` command. This ensures that the latest file information is available for searching.
- The `locate` command is used to find the file named `top_secret.txt` in the entire file system. The output of the `locate` command is then redirected to a file named `secret_place.txt` in the user's home directory (`~` refers to the home directory).
- The script prints the message "location revealed, look in your home" to the terminal using the `echo` command.
- Finally, the script prints "task 1 finished" to the terminal using the `echo` command.

```bash
##task2
sudo find / -maxdepth 4 -type f -size +1M -exec ls -lh {} \; | sort -k 5 -hr > ~/filesizes.txt
echo "----------------------------------------------"
echo task 2 done
```

**Task 2 Explanation:**
- The script starts with another `sudo` command for elevated privileges.
- The `find` command is used to search for files in the entire file system starting from the root directory `/`.
- The `-maxdepth 4` option limits the search to a maximum depth of 4 subdirectories. This helps improve search performance and prevents exhaustive searching.
- The `-type f` option specifies that only regular files should be considered for the search.
- The `-size +1M` option filters files with a size greater than 1 megabyte.
- The `-exec ls -lh {} \;` option is used to execute the `ls -lh` command on each found file, displaying their size and other details in human-readable format.
- The `|` (pipe) operator is used to redirect the output of the `find` command to the `sort` command.
- The `sort -k 5 -hr` command sorts the files based on their size (in the 5th column) in reverse (descending) order. The `-h` option is used to handle human-readable sizes.
- The sorted output is redirected to a file named `filesizes.txt` in the user's home directory (`~`).
- The script prints a line of dashes as a separator using the `echo` command.
- Finally, the script prints "task 2 done" to the terminal using the `echo` command.

In conclusion, this shell script performs tasks related to creating directories and files, searching for files, and generating a list of files based on their sizes. The script also uses `sudo` for privileged operations that require administrative permissions.
