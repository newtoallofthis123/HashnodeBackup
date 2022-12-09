# Search For Files in The Terminal

## TLDR;
Okay, So the find utility in linux sucks. There are alternatives to find out there, like [fd-find](https://github.com/sharkdp/fd), but why not build our own small utility nicknamed gf to help us find files in our terminal. For this, we pipe the output of `ls -a` to grep and show the results. For a better experience, instead of grep, use [ripgrep](https://github.com/BurntSushi/ripgrep) and replace grep with rg in the code. To use it, just paste the following in your config file.
```bash
alias gf="ls -a | grep -i $1"
```

## Why To Change
The main reason to change from find to other stuff is because, though find has some good uses and use cases, for the most part, find sucks. You have to provide the exact string for it to work and it honestly not very use friendly.

## Other Tools
Okay, usually when people talk about upgrading your terminal search experience, they talk about mostly rust tools like [fd-find](https://github.com/sharkdp/fd) among others, which are excellent on their own but won't it be better and more encouraging if we can do the same thing, without any dependencies and any upgrading. All you will need is a command line with any form of bash installed and any shell prompt like zsh, bash or fish. On windows, you can look into [git bash](), but if you on a unix based operating system like mac os or ubuntu, you are good to go.

## What is grep
Okay, so grep is a gnu based util that basically helps you pick out your query and shows you the results. It is different from find because it actually opens the file contents and checks for the string provided, so it is more in depth search. Try grep with
```bash
$ grep -i "test"
```
This is show you all the instances with "test" in it. We will be piping the ls command into grep to get the results in a limited data set.

## Logic and Setup
We are basically going to pipe the `ls -l` command to grep to find all the instances of a term we provide as
an argument, all with the power of bash and bash aliasing.

First we must open our configuration file to set and alias everytime we open our prompt. For each replace the variable with the respective command
- bash: `~/.bashrc`
- zsh: `.~/zshrc`
- fish: `~/.config/fish/config.fish`
```bash
$ nano ~/.bashrc
```
This should open it up in the inbuilt nano text editor. I am using bash, so this was the result in my case

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662646789522/i4BLk8VIK.png align="left")

Scroll down to the bottom of the file and add the following line at the end of it.
```bash
alias gf='ls -a | grep -i $1'
```
Now press `Crtl + O` and press enter to save the file changes and then press `Crtl + X` to exit. Now restart the shell to see the changes. Now, if you ask your gf about a file, it will show you the output as follows

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1662647071127/whEw7x6th.png align="left")

In this, we basically pipe the ls -a output to grep and use the -i operator to ignore case and the $1 to access the first argument passed.

## RipGrep

You can just stick to using grep, but you can get better color syntaxing and speed by using a rust powered tool called [ripgrep](https://github.com/BurntSushi/ripgrep). if yo can on ubuntu, you can install it with `sudo apt install ripgrep`. To tell your gf to use ripgrep instead of grep, use this code instead of the one given above

```bash
alias gf='ls -a | rg -i $1'
````

## Conclusion

Hence you have a gf who gets you the system file you need and hence lets you relax a bit while using the terminal. Hope you enjoyed this fun beginner friendly article and if you did please be sure to follow my blog and check out some of my projects.