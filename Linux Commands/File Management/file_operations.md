# File Management: File Operations

This document covers essential commands for creating, copying, moving, renaming, and deleting files and directories in Linux. These commands are fundamental for managing files in a Linux environment.

---

## 1. Creating Files and Directories

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `touch`           | Create a new, empty file or update an existing file's timestamp. | `touch newfile.txt`                |
| `mkdir`           | Create a new directory.                                   | `mkdir my_directory`                    |
| `mkdir -p`        | Create nested directories (parent directories).           | `mkdir -p parent/child/grandchild`      |
| `echo "text"`     | Create a new file with specific text content.             | `echo "Hello, World!" > file.txt`       |
| `cat > filename`  | Create a file and start adding content interactively.     | `cat > newfile.txt`                     |

---

## 2. Copying Files and Directories

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `cp file1 file2`  | Copy a file to a new file.                                | `cp source.txt destination.txt`         |
| `cp -r`           | Copy directories recursively.                             | `cp -r sourcedir/ targetdir/`           |
| `cp -i`           | Interactive copy that prompts before overwriting files.   | `cp -i source.txt destination.txt`      |
| `cp -u`           | Copy only when the source file is newer than the destination file. | `cp -u file1.txt file2.txt`   |

---

## 3. Moving and Renaming Files and Directories

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `mv`              | Move a file or directory to a new location.               | `mv file.txt /path/to/destination/`     |
| `mv`              | Rename a file or directory.                               | `mv oldname.txt newname.txt`            |
| `mv -i`           | Interactive move that prompts before overwriting files.   | `mv -i file1.txt /destination/`         |
| `mv -u`           | Move only if the source file is newer than the destination. | `mv -u file1.txt file2.txt`           |

---

## 4. Deleting Files and Directories

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `rm`              | Delete a file.                                            | `rm file.txt`                           |
| `rm -i`           | Interactive delete that prompts before each deletion.     | `rm -i file.txt`                        |
| `rm -r`           | Recursively delete a directory and its contents.          | `rm -r my_directory/`                   |
| `rm -f`           | Force delete files without confirmation.                  | `rm -f file.txt`                        |
| `rmdir`           | Delete an empty directory only.                           | `rmdir empty_directory/`                |

---

## 5. Viewing File Content

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `cat`             | Display the entire content of a file.                     | `cat file.txt`                          |
| `more`            | View content of a file page-by-page.                      | `more file.txt`                         |
| `less`            | View content of a file with the ability to scroll back.   | `less file.txt`                         |
| `head`            | Display the first 10 lines of a file by default.          | `head file.txt`, `head -n 20 file.txt`  |
| `tail`            | Display the last 10 lines of a file by default.           | `tail file.txt`, `tail -n 20 file.txt`  |
| `nl`              | View content of a file with line numbers.                 | `nl file.txt`                           |

---

## 6. File Content Manipulation

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `echo "text" >> file` | Append text to the end of a file.                   | `echo "New line" >> file.txt`           |
| `cat file1 file2 > merged` | Concatenate multiple files into one file.     | `cat part1.txt part2.txt > full.txt`    |
| `tr`              | Translate or delete characters.                          | `cat file.txt | tr 'a-z' 'A-Z'`         |
| `sort`            | Sort the lines of a file alphabetically.                 | `sort file.txt`, `sort -r file.txt`     |
| `uniq`            | Remove duplicate lines from sorted data.                 | `sort file.txt | uniq`                  |
| `sed`             | Stream editor for basic text transformations.            | `sed 's/old/new/g' file.txt`            |

---

## 7. Viewing File Details

| Command           | Description                                               | Example                                 |
|-------------------|-----------------------------------------------------------|-----------------------------------------|
| `ls -l`           | List files with detailed information (permissions, size, etc.). | `ls -l`                          |
| `stat`            | Display detailed information about a file.               | `stat file.txt`                         |
| `file`            | Determine the file type of a file.                       | `file file.txt`                         |
| `du -sh`          | Display the size of a file or directory.                 | `du -sh file.txt`, `du -sh folder/`     |
| `wc`              | Count lines, words, and characters in a file.            | `wc file.txt`, `wc -l file.txt`         |

---

These commands provide a comprehensive guide for managing files and directories in Linux. Each command includes examples for practical reference, making it easy to perform file operations efficiently.
