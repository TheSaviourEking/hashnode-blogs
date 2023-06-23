---
title: "Transform Your Terminal: A Step-by-Step Guide to Show Git Branch in Bash Prompt"
seoTitle: "How to Show Git Branch in Bash Prompt"
seoDescription: "Enhance productivity: display Git branch, add color, and optimize your command line, customize terminal and improve workflow. #Bash #Git #Commandline #codej"
datePublished: Fri Jun 23 2023 13:00:39 GMT+0000 (Coordinated Universal Time)
cuid: clj8kygb70ot70fnvb7cm3zqb
slug: show-git-branch-in-bash-prompt
canonical: https://www.linkedin.com/pulse/transform-your-terminal-step-by-step-guide-show-git-branch-eking/
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1687489952454/41ce3122-f5d8-478d-a4e0-5b8d5690543f.png
tags: bash, git, command-line, programming-ciovqvfcb008mb253jrczo9ye, bash-script

---

As a software developer, you likely spend significant time in the terminal. The terminal is indispensable whether you're working with Git, running scripts, or just navigating your file system. But did you know that you can customize your terminal to make your workflow even more efficient?

A straightforward customization that can make a big difference is adding the Git branch name to your terminal prompt. This small change can help you stay organized and save time while working on multiple branches. In this article, we'll go over how to add the Git branch name to your bash prompt and show you how to take your terminal customization to the next level.

## Launch Your Terminal

Your native bash prompt looks like this

