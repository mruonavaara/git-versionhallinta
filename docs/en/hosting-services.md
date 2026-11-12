# Git hosting services

Git hosting refers to providing repository space and Git services for use over the network.

Git hosting can be done on a company's own servers (_self hosting_) or on an internet service provider's servers (_cloud hosting_).

The most commonly used services are:

- GitHub ([https://github.com/](https://github.com/))
- Bitbucket ([https://bitbucket.org/](https://bitbucket.org/))
- GitLab ([https://gitlab.com/](https://gitlab.com/))

In addition to Git functionality and storage space, services provide functionalities like:

- Project member management (_collaborators_)
- Issue and bug tracking
- Project management functionality (_agile boards_)

Free accounts allow implementing small projects. Paid subscriptions provide services needed for implementing larger projects.

## Using services

Like with other online services, users need to open an account on the service.
Multiple repositories (projects) can be created for the account.

A repository on the service acts as a remote repository for the developer. Through the remote repository on the service, a developer can share their work with others, and conversely receive changes made by other developers into their own local repository.

To make authentication easier, you can store an SSH encryption key on the service, allowing communication with repositories to occur via SSH protocol without separate authentication.

Repositories can be created in the service's web interface. Some services also support creating a repository directly with a push operation.

Members (_collaborators_) can be added to repositories, and they can be assigned different roles with different permissions, for example: _guest_, _reporter_, _developer_, _maintainer_.

There are many different features and settings available, for example notifications and workflow automation functions.

Familiarize yourself with your service provider's documentation. All major services have excellent documentation.

## README and Markdown

Services display a file named README on the repository's home page. Usually it becomes the project's home page. README is written in Markdown.

Markdown is a simple markup language, see for example [https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet).

Code editors have Markdown support extensions available, for example Visual Studio Code editor already has a built-in preview and several editing helper functions for writing Markdown documents ([https://code.visualstudio.com/docs/languages/markdown](https://code.visualstudio.com/docs/languages/markdown)).

Markdown is often used for project documentation because it allows the same version control for documentation as for code.

![](./assets/vscode_md_preview.en.png)

## Exercise 5

Push the project to the GitHub service.

<div class="steps" markdown>

1. Add an empty repository to GitHub.
    - Don't let GitHub create anything there, not even create a README file!

    What is displayed on the GitHub repository page?

2. Configure the new repository as a remote repository for your local repository with the name `origin`.
     - You can verify the remote repository settings with the command `git remote -v`.

3. Push the `master` branch of your local repository to GitHub. What is now displayed on the GitHub repository page? 
    
    Which branches do you see on GitHub? Which branches do you see in your local repository?

4. Create a feature branch `new-feat` in your local repository, switch to that branch, create a new file in it and save the change.

5. The new branch is now only in your local repository. You can see local branches with the command `git branch`. 
   
   Push the new branch to the remote repository and verify from GitHub's web interface that the new branch is now there too.

6.  You can also make changes to the repository in the web interface. Create a new file in the feature branch using GitHub's interface and save the change.

7.  The remote repository now has different content than your local repository. Run the command `git status`. Then do `git fetch` and run the command `git status` again. 
   
    What changed?
 
8.  Fetch retrieves changes but does not merge them. You can go to your local repository to view the changes fetched from the remote repository:

    ```bash
    git switch origin/new-feat 
    ```
9.  Return to the local `new-feat` branch and merge the changes from the `origin/new-feat` branch into your local `new-feat` branch. 
    
    What does the `status` command say now?

10.  Finally, merge `new-feat` into the `master` branch and push the changes to the remote repository.

11.  When you have completed the exercise, add a tag `harjoitus5` to the latest commit by running the command

    ```
    git tag exercise5
    ```
</div>

Tips:

- [GitHub's guide for creating a repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-new-repository#creating-a-new-repository-from-the-web-ui)
- [GitHub's guide for adding a file in GitHub's interface](https://docs.github.com/en/repositories/working-with-files/managing-files/creating-new-files)
