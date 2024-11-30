# Shell Tools and Scripting
---

## Introduction

In this lecture, we will cover:
- Basics of using bash as a scripting language
- Common shell tools for the command line

---

## Shell Scripting

### Introduction to Shell Scripting

- Execute commands and pipe them together
- Use control flow like conditionals and loops
- Bash scripting focuses on shell-related tasks:
  - Command pipelines
  - File operations
  - Reading from standard input

---

### Variables in Bash

- Assign variables with `foo=bar`
- Access with `$foo`
- Beware of spaces: `foo = bar` is invalid

Example:
```bash
foo=bar
echo "$foo"  # prints bar
echo '$foo'  # prints $foo
```

---

### Control Flow in Bash

- `if`, `case`, `while`, `for` control structures
- Functions take arguments:
```bash
mcd () {
    mkdir -p "$1"
    cd "$1"
}
```

---

### Special Variables

| Variable | Meaning                                    |
|----------|--------------------------------------------|
| `$0`     | Name of the script                        |
| `$1`-`$9`| Arguments to the script                   |
| `$@`     | All arguments                             |
| `$#`     | Number of arguments                       |
| `$?`     | Return code of the previous command       |
| `$$`     | Process ID of the current script          |
| `!!`     | Entire last command                       |
| `$_`     | Last argument of the last command         |

---

### Return Codes and Operators

- Use `&&` (AND), `||` (OR), `;` (sequential) for chaining commands
```bash
true && echo "Success"
false || echo "Fail"
true ; echo "This will always run"
```

---

### Command Substitution

- Capture command output:
```bash
current_date=$(date)
echo "Today's date: $current_date"
```

- Process substitution:
```bash
diff <(ls dir1) <(ls dir2)
```

---

## Shell Tools

---

### Finding Command Help

- Use `man <command>` for detailed help
- Example:
```bash
man ls
```

- For quick usage examples, use [tldr](https://tldr.sh):
```bash
tldr tar
```

---

### Finding Files

- Using `find`:
```bash
find . -name "*.py" -type f
find . -mtime -1
```

- Perform actions:
```bash
find . -name "*.tmp" -exec rm {} \;
```

---

### Searching Code

- Use `grep` for searching text:
```bash
grep -R "pattern" .
```

- Alternatives like `ripgrep (rg)`:
```bash
rg "pattern"
```

---

### History and Autosuggestions

- Access shell history with `history` or `Ctrl+R`
- Use tools like `fzf` or `zsh-autosuggestions` for enhanced navigation

---

### Directory Navigation

- Tools for fast navigation:
  - `fasd` or `autojump`
  - `z` to jump to frequently used directories

---

## Exercises

### Exercise 1: List Files

Write an `ls` command to:
- Include hidden files
- Show sizes in human-readable format
- Sort by recency
- Use colorized output

Example:
```bash
ls -lath --color=auto
```

---

### Exercise 2: Marco and Polo

Write bash functions `marco` and `polo`:
```bash
marco() {
    export MARCO=$(pwd)
}
polo() {
    cd "$MARCO"
}
```

---

### Exercise 3: Debugging Script

Run a script until it fails, capturing output:
```bash
#!/usr/bin/env bash
count=0
until ./random.sh &> out.txt; do
    count=$((count+1))
done
echo "Failed after $count runs"
cat out.txt
```

---

### Exercise 4: Find HTML and Zip

Find and zip all HTML files:
```bash
find . -type f -name "*.html" | xargs -d '\n' tar -czvf archive.tar.gz
```

---

### Exercise 5: Find Most Recent File

Find the most recently modified file:
```bash
find . -type f -printf '%T@ %p\n' | sort -n | tail -1
```

---

## Conclusion

- Bash scripting and shell tools are essential for efficient command-line workflows.
- Practice and explore tools like `find`, `grep`, `ripgrep`, and `fzf`.

---

## Questions?

```

### Hosting Instructions
1. Save this Markdown content to a file (e.g., `presentation.md`).
2. Use Reveal.js with Markdown support to serve it as described in the previous steps.

Let me know if you’d like help hosting this or making further customizations!
