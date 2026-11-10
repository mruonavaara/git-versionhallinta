# Introduction to Version Control

## What is Version Control?

The purpose of version control is to store changes to source code versions such that:

- Different versions of the same software can be labeled without modifying the program code itself (e.g., file names)
- Earlier versions can be restored when necessary
- Multiple different versions of the software can be developed simultaneously in a controlled manner
- Changes made to the software can be tracked, documented, and managed

Version control makes work easier and more efficient for an individual developer. Most importantly, however, it enables efficient development of software within development teams.

Using version control is one of the fundamental skills of a professional software developer.

## What is Git?

There are many different version control systems. In practice, __Git__ has become the de facto standard for version control.

Git's popularity is likely because it is:

- Open source. Git is licensed under the open source GPLv2 license.
- Free.
- Distributed. It does not have any centralized server.
- Available for all environments.

## Git Repositories

Git stores all information locally in its own data storage, which is called a __repository__.

Almost all operations can be performed locally. This means you can develop and store software versions without an internet connection.

A repository is located on the local machine in the directory where the software is being developed.

## Repository Distribution and Synchronization

The contents of independent repositories can be __synchronized__ with each other. Of course, this requires a network connection.

![](assets/repo_sync.png)

Synchronizing repository contents makes it possible to share their contents among multiple developers. A typical model is that developers synchronize their own work to a repository located on a web service, and receive the work done by other developers through that synchronization.

## Getting Started with Git

### Command Line

Git has several graphical user interfaces, and even the Windows installation package includes one. However, in this course we use __command-line commands__. Most professionals do the same.

Windows has two __command shells__: _cmd_ and _powershell_. Git's Windows installation includes the _Git Bash_ command shell, which emulates the _bash_ command shell pre-installed on many Linux systems.

Git commands are the same in all command shells. Directory and file handling commands may differ in different command shells.

If command shell usage is unfamiliar to you, you can learn about it using material like this:

- [Command line crash course](https://developer.mozilla.org/en-US/docs/Learn/Tools_and_testing/Understanding_client-side_tools/Command_line)

!!! note "Note"

    In this material, bash commands are used for any file system commands.

    In Linux and iOS environments any unix command shell can be used, as the commands are the same.

### Configuration

After installation, it is necessary to perform some configuration before you can start using Git.

#### User Information

Each committed change stores the user's name and email address.
User information needs to be set on the computer only once, and can be changed later if needed.
```
git config set --global user.name "Markku Ruonavaara"
git config set --global user.email markku.ruonavaara@haaga-helia.fi
```

Configuration information can be stored at the system, user, and project levels. The `--global` option means that the setting is system and user-level: it applies to this computer (system) for all repositories of this user.

If no option is specified, the setting becomes project-specific. This means the setting applies only to the repository in which it was made.

#### Editor

In some operations, Git launches an editor for writing text. By default, it is the system's default editor, which is usually vim.

If you wish, you can set the editor that Git launches. The following command sets Visual Studio Code as the editor:

```
git config set --global core.editor "code --wait"
```

Configuration specifies the launch command, so if the editor is not found in the path, you may need to provide the full path.

However, if you ever end up in the vim editor, the following guide may be helpful:

- [https://www.linuxjournal.com/content/how-use-vi-editor-linux](https://www.linuxjournal.com/content/how-use-vi-editor-linux)

GitHub's documentation provides guidance on editor configuration:

- [https://docs.github.com/en/get-started/getting-started-with-git/associating-text-editors-with-git](https://docs.github.com/en/get-started/getting-started-with-git/associating-text-editors-with-git)

#### Viewing Configuration Settings

You can check all settings like this:
```bash
git config list
```

You can check the value of a single parameter by providing the parameter name to the `config` command:
```
git config user.email
```

## General Information About Git Commands

All Git commands start with `git`, followed by the actual __command__ (e.g., `config`). Commands can have __parameters__. In this example, the `config` command is given a parameter with the name of the desired configuration parameter `core.editor`:
```
git config core.editor
```
!!! note "Note"
    In this material, Git commands are referred to in the text using only the command part, e.g., `config`. The command to enter on the command line is then `git config`.

Commands can have __subcommands__ and can be given __options__, which clarify what you want to do.

In this example, `list` is a subcommand of the `config` command, and the `--global` option specifies that you want to list only global parameters that affect all your repositories:
```
git config list --global
```
Some options may also have a short form. For example, in the `git status --short` command, the `--short` option can also be given in the shorter form `-s`.

All commands provide brief help text with the `-h` option (short form of option `--help`):

```
$ git config -h
usage: git config list [<file-option>] [<display-option>] [--includes]
   or: git config get [<file-option>] [<display-option>] [--includes] [--all] [--regexp] [--value=<pattern>] [--fixed-value] [--default=<default>] [--url=<url>] <name>
   or: git config set [<file-option>] [--type=<type>] [--all] [--value=<pattern>] [--fixed-value] <name> <value>
   or: git config unset [<file-option>] [--all] [--value=<pattern>] [--fixed-value] <name>
   or: git config rename-section [<file-option>] <old-name> <new-name>
   or: git config remove-section [<file-option>] <name>
   or: git config edit [<file-option>]
   or: git config [<file-option>] --get-colorbool <name> [<stdout-is-tty>]
```

## Exercise 1

Let's get the environment ready for exercises.

1. Install Git on your computer.
2. Verify that the installation was successful by printing the Git version identifier:

    ```bash
    git --version
    ```
    or use the shorter form of the `--version` option:
    ```
    git -v
    ```

3. Install Visual Studio Code (or an equivalent programming editor).
4. Configure Git, at least user information and editor.
5. Create an account on the GitHub service. This will be used later in the course.