![native bash shell in linux](https://media.licdn.com/dms/image/D4D12AQGefTtGm3mUnQ/article-inline_image-shrink_1500_2232/0/1675859494404?e=1692835200&v=beta&t=a13ykcudNytC2-5KkfdnNNo33FkSIXp6fCWVFnthvlg align="left")

Navigate to a local git repository or use ***"git init"*** to initialize a new local repository.

![bash shell with git active](https://media.licdn.com/dms/image/D4D12AQFJDby1IsRq4Q/article-inline_image-shrink_1500_2232/0/1675859690203?e=1692835200&v=beta&t=G8k5FMwkMlO9yJPSx-epaqeGm92m4DLtIqJr6cHFj6k align="left")

We are in a git repository, and it still looks the same; nothing to let us know which branch we are currently working on, so we would have to run the ***git branch*** each time we need to check our current branch to avoid pushing code to the wrong branch.

Let’s begin

To display the branch name in the bash prompt. You need to edit the **PS1** variable in the bash environmental variables (set value of PS1 in ~/.bash\_profile).

## What is PS1

PS1 denotes Prompt String 1. It is one of the prompts available in the Linux/UNIX shell. The first thing you see is stored in your PS1 variable whenever you open your terminal.

Following is an example bash prompt of my terminal. Here I have defined to display

\* **user** — root 

\* **hostname of machine** — e29b7cc37a65

\* **current working directory** — ~/ (home)

![No alt text provided for this image](https://media.licdn.com/dms/image/D4D12AQEZyjRa-t61mw/article-inline_image-shrink_1500_2232/0/1675859846152?e=1692835200&v=beta&t=xDoAw0-CoxonoJhaiuFaTDhIRcLJsj_3WeGCH-ctHYE align="left")

I am currently signed in as root on this machine; yours would show your username.

P.S. ~/ is the home directory

**Step 1**: Open your .bashrc File

The first step to customizing your terminal is to open your .bashrc file. This file is a script file that runs every time you start a new terminal session, and it's where you can specify customizations for your terminal.

To open your .bashrc file, type the following command in your terminal:

```bash
vi ~/.bashrc
```

This will open the file in the vi text editor. If you prefer to use a different text editor, such as nano or vs code, simply replace "vim" with the name of your preferred editor.

**Step 2**: Edit the PS1 Variable

The PS1 variable is used to specify the format of the terminal prompt. You'll need to edit this variable to add the Git branch name to your prompt.

At the bottom of the .bashrc file, add the following line:

```bash
parse_git_branch() 
   git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
PS1="${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m
\]:\[\033[01;34m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "{
```

![editing ~.bashrc to add git branch](https://media.licdn.com/dms/image/D4D12AQFC8hZyOeiBtQ/article-inline_image-shrink_1500_2232/0/1675859948168?e=1692835200&v=beta&t=Cut_8xbQT-GrHFJG1LaxXFX65QOHxGEUKdQculQnEQE align="left")

Here, parse\_git\_branch() function extracts the branch name when you are in a git repository. This function output is used in the PS1 variable to prompt the branch name.

In the above PS1, we defined the following properties

${debian\_chroot:+($debian\_chroot)} – is a conditional expression that checks if the "debian\_chroot" environment variable is set. If it is set, it adds the value of "debian\_chroot" in parentheses after the prompt. Indicate that the user is in a Debian chroot environment.

\* `\u@\h\[\033[00m\]:\[\033[01;34m\]\`— user, hostname and it's displaying color

\* `w\[\033[33m\]`— current working directory, and it's displaying color

\* `\$(parse_git_branch)\[\033[00m\]` — git branch name and its displaying color

This line specifies that the Git branch name should be displayed in yellow, preceded by the username and hostname in green and the current working directory in blue.

**Step 3**: Save and Close the File

Once you've added the line to your .bashrc file, save your changes and close the file. In vim, you can save your changes by pressing "Esc," then ":wq," and finally "Enter."

**Step 4**: Reload the .bashrc File

The final step is to reload the .bashrc file, so your changes take effect. To do this, type the following command in your terminal:

```bash
source ~/.bashrc
```

Then reload your terminal.

That's it! You should now see the Git branch name in your terminal prompt. This small change can make a big difference in your workflow, saving time and helping you stay organized.

![ reloaded bash prompt](https://media.licdn.com/dms/image/D4D12AQGHBpPVSulEJA/article-inline_image-shrink_1500_2232/0/1675860226252?e=1692835200&v=beta&t=JrmzLzhsXsNUN9X68PmDkxj34zWVrm3NBVW0QKfSTjo align="left")

Now my bash prompt is colored! Wait a minute. It is not displaying the git branch.

Okay, let’s navigate to our previous git repository.

Voilà,

![bash prompt showing git branch with color](https://media.licdn.com/dms/image/D4D12AQFBWMPSho80hg/article-inline_image-shrink_1500_2232/0/1675860267528?e=1692835200&v=beta&t=1VjUdkUPbz0K-CU7TRHiNA0wf_oOu1Vik_BHDqcGaEM align="left")

Yeah, and some more validation

![ bash prompt showing git branch](https://media.licdn.com/dms/image/D4D12AQHogjvyh458Cw/article-inline_image-shrink_1500_2232/0/1675860307652?e=1692835200&v=beta&t=sDJJoR4Bq3MqUa1Y2KXn-LHFe0nPj7BMu78ibGym1HA align="left")

Oh yeah!, let's celebrate as you made it. A new terminal geek is born

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1687483088201/9bd736a1-59fa-4e48-bb2f-95a1120c0baf.gif align="center")

### **Advanced Terminal Customizations**

Now that you've added the Git branch name to your prompt, you may wonder what other customizations you can make to your terminal. Here are a few ideas to get you started:

* **Change the color scheme**: If you don't like the default color scheme of your terminal, you can easily change it. There are many color schemes available online that you can use or create your own. [Check here for a little resource](https://gist.github.com/vratiu/9780109) on how shell colors work and more color codes you could customize your shell with.
    
* **Show Git status**: In addition to the Git branch name, you can also display the Git status in your terminal prompt. This will give you a quick overview of the changes you've made to your repository.
    
* **Show the current time:** If you're always aware, you can add the current time to your terminal prompt. This can be especially helpful when you're working on a deadline task.
    
* **Add shortcuts**: You can create shortcuts for frequently used commands to save time and make your workflow more efficient. For example, you could create a shortcut for "cd .." to quickly navigate up one directory.
    
* **Add a custom banner**: You can add a custom banner to your terminal that displays information such as your name, job title, or motivational quote. This can help you stay focused and motivated while you're working.
    

To implement these customizations, you'll need to modify the .bashrc file similarly to what we showed you for adding the Git branch name. There are many tutorials and resources available online that can help you with these customizations.

### **Conclusion**

Customizing your terminal is a simple and effective way to make your workflow more efficient. By adding the Git branch name to your bash prompt, you can stay organized and save time while working on multiple branches. You can make many other customizations to your terminal, and we've provided a few examples to get you started. So go ahead, take some time to customize your terminal, and start enjoying a more efficient Git workflow today!