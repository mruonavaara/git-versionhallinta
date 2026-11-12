# Workflows in distributed Git environments

Git usage is based on everything happening in a local repository. When a project has multiple developers, the work of different developers is shared with each other through remote repositories.

Remote repositories can be organized in different ways, and various workflows can be implemented for their use. 

A __workflow__ answers the questions:

- How do I organize my work in my own repository so that pushing it to a shared project succeeds
- How do I push my work to a shared project
- How do I get the work of others into my own repository

Below are two examples of different approaches to organizing version control workflows in a project.

### Centralized model

In the centralized model, a project has one shared repository with which all developers synchronize their work.

![](./assets/centralized_workflow.png)

_Source: [Chacon S., Straub B, Pro Git, Chapter 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

Developers fetch changes made by others from the shared repository, combine them with their own changes, and finally push their own changes to the shared repository.

Using this model requires that all developers on the project have permissions to push changes to the shared repository.

### Integration manager model

In public projects (e.g., open source projects), it is not possible to give all project members permissions to modify the contents of the shared repository.

In this case, a model can be applied in Git version control where each developer has their own public repository and read access to each other's repositories.

One repository is the common "official" one, which all have read access to, but only the project maintainer (_integration manager_) has permission to push changes to.

![](./assets/integration_manager_workflow.png)

_Source: [Chacon S., Straub B, Pro Git, Chapter 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

Each developer publishes their changes to their own public repository and sends the maintainer a change request (_pull request_) to merge them into the official repository. The maintainer can thus review the proposed change and, if desired, accept it as is or ask the author to make corrections.

Pull requests can be made within repositories as well, and in real-world project version control practices, changes to shared code are often pushed through pull requests. Pull requests are covered in more detail in section [Pull requests](pull-requests.md).

## Commit practices

Commit messages communicate to project developers what changes others have made to the project. It is important to agree on commit message practices within the project.

There are established good practices for commenting, e.g., [How to Write a Git Commit Message](https://cbea.ms/git-commit/). According to them, comments should include:

- A short (max 50 characters), title-like description on the first line.
- If necessary, a longer description of the change and its reasons, separated by a line break.

Each logical unit should be made into a separate commit. This makes it easier to review and handle changes in the project. Even if you have developed multiple features at once, you can split the changes into different commits during the `add` stage.

Unnecessary white-space (spaces, tabs, line breaks, etc.) does not affect execution but can appear in Git commits as unnecessary changes to others. You can check for such issues with the `diff` command:
```bash
$ git diff --check
```

Editors have features that can automatically remove white-space problems.

## Collaboration in the centralized model

The simplest model used in most small projects is the centralized model. All developers have write access to the shared repository.

Initially, everyone clones the shared repository:

```bash
$ git clone <repository-url>
```

Changes are made in the local repository and committed to it, each developer at their own pace:

```bash
$ git commit
```

When changes are ready, they can be pushed to the shared repository:

```bash
$ git push origin master
```

1. Situation after the `fetch` command:
   
    ![](./assets/after_fetch.png)

2. Situation after the `merge` command:

    ![](./assets/after_merge.png)

3. Situation after the `push` command:
   
    ![](./assets/after_push.png)

_Source: [Chacon S., Straub B, Pro Git, Chapter 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

In the end state, your local repository and the shared repository are on the same level, and the latest commit in the `origin/master` branch contains a version that combines all the changes made by all developers so far.

## Parallel changes

What is described above works relatively smoothly, but only if developers make changes in turn.

Other developers may have published new changes while you are developing yours. In this case, the version paths diverge.

Before your own changes can be pushed to the shared repository, you must fetch any new changes others may have made into your own repository.

The changes made by others must be merged with your own changes, and any conflicts must be resolved. Only then can the finished and tested end result be pushed to the shared repository.

In the following example, the process of merging your own and other developers' changes is shown step by step:

```bash
$ git fetch origin          # 1. fetch changes made by others
$ git merge origin/master   # 2. merge them with your own changes
# ...resolve any conflicts
$ git push origin master    # 3. push the finished result to the shared repository
```

Steps 1 and 2 (`fetch` and `merge`) are often done at once with the `pull` command:

```bash
$ git pull origin master
```
Note that `pull` can cause conflicts, as it also performs a merge. If the situation looks too messy, you can cancel the pending merge with the `git merge --abort` command.

You can check beforehand whether there are new commits in the remote repository by performing a `fetch` operation. In this case, `status` will tell you the situation:

```
$ git status
On branch main
Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
```

## Summary

Each logical unit should be made into a separate commit. This makes it easier to review and handle changes in the project.

Commit messages are important for communication between project developers. Follow good commenting practices.

The following image summarizes a typical workflow in a project that follows the centralized model.

![](./assets/centralized_workflow_example.png)

_Source: [Chacon S., Straub B, Pro Git, Chapter 5.](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) [CC BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)_

- Initially, developers clone the shared repository. This way they get the existing code into their workspace and can continue development.
- Each developer does their own work in their own repository.
- Before publishing the changes they made, each developer must fetch the branch to which the new changes are to be pushed into their own repository.
- Changes obtained from the remote repository must be merged with their own changes. The result is a new commit that contains all current changes.
- The new commit is pushed to the shared repository, from which other developers can then fetch it for themselves.

## Exercise 6

Practice software development and synchronizing changes with a remote repository located on a web service.

!!! note "Exercise preliminaries"

    For this exercise, you will have a virtual team member. Your colleague will continue developing the application created in previous exercises with you.
    
    To complete this exercise, your repository must be prepared. Run the following commands:

    ```
    git remote add actions https://github.com/mruonavaara/git-actions.git
    git fetch actions main
    git merge actions/main --allow-unrelated-histories
    ``` 

    This exercise is based on previous exercises, and completing it requires knowledge from all previous sections!

    You must complete all the steps exactly according to instructions, otherwise your virtual colleague might not be able to follow up on the project progress and do their own development tasks.

You are developing the Hello application as a project team. You have agreed on the following version control practices:

- Each person makes their own changes first in a branch called `develop`.
- Only versions that have been tested and jointly approved as complete are pushed to the main branch.

The next step in the project is to add functionality to the application that shows the user the current time. Your first task is to add a button that allows the user to request the time display.

!!! note "Note"

    Your virtual colleague assumes that the Hello website is in the root directory of the repository and the HTML file is named `index.html`. If you created the website in a subdirectory, move it to the root of the repository for this exercise.

<div class="steps" markdown>

1. Following version control practices, switch to the `develop` branch. It does not exist yet, so you need to create it.

    ``` { .bash .no-copy }
    git switch -c develop
    ```

    It doesn't exist in the remote repository either, so push it there:

    ``` { .bash .no-copy }
    git push -u origin develop # -u is the same as --set-upstream
    ```

2. Add to the `<main>` section in HTML file an element for displaying the date and time, and a button that will launch displaying this information when pressed:

    ```html
    <div id="datetime"></div>
    <button>What time is it?</button>
    ```

    The button doesn't work yet, but don't worry, your colleague will implement the functionality.

    Test the page. When you are satisfied with the result, commit the changes to the `develop` branch.
    
    Push the `develop` branch to the remote repository on GitHub.

3. You notice that your colleague has implemented the button functionality (how?).

    Attach the JavaScript file to your program by adding to the end of the `<body>` section:

    ```html
    <script src="scripts.js"></script>
    ```
    They have also written instructions in the commit message on how to connect the functionality to the button.

    Connect the functionality to the button and test that it works.
    
    When you are satisfied with the page's functionality, commit the change and push it to the shared development branch.

4. You notice that the basic button looks plain. Define better style rules for it in the CSS file, for example:

    ```css
    button {
      background-color: blue;
      color: white;
      margin: 10px;
      padding: 8px;
      border-radius: 8px;
    }
    ```
    Test the page.
    
    When you are satisfied with the result, commit the changes to the `develop` branch and push to the remote repository.

5. In the Scrum meeting this morning, the decision was to change the functionality so that the time is displayed continuously instead. 

    Your colleague has already implemented the JavaScript functionality, and your task is to remove the button that has become unnecessary.

    Fetch your team member's changes and remove all unnecessary code related to the button, test that everything works.
    
    When the change is complete, push it to the shared development branch.

6. In the next Scrum meeting, the team determines that the feature is ready to be presented at the sprint review according to the latest version of the `develop` branch.

    Merge it to the main branch. 
    
    Remember to check that you have all the latest changes before merging and pushing the main branch to the remote repository!

7.  When you have completed the exercise, add a tag `exercise6` to the latest commit by running:

    ```
    git tag exercise6
    ```

</div>

The end result should look something like this:

![](./assets/hei_maailma_lopputulos.png)

### Doesn't the result look the same? 

Did you remember to fetch the latest changes from others before merging? 

If not, fetch them, test on the `develop` branch, and then merge again to the main branch and move the tag accordingly.

??? note "Would you like to try again?"

    If you want to do the exercise again, you can delete both the local repository's and the remote repository's `develop` branch and return to the beginning. Switch to your repository's main branch and run the following commands:

    ```bash
    git branch -D develop # delete the local develop
    git push origin --delete develop # delete the remote origin's develop
    ```
    What happens to the commits made to the branch?
    
    As mentioned earlier, everything that has been committed to version control is preserved there. So are these commits, but the branch reference to them (`develop`) has been deleted. The commits are harder to find and work with, but it is possible to recover them until the Git garbage collection eventually removes them.
    




