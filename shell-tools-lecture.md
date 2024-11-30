# 🛠️ Shell Tools and Scripting
### Part 2 of Shell Series
#### By Shiyaf C

<!-- .slide: data-background="linear-gradient(120deg, #4B1248 0%, #F0C27B 100%)" -->

---

<!-- .slide: data-background="linear-gradient(120deg, #2C3E50 0%, #3498DB 100%)" -->

## Course Progress
- ✅ Week 1: Shell Basics Completed
- 📍 Week 2: Shell Tools Introduction

---

<!-- .slide: data-background="linear-gradient(120deg, #1a2a6c 0%, #2980B9 100%)" -->

Building on the previous shell basics, we'll cover:
- 📝 Shell scripting basics
- 🔧 Shell tools for common tasks
- 🔍 Finding and searching
- ⌛ Command history
- 📂 Directory navigation

---

<!-- .slide: data-background="linear-gradient(120deg, #203A43 0%, #2C5364 100%)" -->

## 💻 Shell Scripting Introduction

While we've learned to execute commands and pipe them together, real power comes from:

- ♻️ Writing reusable scripts
- 🔄 Using control flow (conditionals, loops)
- 🔗 Creating command pipelines
- 🤖 Automating repetitive tasks

--

Shell scripting is uniquely powerful because it's:
- Optimized for shell-related tasks
- Easy command pipelines
- Built-in file operations
- Perfect for system tasks

---

## 🔤 Variables and Strings

Variables are a core concept in shell scripting. They can store strings, numbers, and command outputs.

```bash
# Variable assignment (no spaces!)
foo=bar
echo "$foo"    # prints: bar
# String behavior
echo "$foo"      # prints: bar
echo '$foo'      # prints: $foo
# Command output to variable
current_date=$(date)
echo "$current_date"  # prints: 2024-01-14
# Arithmetic
count=5
total=$((count + 3))
```

--

## String Delimiters

