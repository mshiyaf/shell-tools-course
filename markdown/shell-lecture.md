# 🐚 Shell Fundamentals
### A Two-Part Beginner Course (2 Weeks)
#### By Shiyaf C

<!-- .slide: data-background="linear-gradient(120deg, #0A192F 0%, #203A43 50%, #2C5364 100%)" -->

---

<!-- .slide: data-background="linear-gradient(120deg, #2C3E50 0%, #3498DB 100%)" -->

## 🎯 Course Structure

- 2 weeks, 2 sessions per week
- Each session: 1.5 hours
- Hands-on exercises in every class
- Beginner-friendly pace
- Focus on practical skills

---

<!-- .slide: data-background="linear-gradient(120deg, #1a2a6c 0%, #2980B9 100%)" -->

## 📚 Session Breakdown

Week 1:
- Session 1 (1.5h): Shell Basics & Navigation
- Session 2 (1.5h): File Operations & Permissions

Week 2:
- Session 1 (1.5h): Basic Shell Tools & Scripts
- Session 2 (1.5h): Finding Files & Practice

---

<!-- .slide: data-background="linear-gradient(120deg, #1a2a6c 0%, #2980B9 100%)" -->

## 🤔 Why Learn the Shell?

- 🤖 Computers excel at automating repetitive tasks
- 🎯 Most users only scratch the surface of available tools
- 🖥️ GUIs are great but fundamentally limited
- ⚡ Shell provides unrestricted access to your computer's capabilities
- 🚀 Essential skill for developers and power users
- 📚 Moving beyond copy-pasting commands from the internet

Note: As computer scientists, we know computers are great at aiding in repetitive tasks. However, we often forget this applies to our _use_ of computers as well.

--

<!-- .slide: data-background="linear-gradient(120deg, #2C3E50 0%, #27AE60 100%)" -->

## 📋 Why This Course?

- 🎓 Traditional CS curricula focus on programming concepts
- 🔍 Little attention to practical development tools
- 🌟 This course fills that gap by teaching:
  - 💻 Shell usage and scripting
  - 🔧 Essential command-line tools
  - ⚙️ Automation techniques

--

<!-- .slide: data-background="linear-gradient(120deg, #1a2a6c 0%, #3498DB 100%)" -->

## 🎯 Learning Goals

- 📚 Master fundamental shell concepts
- 📂 Understand Unix file system
- 🤖 Learn to automate repetitive tasks
- ⚡ Develop efficient command-line workflows
- 💪 Build confidence in system manipulation

---

<!-- .slide: data-background="linear-gradient(120deg, #2C3E50 0%, #2980B9 100%)" -->

## 📚 Course Overview

This is a two-part lecture series:

**Part 1: Shell Basics** 🔰
- Understanding the shell
- Basic command structure
- Navigation and file operations
- Input/output redirection
- Permissions and sudo

--

**Part 2: Shell Tools & Scripting** 🛠️
- Shell scripting fundamentals
- Finding and searching tools
- Command history
- Directory navigation tools
- Advanced shell techniques

Note: While we can't cover everything in depth, we'll provide resources for further exploration of topics that interest you.

---

<!-- .slide: data-background="linear-gradient(120deg, #1a2a6c 0%, #3498DB 100%)" -->

# 🔰 Shell Basics
## Part 1 of Shell Series

---

## 💻 What is the Shell?

- Text interface to your computer
- Available on all platforms:
  - Linux/macOS: Built-in terminal
  - Windows: WSL or Linux VM recommended
- We'll focus on Bash (Bourne Again SHell)

--

## 🔄 Shell vs Other Interfaces

- GUIs are intuitive but limited
- Voice/AR/VR good for common tasks
- Shell provides:
  - Full system access
  - Automation capabilities
  - Precise control
  - Remote system management

---

## 📝 Basic Command Structure

```bash
missing:~$ date
Fri 10 Jan 2020 11:49:31 AM EST
```

```bash
missing:~$ echo hello
hello
```

--

## 🔍 Command Components

- Shell splits commands by whitespace
- First word is the program name
- Remaining words are arguments

--

## ⚡ Special Characters

- 📝 Quotes:
  - 'Single quotes': Literal strings
  - "Double quotes": Allow variable expansion
- \ Backslash: Escape special characters
- $ Dollar sign: Variable expansion

