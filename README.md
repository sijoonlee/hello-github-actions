## Welcome to "Hello World" with GitHub Actions

This course will walk you through writing your first action and using it with a workflow file. 

**Ready to get started? Navigate to the first issue.**


### Actions and Workflows

There are two components to using GitHub Actions that we'll cover:

- the **action** itself
- a **workflow** that uses action(s)

A workflow can contain many actions. Each action has its own purpose. We'll put the files relating to the action in their own directories.

### Types of Actions

Actions come in two types: **container actions** and **JavaScript actions**.

Docker **container actions** allow the environment to be packaged with the GitHub Actions code and can only execute in the GitHub-Hosted Linux environment.

**JavaScript actions** decouple the GitHub Actions code from the environment allowing faster execution but accepting greater dependency management responsibility.

<!--
UNCOMMENT WHEN THESE TWO COURSE GO LIVE AND ADD PROPER LINK DETAILS
📖 To learn more about creating each type of action, refer to the related learning lab course:
  - [Writing JavaScript Actions]()
  - [Writing Docker Container Actions]() -->

## Step 1: Add a `Dockerfile`

Our action will use a Docker container so it will require a `Dockerfile`. Let's add it now. We won't discuss what each line means in detail, but the important thing to know is that the action will be executed in an environment defined by this file.

### :keyboard: Activity: Create a `Dockerfile` and open a pull request

