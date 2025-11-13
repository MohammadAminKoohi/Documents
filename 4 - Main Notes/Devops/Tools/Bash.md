
2024-10-09 15:18

Tags: #Devops #Terminal #Scripting
# ‌Bash

Bash is short for Bourne Again Shell, one of the most commonly used Unix shells for scripting and automating tasks.

### Why learn Bash?
- **Most widely used shell**: Bash is the default shell in most Linux distributions and macOS, making it essential for system administration and automation tasks.
- **Comes with Linux and other OS**: No need for extra installation in most Unix-like operating systems.

---

## Bash Commands and Their Flags

### `echo`
Prints text to the terminal or another output stream.

**Syntax:**
```bash
echo [OPTIONS] [STRING]
```

**Common flags:**
- `-n`: Do not output the trailing newline.
- `-e`: Enable interpretation of backslash escapes (e.g., `\n` for a new line).

**Example:**
```bash
echo "Hello, World!"
echo -n "No newline after this."
```

### `|` (Pipe)
Passes the output of one command as input to another.

**Example:**
```bash
echo "Hello" | grep "H"
```

### `>` (Redirection)
Redirects output to a file (overwrites the file).

**Example:**
```bash
echo "Hello" > file.txt
```

### `>>` (Append Redirection)
Appends output to the end of a file.

**Example:**
```bash
echo "More text" >> file.txt
```

### `grep`
Searches for a pattern in files or input streams.

**Syntax:**
```bash
grep [OPTIONS] PATTERN [FILE...]
```

**Common flags:**
- `-i`: Ignore case.
- `-r`: Recursively search directories.
- `-v`: Invert match (show lines that do not match the pattern).

**Example:**
```bash
grep -i "hello" file.txt
```

### `wc`
Word, line, or byte count.

**Syntax:**
```bash
wc [OPTIONS] [FILE...]
```

**Common flags:**
- `-w`: Count words.
- `-l`: Count lines.
- `-c`: Count bytes.

**Example:**
```bash
echo "Hello World" | wc -w  # Output: 2
```

### `<` (Input Redirection)
Feeds a file as input to a command.

**Example:**
```bash
sort < file.txt
```

### `<<` (Here Document)
Used for multi-line string input.

**Example:**
```bash
cat << EOF
This is a multi-line
input block.
EOF
```

### `<<<` (Here String)
Passes a string as input to a command.

**Example:**
```bash
grep "pattern" <<< "search this string"
```

### `$?`
Returns the exit status of the last executed command. `0` means success; any other number indicates an error.

**Example:**
```bash
ls
echo $?  # Shows 0 if 'ls' succeeds
```

---

## Bash Control Structures

### `if` Statement
Used to execute commands based on conditions.

**Syntax:**
```bash
if [ condition ]; then
    # Commands if condition is true
elif [ other_condition ]; then
    # Commands if other_condition is true
else
    # Commands if no condition is true
fi
```

**Example:**
```bash
if [ -f file.txt ]; then
    echo "file.txt exists."
else
    echo "file.txt does not exist."
fi
```

### `for` Loop
Used to iterate over a list of items.

**Syntax:**
```bash
for var in list; do
    # Commands
done
```

**Example:**
```bash
for i in 1 2 3; do
    echo "Number $i"
done
```

### `while` Loop
Executes a block of code while a condition is true.

**Syntax:**
```bash
while [ condition ]; do
    # Commands
done
```

**Example:**
```bash
counter=1
while [ $counter -le 5 ]; do
    echo "Counter: $counter"
    ((counter++))
done
```

### `case` Statement
A more efficient way to match a variable against multiple patterns.

**Syntax:**
```bash
case $var in
    pattern1)
        # Commands for pattern1
        ;;
    pattern2)
        # Commands for pattern2
        ;;
    *)
        # Default commands
        ;;
esac
```

**Example:**
```bash
fruit="apple"
case $fruit in
    apple)
        echo "Apple selected."
        ;;
    banana)
        echo "Banana selected."
        ;;
    *)
        echo "Unknown fruit."
        ;;
esac
```

---

## Other Useful Bash Commands

### `sed`
Stream editor for text manipulation.

**Syntax:**
```bash
sed [OPTIONS] [SCRIPT] [INPUTFILE...]
```

**Common flags:**
- `-i`: Edit files in place.
- `s/pattern/replacement/`: Replace `pattern` with `replacement`.

**Example:**
```bash
sed 's/foo/bar/g' file.txt
```

### `awk`
Pattern scanning and processing language.

**Syntax:**
```bash
awk 'script' [file...]
```

**Example:**
```bash
awk '{ print $1 }' file.txt  # Print the first column of a file
```

### `find`
Search for files and directories.

**Syntax:**
```bash
find [PATH] [EXPRESSION]
```

**Common flags:**
- `-name`: Search by name.
- `-type f`: Search for files only.
- `-type d`: Search for directories only.

**Example:**
```bash
find /home/user -name "*.txt"
```

### `xargs`
Builds and executes command lines from standard input.

**Example:**
```bash
echo "file1 file2 file3" | xargs rm  # Deletes the listed files
```

### `ps`
Displays information about running processes.

**Common flags:**
- `-e`: Show all processes.
- `-f`: Full format (detailed process info).

**Example:**
```bash
ps -ef
```

### `kill`
Sends a signal to terminate a process.

**Syntax:**
```bash
kill [OPTIONS] PID
```

**Common signals:**
- `-9`: Forcefully kill a process.

**Example:**
```bash
kill -9 1234  # Terminates process with PID 1234
```

### `chmod`
Changes file permissions.

**Syntax:**
```bash
chmod [OPTIONS] MODE FILE
```

**Common flags:**
- `+x`: Adds execute permissions.

**Example:**
```bash
chmod +x script.sh  # Makes script executable
```

### `chown`
Changes the owner of a file.

**Syntax:**
```bash
chown [OPTIONS] OWNER[:GROUP] FILE
```

**Example:**
```bash
chown user:group file.txt
```

---

# References
- [GNU Bash Documentation](https://www.gnu.org/software/bash/manual/bash.html)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)