Example:
```bash
missing:~$ name="world"
missing:~$ echo "Hello $name"  # prints: Hello world
missing:~$ echo 'Hello $name'  # prints: Hello $name
```

--

## 🔍 Finding Programs

```bash
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

```bash
missing:~$ which echo
/bin/echo
```

The shell:
1. Receives your command
2. Splits it into program name and arguments
3. Searches $PATH for the program
4. Executes it with given arguments

---

## 🗺️ Navigating the Filesystem

### 📂 Core Navigation Commands

- `pwd` - Print working directory
- `cd` - Change directory
- `ls` - List contents
- `.` - Current directory
- `..` - Parent directory

--

## 🛣️ Path Types & Examples
- Absolute: starts with / (Linux/macOS) or C:\ (Windows)
  ```bash
  cd /home/user/documents
  ```
- Relative: based on current location
  ```bash
  cd ./projects
  cd ../downloads
  ```

--

Example navigation:
```bash
missing:~$ pwd
/home/missing
missing:~$ cd /home
missing:/home$ cd ..
missing:/$ cd ./home
missing:/home$ cd missing
missing:~$ pwd
/home/missing
```

---

## 🔗 Advanced Path Concepts

- Symbolic links (`ln -s`)
- Path expansion (`~`, `${HOME}`)
- Globbing patterns (`*.txt`, `???`, `[a-z]`)

--

## 🔗 Symbolic Links

Symbolic links are a type of file that points to another file or directory.

```bash
missing:~$ ls -l /usr/bin/python3
lrwxr-xr-x 1 root wheel 9 Jan 14 09:53 /usr/bin/python3 -> /opt/homebrew/bin/python3
```

--

## 🏠 Path Expansion

Path expansion allows you to use special variables to refer to commonly used directories.

- `~` or `${HOME}` refers to your home directory
- `${PWD}` refers to your current working directory
- `${USER}` refers to your username

--

## 🎯 Globbing Patterns

Globbing patterns allow you to match multiple files based on patterns.

- `*.txt` matches all files with a `.txt` extension
- `???` matches all files with exactly three characters
- `[a-z]` matches all files that start with a letter from a to z

--

## 🎯 Globbing Examples

```bash
missing:~$ ls /home/missing/documents/*.txt
notes.txt
```

---

## 📂 Working with Files

Basic Operations:
- `mv` - Move/rename files
- `cp` - Copy files
- `mkdir` - Create directories

--

## ℹ️ File Information

- `ls` - List contents
- `ls -l` - Detailed listing
- `file` - Show file type
- `man` - View documentation

Example:
```bash
missing:~$ file hello.txt
hello.txt: ASCII text
```

--

## 🔒 Understanding Permissions

File Permissions:
- Read (r), Write (w), Execute (x)
- Set for: Owner, Group, Others

--

```bash
missing:~$ ls -l
drwxr-xr-x 1 user group 4096 Jan 14 09:53 documents
-rw-r--r-- 1 user group  514 Jan 14 06:42 notes.txt
```

Breakdown:
- First character: file type (d for directory, - for regular file)
- Next three triplets: permissions for owner, group, others
- Numbers: number of links, owner, group, size
- Date: last modification time
- Name: file/directory name

---

# ⚡ Power Tools

## 🔄 Input/Output Redirection

Basic Redirection:
- `>` writes output to file
- `<` reads input from file
- `|` connects programs together

--

## 🔄 Advanced Redirection

File Descriptors:
- 0: Standard input (stdin)
- 1: Standard output (stdout)
- 2: Standard error (stderr)

Examples:
```bash
# Redirect only errors
./script.sh 2> errors.log

# Redirect both output and errors to different files
./script.sh 1> output.log 2> errors.log
```

--

## 🔄 More Redirection Features

- `>>` append to file
- `&>` redirect both output and errors
- `|&` pipe both output and errors
- `2>&1` redirect stderr to stdout

---

# 👑 Root Access

## 🔑 The Superuser

- Root user has complete system access
- Never log in directly as root
- Use `sudo` for administrative tasks
- Verify before using sudo

--

## 🗄️ System Files

Special system locations:
- `/sys` - Kernel parameters
- `/proc` - Process information
- `/dev` - Device files

Example:
```bash
# Changing screen brightness (Linux)
echo 3 | sudo tee /sys/class/backlight/acpi_video0/brightness
```

---

## 🎯 Practical Exercises

Each exercise builds on previous concepts:

1. Environment Setup
2. File Creation and Editing
3. Permissions Management
4. I/O Redirection
5. System Exploration
6. Navigation Challenge

--

## 🎯 Exercise 1: Environment Setup


1. Verify Unix shell:
```bash
echo $SHELL
# Should show /bin/bash or similar
```

2. Create working directory:
```bash
mkdir -p /tmp/missing
cd /tmp/missing
```

--

## Exercise 2: File Creation
1. Create a new file:
   ```bash
   touch semester
   ```
2. Write a simple script:
   ```bash
   #!/bin/sh
   curl --head --silent https://missing.csail.mit.edu
   ```
   > 💡 Note: Use single quotes for first line to handle !

--

## Exercise 3: Permissions

1. Try running the script:
   ```bash
   ./semester
   # Permission denied
   ```
2. Check permissions:
   ```bash
   ls -l semester
   ```
3. Add execute permission:
   ```bash
   chmod +x semester
   ```

--

## Exercise 4: I/O Redirection
1. Save command output:
   ```bash
   ./semester | grep last-modified > last-modified.txt
   ```
2. Explore different redirections:
   ```bash
   ./semester > output.txt 2> errors.txt
   ```

--

## Exercise 5: System Exploration (Linux)
1. Find your battery status:
   ```console
   cat /sys/class/power_supply/BAT0/status
   ```
2. Monitor CPU temperature:
   ```bash
   cat /sys/class/thermal/thermal_zone0/temp
   ```

> 💡 Note: These paths might vary by system

--

## Exercise 6: Navigation Challenge

1. Navigate to your home directory
2. List all files in your home directory
3. Create a new directory called `missing`
4. Navigate to your missing directory
5. List all files in your missing directory

--

### Exercise 7: File Creation (Part 1)

1. Look up the `touch` program
2. Use `touch` to create a new file called `learn-shell`
3. Write the following into that file, one line at a time:
   ```bash
   #!/bin/sh
   curl --head --silent https://learn-shell.mshiyaf.com
   ```

--

### Exercise 7: File Creation (Part 2)

4. Try to execute the file:
   - Type `./learn-shell` into your shell and press enter
   - Understand why it doesn't work by checking `ls` output (Hint: Look at the permission bits of the file)
5. Run with explicit interpreter:
   - Use `sh learn-shell` instead
   - Why does this work?
   - What is the purpose of the shebang line?

---

# Additional Resources

## 📖 Documentation
- `man bash` - Bash manual
- `info bash` - Detailed Bash documentation
- [GNU Coreutils](https://www.gnu.org/software/coreutils/manual/)

--

## 🎓 Learning Resources
- 📘 [Bash Guide](https://mywiki.wooledge.org/BashGuide)
- ✅ [ShellCheck](https://www.shellcheck.net/)
- 🔍 [Explainshell](https://explainshell.com/)
- 💬 [Unix Stack Exchange](https://unix.stackexchange.com/)

--

## 🎯 Practice Resources
- 🎮 [Over The Wire: Bandit](https://overthewire.org/wargames/bandit/)
- 💻 [Command Line Challenge](https://cmdchallenge.com/)
- 📝 [Bash Scripting Tutorial](https://linuxconfig.org/bash-scripting-tutorial)

> 💡 Remember: The best way to learn is by doing. Start with simple commands and gradually increase complexity.
---

<!-- .slide: data-background="linear-gradient(120deg, #0A192F 0%, #203A43 50%, #2C5364 100%)" -->

# Thank You! 🙏

## Connect & Learn More

- 📧 Contact: [shiyafc@gmail.com](mailto:shiyafc@gmail.com)
- 🌐 Website: [learn-shell.mshiyaf.com](https://learn-shell.mshiyaf.com)
- 💼 LinkedIn: [Shiyaf C](https://linkedin.com/in/mshiyaf)
- 🐙 GitHub: [@mshiyaf](https://github.com/mshiyaf)

--

<!-- .slide: data-background="linear-gradient(120deg, #2C3E50 0%, #3498DB 100%)" -->

## What's Next? 🚀

- 📚 Part 2: Shell Tools & Scripting
- 🔍 Advanced Shell Techniques
- 🛠️ Real-world Applications
- 💡 Custom Shell Configuration

> "The shell is your friend. Embrace it!" - Shiyaf C
