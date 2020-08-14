---
layout: post
title: Introducing Github Actions
date: 2020-08-14
category: SDLC
author: parinay.bansal
tags: ["github", "actions", "data-science"]
summary: Github actions can be overwhelming, yet powerful. Moving to the new era we need to automate a lot of things and github has been beautifully catching up. In this post we introduce some concepts how github can be used by data scientists for automating certain tasks.
feature_img: https://upload.wikimedia.org/wikipedia/commons/thumb/e/ef/Octicons-logo-github.svg/1200px-Octicons-logo-github.svg.png
excerpt_separator: <!--more-->
medium: 
linkedin:
facebook:
twitter:
comments: true
youtubeId: 
---

# Introduction to GitHub Actions

## For data scientists

![Image for post](https://miro.medium.com/max/3838/1*e2eE4tHIgABdCpFrSY42OA.png)

GitHub Actions can be a little confusing if you’re new to DevOps and the CI/CD world, so in this article, we’re going to explore some features and see what we can do using the tool.

From the point of view of CI/CD, the main goal of GitHub Actions and Workflows is to **test our software every time something changes**. This way we can spot bugs and correct things as soon as the errors come up.

Today we’ll learn more about GitHub Actions and learn how to use them using Bash scripting and Python. Nice, let’s get started!

# GitHub Actions vs. Workflows

First, it’s good to state the difference between GitHub Actions and Workflows. As the GitHub Actions [Documentation](https://docs.github.com/en/actions) states, actions are “**individual tasks** that you can combine to create jobs and customize your workflow”. On the other hand, [Workflows](https://docs.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow#about-workflows) are “**custom automated processes** that you can set up in your repository to build, test, package, release, or deploy any project on GitHub”. In other words:

*   **Workflows**: automated processes that run on your repository; workflows can have many GitHub Actions
*   **GitHub Actions**: individual tasks; they can be written using Docker, JavaScript and now also shell scrips with the new [Composite Run Steps](https://github.blog/changelog/2020-08-07-github-actions-composite-run-steps/); you can write your own actions or use an action someone else created

# Writing our first Workflow

Let’s first create a workflow with no action just to understand how it works. Workflows are defined using YAML files and you must store them in the `.github/workflows` directory in the root of your repository.

To create a workflow we need to define these things:

*   **_The event_** _that triggers the workflow_
*   **_The machine_** _each job should run_
*   **_The jobs_ **_that make the workflow (jobs contain a set of steps that perform individual tasks and run in parallel by default)_
*   **_The steps_** _each job should run_

The **basic syntax** for a workflow is:

*   `on` — the event that triggers the workflow
*   `runs-on` — the **machine** each job should run
*   `jobs` — the jobs that make the **workflow**
*   `steps` —the **tasks** each job should run
*   `run` —the **command** the step should run

First, we need to define the event that **triggers** the workflow. In this example, we want to say greetings every time someone pushes to the repository.

A workflow **run** is made up of one or more **jobs**. Each job runs in a machine specified by `runs-on`. The machine can be either a GitHub-hosted runner, or a self-hosted runner. We’re going to use the `ubuntu-latest` GitHub-hosted runner.

A job contains a sequence of tasks called **steps**. Steps can run commands, run setup tasks, or run an action. Each step has can have a **run** command that uses the operating system’s shell. Here we’re going to echo a message.

Confusing? Let’s see how it works. Go ahead and create a `first_workflow.yml` file inside `.github/workflows` on your repo, then paste this code:

```
# your-repo-name/.github/workflows/first_workflow.yml

name: First Workflow

on: push

jobs:
  first-job:                             
    name: Say hi                             
    runs-on: ubuntu-latest                             
     steps:
    - name: Print a greeting                               
      run: echo Hi from our first workflow!

```

Now if you commit this file to your repository, push it and go to the Actions tab on the GitHub website you can see the new workflow, check all the runs and view the outputs:

![Image for post](https://miro.medium.com/max/3838/1*e2eE4tHIgABdCpFrSY42OA.png)

<p align="center">
The outputs of our fist workflow
</p>

## Using an Action in our first workflow

Actions are **individual tasks** and we can use them from three sources:

*   Actions defined in the **same repository** as the workflow
*   Actions defined in a **public repository**
*   Actions defined in a **published Docker container image**

They run as a **step** in our workflow. To call them we use the `uses` syntax. In this example, we’re going to use an Action that [prints ASCII art text,](https://github.com/mscoutermarsh/ascii-art-action) written by [Mike Coutermarsh](https://github.com/mscoutermarsh). Since it’s defined in a public repository we just need to pass it’s name:

```
# your-repo-name/.github/workflows/first_workflow.yml
name: First Workflow
on: push
jobs:                           
  first-job:                             
    name: Say hi                             
    runs-on: ubuntu-latest                             
    steps:                             
      - name: Print a greeting                               
        run: echo Hi from our first workflow!     

      - name: Show ASCII greeting                               
        uses: mscoutermarsh/ascii-art-action@master
        with:                                 
          text: 'HELLO!'
```

The `with` syntax is a map of input parameters defined by the action. Here is the result:


![Image for post](https://miro.medium.com/max/3806/1*2j4gjJMnEXEOgWZ1o0x95Q.png)
<p align="center">
The result of the ASCII art Action
</p>

# Using Python with Workflows

As Data Scientists we use a lot of Python in our day to day, so it’s a good idea to learn how to use it in our workflows. **Setting a specific version of Python or PyPy** is the recommended way of using Python with GitHub Actions because it “ensures consistent behavior across different runners and different versions of Python”. To do that we’ll use an action: `setup-python`.

After that, we can run the commands as we usually do in a machine. Here we’ll install Scrapy and run a script to get some TDS posts about GitHub Actions, just to see how it works. Since we want to run a script from **our own repository** we also need to use the `checkout` action to access it. Let’s create a new job to run the script:

```
# your-repo-name/.github/workflows/first_workflow.yml
name: First Workflow
on: push
jobs:                           
  first-job:                             
    name: Say hi                             
    runs-on: ubuntu-latest
    steps:                             
      - name: Print a greeting                               
        run: echo Hi from our first workflow!    

      - name: Show ASCII greeting                               
        uses: mscoutermarsh/ascii-art-action@master      
        with:                                 
          text: 'HELLO!'  
  get-posts-job:
    name: Get TDS posts
    runs-on: ubuntu-latest 
    steps:                               
      - name: Check-out the repo under $GITHUB_WORKSPACE                                 
        uses: actions/checkout@v2

      - name: Set up Python 3.8                                 
        uses: actions/setup-python@v2
        with:                                   
          python-version: '3.8'            

      - name: Install Scrapy                                 
        run: pip install scrapy

      - name: Get TDS posts about GitHub Actions                                   
        run: scrapy runspider posts_spider.py -o posts.json
```

I want to save the scraped posts to a file, so let’s learn how to do it.

## Persisting workflow data

An **artifact** is a file or collection of files produced during a workflow run. We can pass an artifact to another job in the same workflow or download it using the GitHub UI.

Let’s download the JSON file with the posts to see how it works. To work with artifacts we use the `upload-artifact` and `download-artifact` actions. To upload an artifact we need to specify the path to the file or directory and the name of the artifact:

```
# your-repo-name/.github/workflows/first_workflow.yml
get-posts-job:                              
    name: Get TDS posts                              
    runs-on: ubuntu-latest
    steps:                               
      - name: Check-out the repo under $GITHUB_WORKSPACE                                 
        uses: actions/checkout@v2          

      - name: Set up Python 3.8                                 
        uses: actions/setup-python@v2                                
        with:                                   
          python-version: '3.8'            

      - name: Install Scrapy                                 
        run: pip install scrapy           

      - name: Get TDS posts about GitHub Actions                                   
        run: scrapy runspider posts_spider.py -o posts.json</span> <span id="1111" class="ct nk lv bj ng b cb no np nq nr ns nm r nn">** - name: Upload artifact                        
        uses: actions/upload-artifact@v2                          
        with:                                   
          name: posts                                   
          path: posts.json**</span></pre>
```

And now we can download the file using the GitHub UI:

![Image for post](https://miro.medium.com/max/3800/1*NAtP4ADh8SMhh_Zr4d19Lg.png)

<p align="center">
Downloading the artifact
</p>

# Creating your first Action

Actions can be created using Docker containers, JavaScript or you can create an action using shell scripts (a composite run steps action). The main use case for the [composite run steps action](https://github.blog/changelog/2020-08-07-github-actions-composite-run-steps/) is when you have a lot of shell scripts to automate tasks and writing a shell script to combine them is easier than JavaScript or Docker.

The three main components of an action are `runs` , `inputs` and `outputs`.

*   `runs` —**_(required)_** Configures the path to the action’s code and the application used to execute the code.
*   `inputs` —**_(optional)_** Input parameters allow you to specify data that the action expects to use during runtime
*   `outputs` —**_(optional)_** Output parameters allow you to declare data that an action sets

The filename for an action must be either `action.yml` or `action.yaml`. Let’s use the example from GitHub Docs and create an action that prints a “Hey [user]” message. Since it’s a composite action we’ll use the `using: "composite"` syntax:

```
# action.yml
name: 'Hey From a GitHub Action'
description: 'Greet someone'
inputs:  
  user: # id of input  
    description: 'Who to greet'  
    required: true  
    default: 'You'

runs:  
  using: "composite"
  steps:   
    - run: echo Hey ${{ inputs.user }}.  
      shell: bash
```

If an action is defined in the same repository as the workflow we can refer to it using `./path-to-action-file`. In this case, we need to access the file inside the repository, so we also need to use the `checkout` action.

If the action is defined in a public repository we can refer to it using a specific commit, a version of a release or a branch.

## Running an action from the same repository

```
# .github/workflows/use-action-same-repo.yml
name: Action from the same repo

on: push   

jobs:                                   
  use-your-own-action:                             
    name: Say Hi using your own action                             
    runs-on: ubuntu-latest                             
    steps:                               
      - uses: actions/checkout@v2

      - uses: ./ # the action.yml file is in the root folder                             
        with:                                  
         user: 'username'
```

## Running an action from a public repository

```
# .github/workflows/use-action-public-repo.yml

name: Action from a public repository

on: push   

jobs:                                   
  use-your-own-action:                             
    name: Say Hi using your own action                             
    runs-on: ubuntu-latest                             
    steps:                                                 
      - uses: dmesquita/github-actions-tutorial@master
        with:                                  
         user: 'username'
```

And that’s if for our tour. You can also use [variables and secrets](https://docs.github.com/en/actions/configuring-and-managing-workflows/using-variables-and-secrets-in-a-workflow) in your workflow, [cache dependencies](https://docs.github.com/en/actions/configuring-and-managing-workflows/caching-dependencies-to-speed-up-workflows) to speed up them and [connect databases and service containers](https://docs.github.com/en/actions/configuring-and-managing-workflows/using-databases-and-service-containers) to manage workflow tools.

In this guide, we didn’t use one of the main cool things of CI which is to **test often** so we can spot bugs early on in the process. But I think it’s good to understand how the actions and workflow work before doing that. I hope now it’ll be easier to start using CI tools, I plan to do that on the next tutorials.

You can see all the code we used here: [https://github.com/dmesquita/github-actions-tutorial](https://github.com/dmesquita/github-actions-tutorial)

That’s it for today, thanks for reading!

__The original article can be found [here](https://towardsdatascience.com/introduction-to-github-actions-7fcb30d0f959)__