# Hosting service functions

Git hosting services offer many functions that facilitate software development and project management.

This section covers some functions that can be utilized, for example, in learning tasks for courses.

The material presents examples of GitHub service functions, but other hosting services (e.g., GitLab, Bitbucket) offer similar functionality.

## Publishing websites

__GitHub Pages__ is a service provided by GitHub for publishing static websites, which allows websites to be published directly from a GitHub repository. It is particularly popular for creating project websites and personal blogs and portfolios.

!!! info "What is a static website?"

    A static website is one that consists of HTML, CSS, and JavaScript files and does not require server-side processing. This means that all content of the website is pre-created and stored, and does not change dynamically based on user actions.

### Website content to be published

The website content is published from the repository. The content can be either an HTML website or Markdown documents.

You can specify which branch the content is published from. The content can be either in the root of the repository or in a subdirectory named `docs`. 

The home page of the published website must be named `index.html`, `index.md`, or `README.md`.

### Publishing

Publishing a GitHub Pages website is done in the GitHub service web interface as follows:

<div class="steps" markdown>

1. Go to the repository settings (_Settings_).
![GitHub repository Settings option](./assets/github_menu_settings.png)

2. Find the _Pages_ section in the menu and select the branch and directory you want from _Source_ from which the content is published.
![GitHub Pages option](./assets/github_settings_menu_pages.png)
![GitHub Pages source selection](./assets/gh-pages_source.png)

3. Save the settings. GitHub automatically creates a website from the repository content.
   
4. The website will be available shortly at `https://<username>.github.io/<repository-name>/`.

</div>

You can edit the repository content, and alway when you make a new commit to the branch, the changes are automatically updated to the website.

### Limitations

GitHub Pages is intended for publishing static websites, so dynamic functions, such as database connections or server-side scripts, are not supported.

GitHub Pages is only available for public repositories, unless you have a paid GitHub account.

GitHub Pages websites cannot be used for commercial business purposes.

Additionally, the websites have technical limitations regarding website size and traffic volume. You can find more information about these in the GitHub Pages service documentation at https://docs.github.com/en/pages.

## Collaboration and project management

This section introduces features that facilitate collaboration and project management in GitHub.

### Inviting users to a repository

Shared repositories allow you to develop projects in collaboration with other developers. The repository owner can invite other users as __collaborators__.

Inviting a collaborator is done in the GitHub service interface as follows:

<div class="steps" markdown>

1. Go to the repository settings (_Settings_).
2. Find the _Collaborators_ section and select _Add people_.

![Adding GitHub collaborators](./assets/github_add_collaborator.png)

3. Search for a GitHub user by their GitHub username or email address.

![Searching for a GitHub user](./assets/github_lookup_people.png)

4. When you click _Add_, the user receives an email invitation to join the repository as a collaborator. 

5. The user must accept the invitation before they get access to the repository.

</div>

With collaborator rights, you can make changes to the repository content (commits, branches, tags, pull requests, etc.), but you cannot manage the repository (e.g., change settings or invite collaborators).

### Task management

__GitHub Issues__ is a tool for managing bug reports or other tasks in a repository. One task (__issue__) typically describes one thing that needs to be clarified or implemented.

<div class="steps" markdown>

1. Open the repository and select _Issues_.
2. Create a new task by clicking _New issue_.
3. Write a clear title and description: what was noticed, how the problem is repeated or what you want to implement.
4. If necessary, add a person responsible (_assignee_) to whom the task is assigned.
5. Click _Create issue_ to create the new task.

</div>

Tasks can be reviewed, discussed, their progress can be tracked, and they can be marked as complete when the matter is resolved (_Close issue_).

### Project management

__GitHub Projects__ is a project management tool that allows tasks and pull requests to be combined into one view and track the progress of work.

The Projects tool is often used as a board with columns such as _To do_, _In progress_, and _Done_. Work items are moved from column to column as work progresses.

Basic usage proceeds like this:

1. Open the repository and select _Projects_.
2. Create a new project (_New project_) and choose an appropriate template (e.g., _Board_).
3. Add tasks to the project.
4. Update the status of items by moving them between columns.
5. Keep track of the big picture from the project view and update tasks regularly.

## Command line interface

In this material, GitHub service functions (e.g., creating repositories or processing pull requests) are done in the web interface.

GitHub also offers a command line interface __GitHub CLI__ (Command Line Interface), through which functions can be used from the command line without a browser.

### Usage

The command line interface software must be installed on your computer. Installation instructions can be found in the GitHub CLI documentation at https://docs.github.com/en/github-cli/github-cli/about-github-cli.

After installation, GitHub CLI commands can be given on the command line. Commands always start with `gh`.

To be able to give commands, you must log in to your GitHub account on the command line:

``` bash 
  gh auth login
```
The command opens the login page in the browser. You only need to log in once.

Some common GitHub CLI commands:

- `gh repo create`: Create a new repository
- `gh pr create`: Create a new pull request
- `gh issue create`: Create a new issue

All commands and their usage instructions can be found in the GitHub CLI documentation at https://cli.github.com/manual.

