# Shebang <a id="shebang"></a>

Typically the first line in a shell script is a line leading with `#!`. This tells the program loader to run the upcoming commands in the given interpreter. Common ones you might find in the wild:

  - `#!/bin/sh`
  - `#!/bin/bash`
  - `#!/usr/bin/perl`
  - `#!/usr/sbin/python`
  - `#!/usr/local/bin/ruby`
  - `#!/usr/local/sbin/php`
  - `#!/usr/bin/env node`

> Note: I made these paths up to showcase the different locations you might find them. Actual location depends on your distribution.

Afterwards you can author any arbitrary set of commands you need. For example:

```sh
#!/usr/bin/env bash

containers=$(docker ps -a | awk '{print $NF}')

for container in $containers; do
  if [ "$container" == "NAMES" ]; then
    continue;
  fi

  if [ ! -z $container ]; then
    docker logs $container > $CIRCLE_ARTIFACTS/$container.log 2>&1
  fi
done
```

Don't worry too much about understanding right now. As we go on we will cover many topics, such as variables and variable expansion, control flow, pipes, streams and more.

Veterans may notice that this script might be overly verbose with an unnecessary if statement if we skip the first line and this is OK. This script gets the job done and as we all know there are many right ways. Is it the best way? No, but it's pretty good.

For those curious:

```sh
#!/usr/bin/env bash

containers=$(docker ps -a | tail -n +2 | awk '{print $NF}')

for container in $containers; do
  if [ ! -z $container ]; then
    docker logs $container > $CIRCLE_ARTIFACTS/$container.log 2>&1
  fi
done
```

# Common Commands <a id="common"></a>

There are many commands available. I come across new ones all the time as it's always an ongoing learning experience. Here are some invaluable commands many of which you are probably already familiar with (in no particular order):

  - `echo`    Print something
  - `cd`      Change directory
  - `ls`      List directory
  - `cat`     Concatenate
  - `mkdir`   Make a directory
  - `rm`      Remove something
  - `rmdir`   Remove an empty directory
  - `mv`      Move or rename something
  - `cp`      Copy something
  - `history` Show command history
  - `grep`    Search
  - `pwd`     Show present working directory
  - `man`     Show manual pages for command
  - `head`    Show first set of lines
  - `tail`    show last set of lines
  - `vi`      Editor
  - `more`    Text reader
  - `less`    Text reader
  - `find`    Find file(s)
  - `ssh`     Secure remote shell
  - `sed`     Stream editor
  - `awk`     Magic
  - `xargs`   Command arguments utility
  - `sort`    Sort things
  - `wc`      Show word count
  - `ps`      Show process information
  - `top`     Show system resources information
  - `chmod`   Change file modifiers such as permissions
  - `chown`   Change ownership of file(s)
  - `type`    Show definition of function or alias
  - `where`   Show where command (in your path) is located
  - `su`      Switch user
  - `sudo`    Switch user then do command

Each of these you can check the man pages to read more about them and their use. For example, `man rm`. Press `q` to exit the man pages.

# Variables 1 <a id="variables"></a>

In bash you can set string, numbers or arrays into a variable. The basic syntax is:

```sh
foo=bar
foo="bar"
foo="bar baz"
```

Note you cannot do `foo=bar baz` because whitespace is used to separate expressions. This would fail after setting the variable foo to hold the value bar and then try to run a command by the name of baz.

To access a variable you have set simple prefix the variable name with `$`. For example:

```sh
foo=bar
echo $foo
```

or in one line

```sh
foo=bar; echo $foo
```

Note that this does not work as you might expect:

```sh
foo=bar echo $foo
```

This is due to variable expansion. At the time of the command being evaluated `foo=bar` hasn't been run just yet. The shell wants to expand `$foo` first, which, at this time is nothing. The previous examples work because they were separated by either a new line or a semicolon. These tell the shell that the command is over and it's time to move on.

Try it.

# Control Statements 1<a id="control"></a>

###### if, elif, else <a id="if"></a>

Sometimes you want to execute commands conditionally. The syntax here is a bit tedious I admit, so pay close attention to the whitespace.

```sh
foo=bar

if [ "$foo" == "bar" ]; then
  echo "The value is bar!"
elif [ "$foo" == "baz" ]; then
  echo "The value is baz!"
else
  echo "The value is NOT bar or baz!"
fi
```

> Protip: Be extra careful with your variable expansion. Notice I placed `$foo` inside double quotes. Variables inside double quotes are interpolated, that means that they can still be evaluated. Placing them in double quotes allows whitespace to be allowed and not automatically truncated by the shell.

# switch, err, I mean case <a id="case"></a>

```sh
foo=bar

case $foo in
  bar) echo "The value is bar!" ;;
  baz) echo "The value is baz!" ;;
  *) "The value is NOT bar or baz!" ;;
esac
```

The if and case blocks above are equivalent.

> Note: Blocks often end in the reverse of the keyword that started it. The `if` block ends with the `fi` keyword. The `case` block ends with the `esac` keyword.

# [Now try the exercises!](lab.md)

# Resources <a id="resources"></a>

  - [Shebang](http://www.gnu.org/software/bash/manual/bash.html#Shell-Scripts)
  - [Common Commands](https://www.tjhsst.edu/~dhyatt/superap/unixcmd.html)
  - [If](http://www.gnu.org/software/bash/manual/bash.html#Conditional-Constructs)
  - [Case](http://www.gnu.org/software/bash/manual/bash.html#Conditional-Constructs)
