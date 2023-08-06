# Training Schedule - Week 4

### Sunday:

- Learned the `kill` command to terminate processes.
- Explored the `top` and `htop` commands to view processes and system performance.
- Used `htop` to terminate an infinite loop running as a process.
- Practiced using `top` in batch mode and terminating processes with `kill` to stop infinite loops.

### Monday:

- Studied the Proc filesystem to access information about processes and their files.
- Explored the concept of files associated with a process in Linux.
- Gained a deeper understanding of what processes are in the context of the operating system.

### Tuesday:

Applied and learned intermediate to advanced Linux commands, including:
- `ls`, `pwd`, `cd`, `mkdir`, `mv`, `cp`, `rm`, `touch`, `ln`, `cat`, `clear`, `echo`, `less`, `man`, `uname`, `whoami`, `tar`, `grep`, `head`, `tail`, `diff`, `cmp`, `comm`, `sort`, `export`, `zip`, `unzip`, `ssh`, `service`, `ps`, `kill`, `killall`, `df`, `mount`, `chmod`, `chown`, `ifconfig`, `traceroute`, `wget`, `ufw`, `iptables`, `apt`, `pacman`, `yum`, `rpm`, `sudo`, `cal`, `alias`, `dd`, `whereis`, and `whatis`.
- Practiced using these commands and understanding their functionalities.

### Wednesday:

- Learned how to control services and processes, for example, starting and stopping the Apache service.
- Explored controlling the `PATH` variable by adding directories to it, enabling the execution of executables without specifying the path.

### Thursday:

Utilized and learned about the most common Linux tools, including:

1. `xxd`:
   - Use: `xxd` is a powerful command-line utility used for creating a hex dump of a given file.
   - Benefits: Hex dumps are useful for analyzing binary files, viewing file content in hexadecimal and ASCII representation, and identifying patterns or anomalies in the data.
   - Example Usage: `xxd myfile.bin` - Generates a hex dump of `myfile.bin`.

2. `file`:
   - Use: The `file` command is used to determine the file type of a given file.
   - Benefits: This tool helps identify file formats without relying on file extensions, making it useful for handling files with unknown or misleading extensions.
   - Example Usage: `file image.jpg` - Determines the type of the `image.jpg` file.

3. `exiftool`:
   - Use: `exiftool` is a versatile tool for reading and manipulating metadata in image, audio, and video files.
   - Benefits: It allows users to view, edit, and remove metadata information (Exif, IPTC, XMP, etc.) from multimedia files. This is especially valuable for photographers and media professionals who need to manage and modify metadata.
   - Example Usage: `exiftool -Title="My Photo" image.jpg` - Sets the title metadata of `image.jpg` to "My Photo."

4. `unzip`:
   - Use: The `unzip` command is used to extract files from zip archives.
   - Benefits: It simplifies the process of extracting multiple files or directories from compressed zip archives, making it an essential tool for managing compressed data.
   - Example Usage: `unzip archive.zip` - Extracts all files and directories from `archive.zip`.

5. `git`:
   - Use: `git` is a distributed version control system used for tracking changes in source code during software development.
   - Benefits: It allows multiple developers to collaborate efficiently, track changes, manage different versions of the codebase, and revert to previous states if needed.
   - Example Usage: `git init` - Initializes a new Git repository in the current directory.

6. `gzip`:
   - Use: `gzip` is a compression utility used to compress or decompress files.
   - Benefits: It significantly reduces file size, making data storage and transfer more efficient.
   - Example Usage: `gzip myfile.txt` - Compresses `myfile.txt` and creates `myfile.txt.gz`.

These tools provide essential functionalities for different tasks in Linux. For instance, `xxd` helps with low-level data analysis, `file` aids in identifying file types, `exiftool` manages metadata, `unzip` extracts compressed files, `git` facilitates version control, and `gzip` compresses files for efficient storage and transmission.
