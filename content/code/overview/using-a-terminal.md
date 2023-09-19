---
title: Using a Terminal
---

## The Rundown

The terminal (or "CLI") is an essential part of coding. It's a way to interact with your computer using "shell" commands.

There are various shells, but the most common one is called "bash." Windows uses a different shell called "cmd" or "powershell." Mac and Linux use bash. Knowing them all is useful, but bash is where I'd start.

### Why Use a Terminal?

The terminal is **powerful**. It can automate tasks, run programs, and do things that would be difficult to do otherwise. It's also **fast**. It's often faster to type a command than to click through a GUI. It's also **portable**. You can use the same commands on any computer.

---

## The Basics

### Opening a Terminal

On Mac, open the "Terminal" app. On Windows, open the "Command Prompt" app. On Linux, open the "Terminal" app.

### Navigating Directories

A core concept of the terminal is the "current directory." This is the directory that you're currently in. You can see the current directory by running the `pwd` command (print working directory).

What's a directory? It's a folder. Directories can contain files and other directories. To see what's in the current directory, run the `ls` command (list directory contents).

```bash title="ls-example.txt"
$ ls
Tensor.py    TensorMap.py __init__.py  __pycache__

$ ls -lah
total 16
drwxr-xr-x  6 user  staff   192B Sep 12 13:46 .
drwxr-xr-x  5 user  staff   160B Sep 12 13:46 ..
-rw-r--r--  1 user  staff   2.6K Sep 12 13:46 Tensor.py
-rw-r--r--  1 user  staff   2.0K Sep 12 13:46 TensorMap.py
-rw-r--r--  1 user  staff     0B Sep 12 13:46 __init__.py
drwxr-xr-x  5 user  staff   160B Sep 12 13:46 __pycache__
```

To move into a directory, run the `cd` command (change directory). For example, to move into the "Documents" directory, run `cd Documents`.

To move to an "absolute" directory, run `cd /path/to/directory`. To move to a "relative" directory, run `cd path/to/directory`. To move back out of a directory, run `cd ..`. 

### Creating Files and Directories

There are various commands to do these kinds of tasks, but most of the time you'll be using `touch` and `mkdir` to create files and directories respectively.

```bash title="touch-example.txt"
$ touch hello.txt
$ ls
hello.txt
```

Alternatively, you can create a file that contains text like this:

```bash title="echo-example.txt"
$ echo "Hello, World!" > hello.txt
$ cat hello.txt # cat prints the contents of a file
Hello, World!
```

### Using a Text Editor

`vim` is a widely used text editor for the terminal. It's a bit difficult to master, but learning the basics isn't that bad. `nano` is another text editor that's easier to use.

The advantage of using a text editor is that you can edit files without leaving the terminal.

### Running Programs

To run a program, first it needs to be "executable." To make a program executable, you'll use `chmod +x ...`. Assuming the program is executable, you can run it by typing the name of the program. For example, to run a program called "hello", run `./hello`.

---

## Advanced Concepts

### Pipes

Pipes are a way to connect the output of one command to the input of another command. For example, to print the contents of a file and then count the number of lines, you can run `cat hello.txt | wc -l`.

### Environment Variables

Environment variables are variables that are available to all programs. They're often used to store configuration information. To set an environment variable, run `export VAR_NAME=var_value`. To see all environment variables, run `env`.

### $PATH

The `$PATH` variable is a special environment variable that contains a list of directories. When you run a command, the terminal will look through each directory in `$PATH` to find the command. If you ever see an error like "command not found", it's likely because the command isn't in `$PATH`.

---

## Beginner Friendly Tools

>[!note]
>Some of these tools are built-in and some need to be installed. On Windows, you may need a Unix emulator like [Cygwin](https://www.cygwin.com/). Linux or macOS is a better experience in my opinion.

- [git](https://git-scm.com/) - A version control system.
- [tldr](https://tldr.sh/) - A simplified version of `man`.
- [ping](https://linux.die.net/man/8/ping) - A command-line tool for testing network connections.
- [tree](http://mama.indstate.edu/users/ice/tree/) - A command-line tool for displaying directories as a tree.
- [bat](https://github.com/sharkdp/bat) - A prettier version of `cat`.
- [ps](https://linux.die.net/man/1/ps) - A command-line tool for listing processes.
- [file](https://linux.die.net/man/1/file) - A command-line tool for determining the type of a file.
- [htop](https://hisham.hm/htop/) - A command-line tool for monitoring system resources.
- [brew](https://brew.sh/) - A package manager for Mac.
- [apt](https://wiki.debian.org/Apt) - A package manager for Linux.
- [chocolatey](https://chocolatey.org/) - A package manager for Windows.
- [oh-my-zsh](https://ohmyz.sh/) - A framework for managing zsh.
- [npm](https://www.npmjs.com/) - A package manager for JavaScript.
- [man](https://linux.die.net/man/1/man) - A command-line tool for reading documentation on any command.
- [mkdir](https://linux.die.net/man/1/mkdir) - A command-line tool for creating directories.
- [touch](https://linux.die.net/man/1/touch) - A command-line tool for creating files.
- [echo](https://linux.die.net/man/1/echo) - A command-line tool for printing text.
- [cat](https://linux.die.net/man/1/cat) - A command-line tool for printing files.
- [dig](https://linux.die.net/man/1/dig) - A command-line tool for querying DNS.
- [cp](https://linux.die.net/man/1/cp) - A command-line tool for copying files.
- [mv](https://linux.die.net/man/1/mv) - A command-line tool for moving files.
- [rm](https://linux.die.net/man/1/rm) - A command-line tool for removing files
  - Be careful! There is no trash bin with `rm`.
- [date](https://linux.die.net/man/1/date) - A command-line tool for printing the date.

---

## More Advanced Tools

These tools take more time to learn, but they can be very useful.

- [tmux](https://github.com/tmux/tmux/wiki) - A terminal multiplexer.
- [ffmpeg](https://ffmpeg.org/) - A command-line tool for manipulating video.
- [jq](https://stedolan.github.io/jq/) - A command-line JSON processor.
- [grep](https://www.gnu.org/software/grep/) - A command-line tool for searching text.
- [sed](https://www.gnu.org/software/sed/) - A command-line tool for editing text.
- [awk](https://www.gnu.org/software/gawk/) - A command-line tool for processing text.
- [curl](https://curl.haxx.se/) - A command-line tool for transferring data.
- [docker](https://www.docker.com/) - A tool for running containers.
- [Fx](https://github.com/antonmedv/fx) - A command-line JSON viewer.