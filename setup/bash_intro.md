# Introduction to Bash Scripting

## What is Bash?
Bash, short for **Bourne Again Shell**, is a Unix shell and command-line interpreter. It is widely used as the default shell in many Linux distributions and macOS systems. Bash allows users to execute commands, automate tasks, and write shell scripts for repetitive or complex workflows.

## Why Learn Bash?
Learning Bash scripting provides several benefits:
- **Automation**: Automate repetitive tasks to save time and reduce errors.
- **System Administration**: Manage and configure systems efficiently.
- **Programming**: Write scripts to solve problems or manipulate data quickly.

## Basics of Bash

### Running Commands
In Bash, you can execute commands by typing them directly into the terminal. For example:
```bash
ls
pwd
echo "Hello, World!"
```

### Writing a Script
A Bash script is a file containing a series of commands. Scripts usually start with a shebang (`#!`) to specify the interpreter:
```bash
#!/bin/bash
# This is a comment

echo "This is my first script!"
```
Save the script as `script.sh`, then make it executable and run it:
```bash
chmod +x script.sh
./script.sh
```

### Variables
Variables store values that can be used later in the script:
```bash
#!/bin/bash
name="Alice"
echo "Hello, $name!"
```

### Conditionals
Bash supports conditional statements like `if`:
```bash
#!/bin/bash
if [ "$1" == "hello" ]; then
  echo "You said hello!"
else
  echo "You didn't say hello."
fi
```

### Loops
You can use loops to iterate over items:
```bash
#!/bin/bash
for i in {1..5}; do
  echo "Number $i"
done
```

### Functions
Define reusable blocks of code using functions:
```bash
#!/bin/bash
function greet {
  echo "Hello, $1!"
}

greet "Bob"
```

## Tips for Effective Scripting
1. **Use Comments**: Add comments to explain complex parts of your script.
2. **Error Handling**: Check for errors using conditional statements and exit codes.
3. **Debugging**: Use `set -x` to debug scripts line by line.

## Resources
- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [Bash Beginner's Guide](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
- [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)

Happy scripting!
