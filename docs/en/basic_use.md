# Basic use

## Creating a repository

You can create a repository in a directory that is not yet under version control using the `init` command.

```bash
mkdir demo 		# create directory
cd demo		    # change to new directory as default
git init
```

The command creates an empty repository where you can store versions. The data is saved to a subdirectory named `.git`.
You can identify if a directory is under Git version control by the presence of the `.git` directory.

Files and directories whose names start with a dot are hidden and are not shown by default. You can make hidden directories visible using the `-a` option with the `ls` command. The `-l` option displays all information about files and directories.

``` bash
$ ls -l -a
total 31
drwxr-xr-x 1 h01975 1049089    0 Feb 15 15:04 ./
drwxr-xr-x 1 h01975 1049089    0 Feb 22 15:08 ../
drwxr-xr-x 1 h01975 1049089    0 Feb 15 15:04 .git/
-rw-r--r-- 1 h01975 1049089   81 Feb 15 12:36 .gitattributes
drwxr-xr-x 1 h01975 1049089    0 Feb 15 12:36 .github/
-rw-r--r-- 1 h01975 1049089  490 Feb 15 12:36 .gitignore
-rw-r--r-- 1 h01975 1049089   13 Feb 15 13:42 hello.txt
-rw-r--r-- 1 h01975 1049089 9305 Feb 15 12:36 readme.md
-rw-r--r-- 1 h01975 1049089   29 Feb 15 15:04 time.txt
```

To make hidden files visible in Windows File Explorer, you need to configure the File Explorer settings to show hidden files.

