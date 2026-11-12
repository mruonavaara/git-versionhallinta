# Remote repositories

## Distributed repositories

As mentioned earlier, git stores all information locally in its own data storage, called a repository. The local data repository contains all the necessary information.

Connections can be defined between independent repositories, allowing their contents to be synchronized with each other. Synchronization can be done in one direction or both ways.

Other repositories to which a local repository has a connection are called __remote repositories__ (_remote_).

<!-- Image to be added here -->

## Cloning

When working on a project, there is usually an agreed-upon main repository that maintains shared code.
In this case, a local copy of the repository can be easily obtained with the `clone` operation:

```bash
git clone https://github.com/libgit2/libgit2
```
Cloning creates a ready-made local repository that is a complete copy of the original. Cloning

- adds the latest files from the default branch (e.g. `master`) to the directory, and
- configures the original repository as a remote repository of the new repository with the default name `origin`.

From here you can continue development in your own workspace.

## Defining remote repositories

Remote repository connections can be defined even without cloning. This is necessary, for example, when you want to make a project's shared repository from an existing local repository.

You can define remote repositories with the `remote add` command:

```bash
git remote add origin https://github.com/user/repository.git
```

- `origin` is the name given to the remote repository
- `https://github.com/user/repository.git` is its address.

Since `origin` is the default name for a remote repository, it is used most often. However, it is just a name, not a reserved word.

You can list remote repositories with the `remote` command:

```bash
git remote
```
You can get more information with the `-v` (`--verbose`) option.
```bash
git remote -v
```
Remote repositories can be renamed with the `rename` command and deleted with the `rm` command.
```bash
git remote rename origin temp
git remote rm temp
```

Information about a specific remote repository can be viewed with the `show` command.
```bash
git remote show origin
```

## Fetching data from remote repositories

Repository data synchronization occurs in two steps:

1. Data in the remote repository branch is fetched to the local repository alongside local branches (_fetch_).
2. The remote repository branch is merged with its corresponding local branch (_merge_).

### Fetch

The `fetch` command downloads data from the remote repository to the local repository.

```bash
git fetch origin
```
However, it does not make changes to the local repository branches but stores them separately. Fetch is therefore a completely safe command; nothing in your repository will change unless you explicitly give commands to make changes.

Remote repository branches are found under the remote repository name, for example `origin/master`. You can list remote repository branches with the `-r` option.

```bash
git branch -r
```

You can examine the content downloaded from the remote repository with the regular `switch` command (and `git log` etc.) and, if you wish, merge it into local content with the regular `merge` command.

```bash
git switch master
git merge origin/master
```

### Pull

The `fetch` command downloads all changes from the remote repository that you don't have yet. To get them into your repository branch, they must be merged.

Because this two-step operation is so common, there is a separate `pull` command that fetches new data for the current branch from the remote repository and automatically merges them into your current branch.

```bash
git pull origin 
```

This operation is the same as:

```bash
git fetch
git merge
```

Since `pull` also performs merging, the command execution can result in conflicts. Sometimes it may be clearer to perform the operations separately.

## Pushing data to remote repositories

The `push` command synchronizes data from the local repository to the remote repository.

```bash
git push origin master    # push local branch master to repository origin
```

- `origin` is the name of the remote repository where data is being pushed
- `master` is the name of the branch being pushed

Local branches are not automatically pushed to the remote repository but must be explicitly pushed there. If there is no need to share a branch via a remote repository, you can keep it completely local. For example, temporary branches often don't need to be synchronized.

All local branches are pushed if you use the `--all` option.

```bash
git push --all            # push all local branches to the origin repository
```

When pushing for the first time, it's a good idea to use the `--u` (`--set-upstream`) option in the `push` command. It sets the remote repository branch as the default remote branch for the local branch being pushed.

```bash
git push -u origin master
```

Then you won't need to specify the remote repository in the command later; just use:

```bash
git push                  # push current branch to its default remote branch
```

## Remote repositories and branches

Synchronizing remote repositories is actually about synchronizing branches.

When you create branches locally and have a remote repository, you need to decide whether you want to synchronize it or not. If you do, you must explicitly push it there (unless you use the `--all` option). At the same time, it's a good idea to set a default for the remote branch so that synchronization will be easier in the future.
```bash
git push -u origin feat123
```

The `fetch` command brings branch information to the local repository but does not merge it.

```bash
git fetch origin
```

As a result, information about changes in the remote repository is added to the local repository. They are stored in local branches with the name format `<remote>/<branch>`.

The local `origin/master` is therefore a copy of the `master` branch from the `origin` remote repository. When you merge fetched branches, it is done with the local copy.

```bash
git merge origin/master
```

The `git pull` command performs both operations at once. It first fetches the remote repository branch (_fetch_) and merges it into the local branch (_merge_).
```bash
git pull origin
```

### Deleting branches

If you want to delete a branch that has been synchronized to a remote repository, you must delete it from both the local repository and the remote repository.

A branch can be deleted from the local repository with the `branch --delete <branch>` command:
```bash
git branch --delete feat123        # or -d
```

However, the branch still remains in the remote repository. You can delete it from there with the `push --delete <remote> <branch>` command:

```bash
git push --delete origin feat123   # or -d
```


## Multiple remote repositories

Most often, content is synchronized with only one remote repository, but there can be more. In this case, all remote repositories being synchronized must share the same base; they must have a common starting point to which version histories can be merged.

In the following example, two remote repositories, `origin` and `upstream`, are defined for a local repository. The situation could be as follows:

- The `upstream` repository located in a cloud service contains course assignments that students can clone into their own repository.
- The student completes the assignments and saves the answers in their own repository.
- The student creates their own repository in the cloud service for submissions and shares the submissions with the instructor through it.

In this case, the student does not have write access to the `upstream` repository. However, they can merge possible assignment updates from there into their own repository, because all repositories have a common origin, the `upstream` repository.

![](./assets/repo_push_pull.png)
