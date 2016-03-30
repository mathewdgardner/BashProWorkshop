# Arguments <a id="arguments"></a>

Sometimes it is useful for a script to do things conditionally depending on what inputs you give it. This can be achieved by passing arguments to in the command line. No doubt you have already been doing this!

```sh
$ bash my-script.sh one two three
```

In the above example, I passed three arguments to a script `my-script.sh`. Inside your script you can access these by using the `$1`, `$2`, `$3` variables.

> Note `$0` will give you the name of the script itself.

> Double note, the number of arguments you pass is practically unlimited for our purposes!

There are many others, such as `$?`, `$@` and `$$` that you may be interested. Be sure to check out the [resources](#resources) section.

# Aliases <a id="aliases"></a>

Sometimes it is useful to make shortcuts for ourselves because we are lazy, or the commands themselves are too long to remember exactly. Aliases help with that but are only good for simple commands.

```sh
$ alias ls="ls -alh"
```

Normally, the vanilla `ls` command simply lists files in a directory. But that's not always very useful. `ls` has many options we can turn on and we might want those options to always be there by default. We can solve this particular problem with an alias as shown above. The aliased version of `ls` will now always show all files, in a list format and show file sizes in a human readable format.

> Note that if you want to define an `alias` inside of a script you will have trouble. By default, in a non-interactive shell, aliases are not expanded. You can change this behavior by adding `shopt -s expand_aliases` before you define your aliases.

# Functions <a id="functions"></a>

Aliases are great and all but they are limiting in the way that they won't expand past the first word in a simple command nor will they expand variables. For this you will need to define a bash function. The basic syntax looks something like this:

```sh
function echoAllTheThings() {
  echo $1 $2 $3
}

echoAllTheThings one two three
```

# Resources <a id="resources"></a>

  - [Arguments](http://www.gnu.org/software/bash/manual/bash.html#Shell-Parameters)
  - [Aliases](http://www.gnu.org/software/bash/manual/bash.html#Aliases)
  - [Functions](http://www.gnu.org/software/bash/manual/bash.html#Shell-Functions)