- Single quotes ('): Literal strings
    - No variable expansion
    - Good for commands with special characters
- Double quotes ("): Allow variable expansion
    - Variable values are substituted
    - Preserves whitespace

--

## Example

```bash
name="world"
echo "Hello $name"  # prints: Hello world
echo 'Hello $name'  # prints: Hello $name

# Multiline strings
message="First line
Second line
Third line"
echo "$message"
```

---

# Special Variables

Essential shell variables:
```bash
$0         # Script name
$1 to $9   # First 9 arguments
$@         # All arguments
$#         # Number of arguments
$?         # Return code
$$         # Process ID
```

--

## Example Usage
```bash
echo "Script name: $0"
# Prints the script name
```

```bash
echo "First argument: $1"
# Prints the first argument
```

```bash
echo "All arguments: $@"
# Prints all arguments
```

```bash
echo "Number of arguments: $#"
# Prints the number of arguments
```

```bash
echo "Return code: $?"
# Prints the return code of the last command
```

```bash
echo "Process ID: $$"
# Prints the process ID of the current shell
```

--

## More Special Variables

```bash
!!         # Entire last command
$_         # Last argument of previous command

# Example usage
sudo !!    # Run last command with sudo
```

---

# Control Flow

## Exit Codes
```bash
# Success/failure examples
true || echo "Oops"   # Nothing printed
false || echo "Oops"  # Prints "Oops"
true && echo "Yes"    # Prints "Yes"
false && echo "No"    # Nothing printed
```

--

## Command Separators

`;` is a command separator that allows you to run multiple commands on a single line.

```bash
# Commands with ;
false ; echo "Always runs"
```

`&&` and `||` are short-circuit operators that allow you to chain commands together.

```bash
# Short-circuit operators
command1 && command2  # command2 runs if command1 succeeds
command1 || command2  # command2 runs if command1 fails
```

---

# Command Substitution

## Basic Substitution
```bash
echo "We are in $(pwd)"
files=$(ls)

# Command substitution with backticks (older style)
echo "We are in `pwd`"    # Same as $(pwd)
```

--

## Process Substitution
```bash
# Compare directory contents
diff <(ls dir1) <(ls dir2)

# Sort and compare
diff <(sort file1) <(sort file2)

# Multiple commands
diff <(command1) <(command2)
```

---

# Shell Scripting Best Practices

## ShellCheck

- Tool to check shell scripts for common errors
- Can fix common issues

--

### Using ShellCheck

```bash
# Install shellcheck
sudo apt install shellcheck

# Check script
shellcheck script.sh
```

### Fixing Common Issues
```bash
shellcheck -f diff script.sh
```

--

## Debugging Tips
```bash
# Enable debug mode (prints commands before execution)
set -x

# Strict mode (exit on error, undefined variables)
set -euo pipefail

# Both together (recommended)
set -euxo pipefail
```

---

# Finding Files

## Using find

- Powerful command to search for files
- Can search by name, path, type, etc.
- Can execute commands on found files

```bash
# Find by name
find . -name src -type d

# Find by path pattern
find . -path '*/test/*.py' -type f
```

--

## Modern alternatives

- `fd` - simpler syntax than `find`
    - [GitHub: fd](https://github.com/sharkdp/fd)

```bash
fd ".*py"              # Find Python files
fd -e md               # Find by extension
fd -d 2 pattern        # Search depth 2
```

--

## fzf - fuzzy finder

- Powerful tool to search for files
- Can be used to find and edit files
- [GitHub: fzf](https://github.com/junegunn/fzf)

```bash
vim $(fzf)            # Find and edit file
cd $(find . -type d | fzf)  # Fuzzy directory navigation
```

--

## Advanced Find Options
```bash
# Find by time and size
find . -mtime -1                   # Modified in last day
find . -size +500k -size -10M      # Size range

# Execute commands
find . -name '*.tmp' -exec rm {} \;
find . -type f -exec chmod 644 {} +  # More efficient
```

---

# Finding Content

## grep Basics
```bash
# Basic search
grep "pattern" file.txt

# Recursive search
grep -R "pattern" .
```

--

## Modern Alternatives
### ripgrep (rg) faster than grep
- [GitHub: ripgrep](https://github.com/BurntSushi/ripgrep)
```bash
# ripgrep examples
rg -t py 'import requests'    # Search Python files
rg -C 5 'pattern'            # Show context
rg --stats PATTERN           # Show statistics
```

--

### ag (The Silver Searcher)
- [GitHub: The Silver Searcher](https://github.com/ggreer/the_silver_searcher)

```bash
ag --python 'import'         # Search Python files
ag -l 'pattern'             # List matching files
```

### bat - better file viewer
- [GitHub: bat](https://github.com/sharkdp/bat)

```bash
bat file.txt                # Syntax highlighting
bat -A file.txt             # Show all characters
```

---

# Shell History

## Basic History
```bash
history                # Show history
!n                    # Run command n
!!                    # Run last command
!$                    # Last argument
```

--

## History Features
```bash
# Search history
Ctrl+R                # Reverse search

# Ignore commands
HISTCONTROL=ignorespace   # Ignore commands starting with space
HISTCONTROL=ignoredups    # Ignore duplicates
```

---

# Directory Navigation

## Smart Navigation Tools
- zoxide - [GitHub: zoxide](https://github.com/ajeetdsouza/zoxide)
- autojump - [GitHub: autojump](https://github.com/wting/autojump)

```bash
z dotfiles            # Jump to high frequency directory
j project            # Jump to project directory
```

--

## Directory Overview
- tree - [GitHub: tree](https://github.com/kyohe/tree)
- nnn - [GitHub: nnn](https://github.com/jarun/nnn)
- broot - [GitHub: broot](https://github.com/Canop/broot)

```bash
tree                # Show directory tree
nnn                 # Terminal file manager
broot               # Interactive tree view
```

---

# Exercises

## Exercise 1: Advanced ls Command

Create an ls command that lists files in the following manner:
- Includes all files, including hidden files
- Sizes are listed in human readable format (e.g. 454M instead of 454279954)

<div class="more-arrow">⬇️</div>


--

- Files are ordered by recency
- Output is colorized
- Shows detailed information (permissions, owner, size)

<div class="solution-hint">
💡 Solution Below
<span class="arrow">⬇️</span>
</div>

--

```bash
# Solution
ls -lahrt --color=auto

# This will show output like:
-rw-r--r--   1 user group 1.1M Jan 14 09:53 baz
drwxr-xr-x   5 user group  160 Jan 14 09:53 .
-rw-r--r--   1 user group  514 Jan 14 06:42 bar
-rw-r--r--   1 user group 106M Jan 13 12:12 foo
```

Testing:
Try it in different directories to see how it handles various file types and sizes.

--

## Exercise 2: Marco Polo Functions

Write two bash functions that do the following:
- `marco`: Saves the current working directory in a variable
- `polo`: `cd`s back to the directory where marco was called
- Should work from any directory
- Should handle errors (e.g., if marco wasn't called)

<div class="solution-hint">
💡 Solution Below
<span class="arrow">⬇️</span>
</div>

--

```bash
# Solution
marco() {
    export MARCO_PATH=$(pwd)
    echo "Saving current path: $MARCO_PATH"
}

polo() {
    if [ -n "$MARCO_PATH" ]; then
        cd "$MARCO_PATH" || echo "Failed to cd to $MARCO_PATH"
        echo "Returning to: $MARCO_PATH"
    else
        echo "No path saved! Use marco first."
    fi
}

```

#### Testing procedure:
```bash
source marco.sh
cd /path/to/somewhere
marco
cd /somewhere/else
polo   # should return to /path/to/somewhere
```

--

## Exercise 3: Debug Script

Create a script to debug a command that fails rarely:
- Run the given script until it fails
- Capture both stdout and stderr
- Report how many runs it took to fail
- Save the output for debugging
- Handle the case where the script never fails

<div class="solution-hint">
💡 Solution Below
<span class="arrow">⬇️</span>
</div>

--

```bash
#!/usr/bin/env bash

# Solution
count=0
until [[ "$?" -ne 0 ]]; do
    count=$((count+1))
    ./random.sh &> out.txt
    echo -n "." # Show progress
    if ((count >= 1000)); then
        echo "Reached maximum attempts"
        exit 1
    fi
done

echo -e "\nFound error after $count runs"
echo "Output from failed run:"
cat out.txt
```

--

#### Test script (random.sh):
```bash
#!/usr/bin/env bash
n=$(( RANDOM % 100 ))
if [[ n -eq 42 ]]; then
    echo "Something went wrong"
    >&2 echo "The error was using magic numbers"
    exit 1
fi
echo "Everything went according to plan"
```

--

## Exercise 4: HTML Archive

Write a command that:
- Recursively finds all HTML files in the current folder
- Creates a zip/tar archive containing these files
- Properly handles filenames with spaces and special characters
- Maintains directory structure in the archive

<div class="solution-hint">
💡 Solution Below
<span class="arrow">⬇️</span>
</div>

--

```bash
# Solution for Linux
find . -type f -name "*.html" -print0 | \
    xargs -0 tar -czf archive.tar.gz

# Solution for macOS
find . -type f -name "*.html" -print0 | \
    xargs -0 zip html_archive.zip

# Alternative with better progress display
find . -type f -name "*.html" -print0 | \
    tar --null -czf archive.tar.gz --files-from=-

```
#### Testing:
1. Create test files with spaces
2. Create nested directories with HTML files
3. Extract archive and compare contents

--

## Exercise 5: Recent Files

Write commands to:
- Find the most recently modified file in a directory
- List all files by recency
- Handle hidden files
- Support recursive search
- Format output nicely

<div class="solution-hint">
💡 Solution Below
<span class="arrow">⬇️</span>
</div>

--

```bash
# Most recent file
find . -type f -printf '%T+ %p\n' | \
    sort -r | head -n 1

# List all by recency with details
find . -type f -printf '%T+ %s %p\n' | \
    sort -r | \
    awk '{printf "%-20s %10d bytes  %s\n", $1, $2, $3}'

# Alternative using ls (less features but more portable)
ls -t -1 | head -n 1  # Most recent
ls -lath             # All by recency with details

```
### Testing:
1. Create files with different timestamps
2. Test in directories with hidden files
3. Test with different file types

---

# 🎯 Practice Tips

- 🔰 Start with simple scripts
- 🐛 Use shellcheck for debugging
- 🧪 Test scripts with sample data
- 📈 Build complexity gradually
- 📝 Document your code with comments

---

# 📚 Additional Resources

## Documentation
- 📖 man pages (`man command`)
- 📱 tldr pages (`tldr command`)
- 📗 GNU Coreutils documentation (`info coreutils`)

--

## 🌐 Online Resources
- 🎮 [Command Line Challenge](https://cmdchallenge.com/)
- 📘 [Bash Scripting Tutorial](https://linuxconfig.org/bash-scripting-tutorial)
- ✅ [ShellCheck](https://www.shellcheck.net/)

> 💡 Remember: Regular practice is key to mastering shell scripting!

---

<!-- .slide: data-background="linear-gradient(120deg, #4B1248 0%, #F0C27B 100%)" -->

## Course Complete! 🎉

### Congratulations on completing the Shell Series!

You've learned:
- 🔰 Shell Fundamentals
- 🛠️ Shell Tools & Scripting
- 🔄 Automation Techniques
- 🎯 Best Practices

--

<!-- .slide: data-background="linear-gradient(120deg, #2C3E50 0%, #3498DB 100%)" -->

## Stay Connected 🤝

- 📧 Contact: [shiyafc@gmail.com](mailto:shiyafc@gmail.com)
- 🌐 Website: [learn-shell.mshiyaf.com](https://learn-shell.mshiyaf.com)
- 💼 LinkedIn: [Shiyaf C](https://linkedin.com/in/mshiyaf)
- 🐙 GitHub: [@mshiyaf](https://github.com/mshiyaf)

> "The command line is where the magic happens!" - Shiyaf C

--

<!-- .slide: data-background="linear-gradient(120deg, #1a2a6c 0%, #2980B9 100%)" -->

## Continue Learning 📚

- 🔍 Explore Advanced Topics
- 🛠️ Build Shell Scripts
- 🎯 Practice Daily
- 🤝 Join Shell Communities
- 📚 Read Shell Documentation

Remember: The best way to master the shell is through regular practice!