1. Create a file titled `action-a/Dockerfile` by [using this quick link](https://github.com/sijoonlee/hello-github-actions/new/master?filename=action-a/Dockerfile) or manually:
   - Create a new branch. _Branches should be named intentionally, so a good name for this branch could be `first-action`_.
   - On the new branch, create a directory: `action-a`. _Note:_ If you're working on GitHub.com, you can create a directory and a file at the same time by naming the file `action-a/Dockerfile`.
   - In the `action-a` directory, create a file titled `Dockerfile`.
1. Fill the `Dockerfile` with the content below:

   ```Dockerfile
   FROM debian:9.5-slim

   ADD entrypoint.sh /entrypoint.sh
   RUN chmod +x /entrypoint.sh
   ENTRYPOINT ["/entrypoint.sh"]
   ```

1. Commit your file
   - If you're working locally, you will also need stage your file and to push the branch to GitHub.
1. Open a pull request with your new branch against `master`

<hr>
<h3 align="center">I'll respond in your new pull request with next steps.</h3>


Nice work, you committed a `Dockerfile`. You'll notice at the end of the Dockerfile, we refer to an entrypoint script.

```Dockerfile
ENTRYPOINT ["/entrypoint.sh"]
```

The `entrypoint.sh` script will be run in Docker, and it will define what the action is really going to be doing.

## Step 2: Add an entrypoint script

An entrypoint script must exist in our repository so that Docker has something to execute.

### :keyboard: Activity: Add an entrypoint script and commit it to your branch

1. As a part of this branch and pull request, create a file in the `/action-a/` directory titled `entrypoint.sh`. You can do so with [this quicklink](https://github.com/sijoonlee/hello-github-actions/new/first-action?filename=action-a/entrypoint.sh)
1. Add the following content to the `entrypoint.sh` file:

   ```shell
   #!/bin/sh -l

   sh -c "echo Hello world my name is $INPUT_MY_NAME"
   ```

1. Stage and commit the changes
1. Push the changes to GitHub

<hr>
<h3 align="center">I'll respond when I detect a new commit on this branch.</h3>


Nice work adding the `entrypoint.sh` script.

In `entrypoint.sh`, all we're doing is outputting a "Hello world" message using an environment variable called `MY_NAME`.

Next, we'll define a **workflow** that uses the GitHub Action.
Next, we'll define the `action.yml` file which contains the metadata for our action.

### action.yml

All actions require a metadata file that uses YAML syntax. The data in the metadata file defines the `inputs`, `outputs` and main `entrypoint` for your action.

## Step 3: Add an action metadata file

We will use an `input` parameter to read in the value of `MY_NAME`.

### :keyboard: Activity: Create action.yml

1. As a part of this branch and pull request, create a file titled `action-a/action.yml`. You can do so using [this quicklink](https://github.com/sijoonlee/hello-github-actions/new/first-action?filename=action-a/action.yml) or manually.
1. Add the following content to the `action.yml` file:

   ```yaml
   name: "Hello Actions"
   description: "Greet someone"
   author: "octocat@github.com"

   inputs:
     MY_NAME:
       description: "Who to greet"
       required: true
       default: "World"

   runs:
     using: "docker"
     image: "Dockerfile"

   branding:
     icon: "mic"
     color: "purple"
   ```

1. Stage and commit the changes
1. Push the changes to GitHub

<hr>
<h3 align="center">I'll respond when I detect a new commit on this branch.</h3>

Next, we'll define a **workflow** that uses the GitHub Action.

### Workflow Files

Workflows are defined in special files in the `.github/workflows` directory, named `main.yml`.

Workflows can execute based on your chosen event. For this lab, we'll be using the [`push`](https://developer.github.com/v3/activity/events/types/#pushevent) event.

We'll break down each line of the workflow in the next step.

## Step 3: Start your workflow file

First, we'll add the structure of the workflow.

### :keyboard: Activity: Name and trigger your workflow

1. Create a file titled `.github/workflows/main.yml`. You can do so [using this quicklink](https://github.com/sijoonlee/hello-github-actions/new/first-action?filename=.github/workflows/main.yml) or manually:
   - As a part of this branch and pull request, create a `workflows` directory nested inside the `.github` directory.
   - In the new `.github/workflows/` directory, create a file titled `main.yml`
1. Add the following content to the `main.yml` file:
   ```yaml
   name: A workflow for my Hello World file
   on: push
   ```
1. Stage and commit the changes
1. Push the changes to GitHub

<details><summary>Trouble pushing? Click here.</summary>

The `main.yml` file cannot be edited using an integration. Try editing the file using the web interface, or your command line.

It is possible that you are using an integration (like GitHub Desktop or any other tool that authenticates as you and pushes on your behalf) if you receive a message like the one below:

```shell
To https://github.com/your-username/your-repo.git
 ! [remote rejected] your-branch -> your-branch (refusing to allow an integration to update main.yml)
error: failed to push some refs to 'https://github.com/your-username/your-repo.git'
```

</details>
<br />

<hr>
<h3 align="center">I'll respond when I detect a new commit on this branch.</h3>

Next, we'll define a **workflow** that uses the GitHub Action.

### Workflow Files

Workflows are defined in special files in the `.github/workflows` directory, named `main.yml`.

Workflows can execute based on your chosen event. For this lab, we'll be using the [`push`](https://developer.github.com/v3/activity/events/types/#pushevent) event.

We'll break down each line of the workflow in the next step.

## Step 3: Start your workflow file

First, we'll add the structure of the workflow.

### :keyboard: Activity: Name and trigger your workflow

1. Create a file titled `.github/workflows/main.yml`. You can do so [using this quicklink](https://github.com/sijoonlee/hello-github-actions/new/first-action?filename=.github/workflows/main.yml) or manually:
   - As a part of this branch and pull request, create a `workflows` directory nested inside the `.github` directory.
   - In the new `.github/workflows/` directory, create a file titled `main.yml`
1. Add the following content to the `main.yml` file:
   ```yaml
   name: A workflow for my Hello World file
   on: push
   ```
1. Stage and commit the changes
1. Push the changes to GitHub

<details><summary>Trouble pushing? Click here.</summary>

The `main.yml` file cannot be edited using an integration. Try editing the file using the web interface, or your command line.

It is possible that you are using an integration (like GitHub Desktop or any other tool that authenticates as you and pushes on your behalf) if you receive a message like the one below:

```shell
To https://github.com/your-username/your-repo.git
 ! [remote rejected] your-branch -> your-branch (refusing to allow an integration to update main.yml)
error: failed to push some refs to 'https://github.com/your-username/your-repo.git'
```

</details>
<br />

<hr>
<h3 align="center">I'll respond when I detect a new commit on this branch.</h3>
