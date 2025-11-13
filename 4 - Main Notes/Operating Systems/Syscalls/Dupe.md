
2025-11-13 09:36

Tags: #OS #Scripting 

# What are dup and dup2

The `dup` and `dup2` system calls are used to duplicate file descriptors in Unix-like operating systems. They create aliases for existing file descriptors, allowing multiple descriptors to refer to the same open file description, which includes the same file offset and status flags.

- **File descriptor duplication** creates a new file descriptor that shares the same open file description as the original descriptor
- Both descriptors can be used interchangeably for reading, writing, or seeking
- Changes made through one descriptor (like file offset) are visible through the other
- This is particularly useful for **I/O redirection** and **pipeline implementation**

### Syntax in C

```c
int dup(int oldfd);
int dup2(int oldfd, int newfd);
```

==dup(oldfd)== creates a duplicate of `oldfd` using the lowest-numbered available file descriptor.

==dup2(oldfd, newfd)== creates a duplicate of `oldfd` using the specified `newfd`. If `newfd` was already open, it is closed first.

---

## Key Differences

- `dup()`: Lets the system choose the new file descriptor number
    
- `dup2()`: You specify exactly which file descriptor number to use
    
- `dup2()` is **atomic** - the close and duplicate operations happen as a single operation
    
- `dup2()` is commonly used for standard I/O redirection (stdin, stdout, stderr)
    

### Example Code: Basic dup usage

```c
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd1, fd2;
    char buffer[100];
    
    // Open a file
    fd1 = open("test.txt", O_RDONLY);
    if (fd1 < 0) {
        perror("open");
        return 1;
    }
    
    // Duplicate the file descriptor
    fd2 = dup(fd1);
    
    // Both descriptors point to the same file
    read(fd1, buffer, 10);  // Reads first 10 bytes
    read(fd2, buffer + 10, 10); // Reads next 10 bytes (continues from same offset)
    
    close(fd1);
    close(fd2);
    return 0;
}
```

```c
### Example Code: I/O Redirection with dup2

#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>

int main() {
    int fd;
    
    // Open a file for writing
    fd = open("output.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
    if (fd < 0) {
        perror("open");
        return 1;
    }
    
    // Redirect stdout to the file
    if (dup2(fd, STDOUT_FILENO) == -1) {
        perror("dup2");
        return 1;
    }
    
    // Close the original descriptor (no longer needed)
    close(fd);
    
    // Now printf will write to the file instead of terminal
    printf("This text goes to output.txt\n");
    printf("Another line in the file\n");
    
    return 0;
}
```

# Content of output.txt:
This text goes to output.txt
Another line in the file

### Common Use Cases

1. **I/O Redirection**: Redirect stdin/stdout/stderr to files
    
2. **Pipeline Implementation**: Connect processes via pipes
    
3. **Backup Standard Streams**: Save original stdin/stdout before redirection
    
4. **Socket Programming**: Duplicate socket descriptors for multiple uses







