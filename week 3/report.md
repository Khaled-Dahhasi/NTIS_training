**Training Schedule - Week 3**

**Sunday:**
- Continued going through Linux commands at [Linux Command Line](https://infinite.education/view/TpiRKhW9K0aIKJo2pwvq9mPL?new&e=xdkXxYqQmhyJTYQNzHBwqWrR)
- Understood `chmod` and `chown` commands: Learned how to change file permissions and ownership in Linux.
- Understood the meaning of permissions when using the `ls -lh` command on files: Learned how to interpret the file permissions displayed by the `ls` command.
- Understood hard links and symbolic "soft" links: Learned about different types of links used to reference files in Linux.

**Monday:**
- Explored the concepts of users, groups, and others in Linux: Learned about user and group ownership and the concept of "others" in file permissions.
- Learned how to make and join groups: Understood the process of creating and becoming a member of a group.
- Learned how to make a new user: Explored the steps to create a new user account on the system.

**Tuesday:**
- Installed packages via `sudo apt-get` and other package management commands: Learned how to use package managers to install software packages on the system.
- Explored the system update command: Learned how to update the package lists from repositories to get the latest information about available packages.
- Explored the system upgrade command: Learned how to upgrade installed packages to the latest versions.

**Wednesday:**
- Installed Visual Studio Code (VSCode) via the command line: Learned how to download and install VSCode using the terminal.
- Built a "Hello World!" program in C: Created a simple C program that prints "Hello World!" to the console.

**Thursday:**
- Programmed a makefile for a C program with multiple running options:

**Makefile -**

```make
helloworld: helloworld.c
        @gcc helloworld.c -o a.out

add: helloworld.c
        @gcc helloworld.c -o a.out
        @./a.out add $(x) $(y)

sub: helloworld.c
        @gcc helloworld.c -o a.out
        @./a.out sub $(x) $(y)

print:
        @echo $(x)
```

**C program -**

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char **argv) {
    if (argc > 3) {
        char *p;
        char *q;
        int x = strtol(argv[2], &p, 10);
        int y = strtol(argv[3], &q, 10);

        if (!strcmp(argv[1], "add")) {
            printf("adding %d + %d = %d\n", x, y, (x + y));
        } else if (!strcmp(argv[1], "sub")) {
            printf("subtracting %d - %d = %d\n", x, y, (x - y));
        } else {
            printf("usage: ./a.out <OPERATION> <operand1> <operand2>\n");
            printf("Operations: sub add\n");
        }
    }
    return 0;
}
```

**Task Explanation:**
- The makefile provides different targets for the C program, allowing various operations to be performed based on command-line arguments.
- The target `helloworld` is the default target and is used to compile the C program into an executable named `a.out`.
- The targets `add` and `sub` compile the C program and execute it with additional arguments (`$(x)` and `$(y)`). These targets perform addition and subtraction operations, respectively, based on the input operands provided as command-line arguments.
- The target `print` is used to display the value of `$(x)`.

**C program Explanation:**
- The C program takes command-line arguments and performs addition or subtraction based on the first argument (`add` or `sub`) and the two integer operands (`$(x)` and `$(y)`).
- The `strtol` function is used to convert the operand strings to integer values.
- If the correct number of arguments is not provided, the program displays usage instructions.

In conclusion, this week's training schedule focused on enhancing Linux skills by exploring various Linux commands, understanding file permissions, learning about users and groups, and working with package management. Additionally, practical experience was gained in installing software, writing C programs, and creating a makefile for a C program with multiple running options.
