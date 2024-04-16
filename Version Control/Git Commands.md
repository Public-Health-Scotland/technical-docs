# Git Commands Reference Guide

When working with Git, it's inevitable you'll have to work with the command line. This guide will help you with the most common commands you'll need to know. For more information on a specific command, you can use the `git help` command followed by the command you want to learn more about. For example, `git help commit`. There is also the [Git Guide](https://public-health-scotland.github.io/git-guide), which is a more in-depth guide to using Git in PHS, including a more complete list of commands.

Some commands don't require additional arguments and can be used standalone to action something or get information. Where a command requires additional arguments, they will be listed in the table below using square brackets. For example, `[Message]` would be replaced with the message you want to use (the square brackets should not be included in the command).

## Table of Contents

- [Setup and Config](#setup-and-config)
- [Creating Repositories](#creating-repositories)
- [Staging and Committing](#staging-and-committing)
- [Branching](#branching)
- [Remote Repositories](#remote-repositories)
- [History and Changes](#history-and-changes)

## Setup and Config

| Command                                         | Description                                                                                     |
| ----------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| `git config --global user.name "[Your Name]"`   | Set your name for Git to use, for simplicity this should match your GitHub username.            |
| `git config --global user.email "[Your Email]"` | Set your email address for Git to use, for simplicity this should match your PHS email address. |
