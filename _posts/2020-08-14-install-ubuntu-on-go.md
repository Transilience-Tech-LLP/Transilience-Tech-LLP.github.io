---
layout: post
title: Install Go on Ubuntu
date: 2020-08-14
category: ["system-administration"]
author: parinay.bansal
tags: ["install", "ubuntu", "golang"]
summary: A guide on how to install latest version of GoLang on Ubuntu
feature_img: 
excerpt_separator: <!--more-->
medium: 
linkedin:
facebook:
twitter:
comments: true
youtubeId: 
---

# How to install Go on Ubuntu

**Go** is a compiled, statically typed programming language developed by Google. Follow the steps below to install Go on Ubuntu:

## Step 1 - Downloading Go binary files

Use `curl` or `wget` to download the current binary for Go from the official download page.

```
    curl -O https://storage.googleapis.com/golang/go1.13.5.linux-amd64.tar.gz
```

`1.13.5` is the version of Go you’ll want to download. However, this can be replaced with any other version if necessary.

## Step 2 - Extracting from the `tar.gz` file

Next, use **`tar`** to unpack the package. The following command will use the `tar` tool to open and expand the downloaded `tar.gz` file and to create a folder of the package name:

```
    tar -xvf go1.13.5.linux-amd64.tar.gz
```

Then, move the folder to `/usr/local`.

```
    sudo mv go /usr/local
```
The Go package is now in `/usr/local`, which makes sure that Go is in your `$PATH` for Linux.

## Step 3 - Setting paths

Now, we have to set some paths that Go needs. The paths given in this step are all relative to the location of the Go installation in `/usr/local`.

The first step is to set Go’s root value, which tells Go where to look for its files. Run the following command to open the file in your preferred editor:

```
    sudo subl ~/.profile
```

Add the following lines at the end of the file:

```
    export GOPATH=$HOME/work
    export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
```

`$HOME/work` can be replaced with any directory. This directory is where you will be able to use the functionalities of the Go language.

Save and close the file. Then, refresh the file by running:

```
    source ~/.profile
```


## Step 4 - Verifying

It’s always a good idea to see if your installation has been successful or not. This can be done by checking the version number of the Go language installed in your system.

```
    go version
```

The version number of Go installed in your system will be displayed on the terminal.