- [View hidden files and folders in Windows](https://support.microsoft.com/en-us/windows/view-hidden-files-and-folders-in-windows-97fbc472-c603-9d90-91d0-1166d1d9f4b5)

### Creating a repository from an existing repository

Often you want to copy an existing repository and continue working from it. This is done using the `clone` command, for example:

```
git clone https://github.com/libgit2/libgit2
```

The command adds a subdirectory libgit2 to the current directory, which contains a copy of the original repository's data (`.git`) and the latest version files. It also configures the original repository as the remote repository for the new repository.

This topic will be covered later in the section _Distributed Git_.

## Files in a Git directory

A directory that has a Git repository created in it is Git's __working directory__ (_working set_).

The files and subdirectories in the working directory can be brought under Git control. Files must be explicitly added to Git control to enable version control for them. The working directory may also contain files that are not under Git control.

From Git's perspective, files in the directory can be either:

- _Tracked_ (taken under Git management) or
- _Untracked_ (not under Git management).

A file under Git management in the working directory can be:

- _Unmodified_ - unchanged, the same as the latest stored version
- _Modified_ – changed, different from the latest stored version
- _Staged_ – marked to be included in the next commit

The following diagram shows different states and transitions between them.

1. Initially, a new file is in the `untracked` state
2. A new file can be marked to be included in the next commit using the `add` operation (_Add the file_), which changes its state to `staged`.
3. A file already under Git management is initially in the `unmodified` state
4. When a file under Git management in the directory changes (_Edit the file_), its state becomes `modified`.
5. Changed (and new) files can be marked to be included in the next commit using the `add` operation (_Stage the file_). Then files are in the `staged` state
6. When a commit is made, all file versions marked to be included in it are stored, and their state becomes `unmodified`.

![](assets/git_file_states.png)

You can check the Git status of files in the working directory with the `status` command.

```bash
git status
```

!!! tip "Tip"
    
    It is a good idea to check the Git status of your working directory (command `status`) before and after Git operations. This way you always know what is happening in your repository.

## Storing changes

Storing file versions is a two-step operation.

### Step 1: add

When a file is ready to be stored in version control, a new or modified file must be marked to be included in the next commit. This operation is called _staging_ in Git terminology and is done with the `add` command.

Files can be added to the next commit individually.

```bash
git add hello.html   # hello.html file will be included in the next commit
```

You can also add an entire directory, which adds all files in the directory and its subdirectories at once. Directories are also files, they are versioned too.

```bash
git add .		# dot refers to the current directory, all new and changed files will be included
```

Now the changed files are ready to be stored in version control. As you may have noticed, introducing a new file is a change just like modifying an existing one.

Git is aware of what needs to be stored, and we're ready for the `commit` operation.

### Step 2: commit

The actual storage happens with the `commit` command.

```bash
git commit
```

The command launches an editor where you can write a comment to be stored with the change. When you save and close, the change is written to the repository.

Write the topic of the change in the comment clearly, as it is important communication for yourself and your project team.

You can also write the comment on the command line without using an editor:

```bash
git commit –m "Add logout functionality"
```

!!! tip "Tip"

    If you have not configured anything else, Git opens the `vim` editor by default, which can be quite difficult to understand and use for the unfamiliar.

    You can exit the vim editor as follows:

    1. Press ++escape++ to enter command mode.
    2. Give the command `:wq` to save and exit the editor.

    After that, you can return to the [Git Getting Started chapter's configuration section](introduction.md#editor) and set your preferred Git editor.


## Viewing commits

You can view changes in the working directory compared to stored commits using the familiar `status` command. You should use it frequently to keep track of the Git status of your directory and its changes:

```bash
git status
```

You can see the history of `commit` storage with the `log` command.

```bash
git log
```

The command lists all commits in reverse chronological order. With the `--stat` option, Git adds a brief summary of the changes in the commits to the output:

```
git log --stat
```

You can view changes in a file in the working directory compared to the most recently committed version using the `diff` command.

```bash
git diff hello.html
```

## Removing and moving files

As mentioned earlier, directories are also versioned. If you want to delete a file from the repository or move a file to another directory, you are creating a new version of the directories.

The Git command `rm` removes a file from both the working directory and Git management. This change must also be stored in version control.

```bash
git rm test.txt
git commit -m "Removed unnecessary file"
```

Note that old stored versions remain in version control! What has been stored in version control stays there.

You can rename a file or move it to another directory using the Git command `mv`.

``` bash
git mv oldname.txt newname.txt
mkdir newdir
git mv newname.txt newdir
git add .
git commit -m "Reorganized files"
```

You can delete and move files within the repository using operating system commands (e.g., `rm` or `mv`). Changes are stored in Git management the same way as any other change: first `add`, then `commit`. The equivalent Git commands do not require the `add` step.

## Exercise 2
Let's practice basic operations.

Check the repository status with the `status` command regularly. Remember to write descriptive comment messages for your commits!

<div class="steps" markdown>

1. Create a directory on your computer for this course's exercises and create a Git repository in it.
2. Create a file in the repository (e.g., `test.txt`) and write something in the file. Store the file in Git management.
4. Create a file `hello.html` in the repository. The file content could be, for example:

    ``` html
    Hello world!
    ```

    Add these changes to Git management.

5. The content of the `hello.html` file is not yet HTML code. Add h1 markup to the text to make it an HTML element:

    ``` html
    <h1>Hello world!</h1>
    ```

    Add the change to version control.

6. Rename the `hello.html` file to `index.html` and store the change.
7. The test.txt file created first is now becoming unnecessary. Delete it from version control and store the change. Write a descriptive comment message for the commit.
8. Add a few more files and store them in version control.
9. View the commits you made using the `git log` command. Also try the command with the `--stat` option. What additional information do you get?
10. When you have completed the task, add the identifier `exercise2` to the latest commit by running the command

    ```
    git tag exercise2
    ```
</div>

## Going back in time

The introduction section claimed that with version control, it is possible to restore earlier versions of the software. Let's try that next.

Let's look at the output of the Git command `log`:
```
commit 6fa5fd1b94a163464aaf56a7b69b6f7f4cca429b
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:16:39 2024 +0200

    Add second file

commit 77d8790ada4aa9ce8e438a360e44657334eeb7d3
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:14:41 2024 +0200

    Reorganize files

commit 5d565f66349cb8eb1b3550855d89d12496f23a1b
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:13:46 2024 +0200

    Add file

commit f78c0a4d638b3c3f3cfb85a2c5e7eba38023d8b3
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 14:57:53 2024 +0200

    Initial commit

```

Git gives each commit a unique identifier string (e.g., _6fa5fd1b94a163464aaf56a7b69b6f7f4cca429b_). This identifier is called a _hash_ in Git terminology.

When we know the commit identifier, we can return to that state using the `checkout` command. Let's return to the first commit's _First commit_ state:
```bash
$ git checkout f78c0a4
Note: switching to 'f78c0a4'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at f78c0a4 First commit
```

You don't need to provide the full identifier; the first seven characters are enough.

Now the working directory has been updated to the state of the first commit, and the directory contains only the file `text.txt` that was created there first.

```
$ ls -l -a
total 13
drwxr-xr-x 1 h01975 1049089  0 Mar 10 16:17 ./
drwxr-xr-x 1 h01975 1049089  0 Mar 10 13:49 ../
drwxr-xr-x 1 h01975 1049089  0 Mar 10 16:20 .git/
-rw-r--r-- 1 h01975 1049089 17 Mar 10 15:00 test.txt

```

The command notification tells you that we are in _detached HEAD_ state. This means that if we make changes, they won't be recorded in any _branch_, so they won't show up in version history. Practically speaking, it's not a good idea to make commits in this state.

You can return to the current state, for example, as suggested by Git:

```bash
git switch -     # return to the branch from which checkout was performed
```

We'll return to what this is about and how to proceed later in the section _Branches_.

!!! tip "Tip"
    Git always advises you when you perform an operation.
    
    You should read the notifications and try to interpret them. In problem situations, its suggestions often point you in the right direction.


## Oops! Never mind…

It's easy to make mistakes when working with version control operations. But there's no need to worry; everything can be corrected. Here are some basic undo instructions.

### Undoing the `add` command

If you added a file to the next commit that shouldn't be there, you can undo the addition with the `reset` command.

```bash
git reset temp.log
```

If you don't provide a parameter, all added files are removed from the next commit.

The command does not delete or modify files, it only changes the status of files relative to the commit.

### Undoing changes in the working directory before committing

If you want to undo changes you made in the working directory, __which have not yet been committed to version control__, you can restore the file to the latest version in version control using the `restore` command:

```bash
git restore hello.html
```

!!! danger "Warning"
    Note that in this case __your changes are lost and cannot be recovered__. Only committed versions can be restored.

If you want to undo all changes you made in the working directory, you can do it with the `git reset --hard` command. Use it only when you are sure you want to discard all the changes you made.

### Undoing committed changes

If you have committed a change to version control, an identifier has already been created for it and all its information is stored. If you tried to change it, you would end up tampering with the repository's version history.

Actually, undoing a committed change doesn't even make sense. Instead of trying to change history, you can make a new change that corrects the wrong change.

One extra commit doesn't hurt, and the correction is completely safe. Changing history, on the other hand, would be risky and could cause many times more problems than an extra commit.

You can undo an entire commit by making an "anti-commit" using the Git command `revert`. The command makes a change that completely reverses the commit provided as a parameter.

```bash
$ git log -2      # shows the last two commits
commit 4a731586b83b6c1469416a489e5da1a4560707d4 (HEAD -> master)
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 16:58:47 2024 +0200

    Add log file

commit 21f29c9814e6f101319edc51a199b2d62eb97fae
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 15:19:32 2024 +0200

    Reorganize files

$ git revert 4a73158
[master 83e809b] Revert "Add log file"
 1 file changed, 53 deletions(-)
 delete mode 100644 log.txt

$ git log -2
commit 83e809b0dd28076a423d916229567e61f8f44043 (HEAD -> master)
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 16:59:26 2024 +0200

    Revert "Add log file"

    This reverts commit 4a731586b83b6c1469416a489e5da1a4560707d4.

commit 4a731586b83b6c1469416a489e5da1a4560707d4
Author: Ruonavaara Markku <markku.ruonavaara@haaga-helia.fi>
Date:   Sun Mar 10 16:58:47 2024 +0200

    Add log file

```

The `revert` command undoes one commit at a time. If you want to undo multiple commits, each one must be undone one at a time.

Remember that __everything that is stored in version control can be recovered__. That's why you should `commit` your work frequently.

## Exercise 3

Let's practice undoing operations.

<div class="steps" markdown>

1. Make several changes to your repository: modify committed files and add new files. Do not commit!

2. Practice undoing the `add` operation.
     - Add the changes to the next commit (`add`).
     - Remove changes one at a time from the next commit.
     - Remove all remaining changes from the next commit.
     - You should now have several uncommitted changes in your working directory, none of which are going into the next commit.

3. Practice undoing changes made to the working directory. Check the status regularly with the `status` command.
     - Undo changes to a previously committed file from the working directory.
     - Delete all remaining changes from the working directory.
     - What happened to the new files in _untracked_ status?

4. Practice undoing a commit.
     - Make several changes and commit them.
     - Undo the commit using the `revert` command.
     - What does the `log` command show?

5. When you have completed the task, add the identifier `exercise3` to the latest commit by running the command

    ```
    git tag exercise3
    ```
</div>
