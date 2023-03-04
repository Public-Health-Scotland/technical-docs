# Contributing to the PHS Data Science Knowledge Base

Firstly, thanks for taking the time to check out this guide and thinking about contributing! :tada::+1: 

The following is a set of guidelines for contributing, hosted on GitHub. These guidelines mainly focus on the development of the application, rather than content. If you're interested in contributing to content, go to the [resources](#resources) section.

#### Table Of Contents

[Code of Conduct](#code-of-conduct)

[I just have a question!](#i-just-have-a-question)

[How Can I Contribute?](#how-can-i-contribute)

* [Reporting Bugs](#reporting-bugs)
* [Suggesting Enhancements](#suggesting-enhancements)
* [Pull Requests](#pull-requests)
* [Resources](#resources)

* [Styleguides](#styleguides)
* [Git Commit Messages](#git-commit-messages)
* [JavaScript Styleguide](#javascript-styleguide)

## Code of Conduct

This project and everyone participating in it is governed by the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to [phs.datascience@phs.scot](mailto:phs.datascience@phs.scot).

## I just have a question!

> **Note:** Please don't file an issue to ask a question. You'll get faster results by using the resources below.

Whether your question is about the resources available on the base or something about the base iteself, the Data Science team will be able to help. Either post a message on the [Data Science channel](https://teams.microsoft.com/l/channel/19%3a371c5503869d4dc8a6ac090c0844ce55%40thread.tacv2/Data%2520Science?groupId=1d322b44-bb66-4789-bb8e-1c5cffc733b7&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a) in the PHS People Development Hub or email them [here](mailto:phs.datascience@phs.scot).

## How Can I Contribute?

### Reporting Bugs

This section guides you through submitting a bug report. Following these guidelines helps maintainers and the community understand your report :pencil:, reproduce the behavior :computer:, and find related reports :mag_right:.

Before creating bug reports, please check [this list](#before-submitting-a-bug-report) as you might find out that you don't need to create one. When you are creating a bug report, please [include as many details as possible](#how-do-i-submit-a-good-bug-report). Fill out [the required template](https://github.com/Public-Health-Scotland/knowledge-base/blob/master/.github/ISSUE_TEMPLATE/bug_report.md), the information it asks for helps us resolve issues faster.

> **Note:** If you find a **Closed** issue that seems like it is the same thing that you're experiencing, open a new issue and include a link to the original issue in the body of your new one.

#### Before Submitting A Bug Report

* **Perform a [cursory search](https://github.com/Public-Health-Scotland/knowledge-base/issues)** to see if the problem has already been reported. If it has **and the issue is still open**, add a comment to the existing issue instead of opening a new one.

#### How Do I Submit A (Good) Bug Report?

Bugs are tracked as [GitHub issues](https://guides.github.com/features/issues/). After you've determined a bug exists, create an issue and provide the following information by filling in [the template](https://github.com/Public-Health-Scotland/knowledge-base/blob/master/.github/ISSUE_TEMPLATE/bug_report.md).

Explain the problem and include additional details to help maintainers reproduce the problem:

* **Use a clear and descriptive title** for the issue to identify the problem.
* **Describe the exact steps which reproduce the problem** in as many details as possible. For example, start by explaining what link you used, on what browser (e.g. Chrome, Internet Explorer, Firefox, etc.), which page you were on, etc.
* **Provide specific examples to demonstrate the steps**. Include links.
* **Describe the behavior you observed after following the steps** and point out what exactly is the problem with that behavior.
* **Explain which behavior you expected to see instead and why.**
* **Include screenshots** which show you following the described steps and clearly demonstrate the problem.
* **If the problem wasn't triggered by a specific action**, describe what you were doing before the problem happened and share more information using the guidelines below.

Provide more context by answering these questions:

* **Did the problem start happening recently** or was this always a problem?
* **Can you reliably reproduce the issue?** If not, provide details about how often the problem happens and under which conditions it normally happens.

Include details about your configuration and environment:

* **What's the name and version of the OS you're using**?
* **What's the name and version of the browser you're using**?
* **Which keyboard layout are you using?** Are you using a US layout or some other layout?

### Suggesting Enhancements

This section guides you through submitting an enhancement suggestion, including completely new features and minor improvements to existing functionality. Following these guidelines helps maintainers and the community understand your suggestion :pencil: and find related suggestions :mag_right:.

Before creating enhancement suggestions, please check [this list](#before-submitting-an-enhancement-suggestion) as you might find out that you don't need to create one. When you are creating an enhancement suggestion, please [include as many details as possible](#how-do-i-submit-a-good-enhancement-suggestion). Fill in [the template](https://github.com/Public-Health-Scotland/knowledge-base/blob/master/.github/ISSUE_TEMPLATE/feature_request.md), including the steps that you imagine you would take if the feature you're requesting existed.

#### Before Submitting An Enhancement Suggestion

* **Perform a [cursory search](https://github.com/Public-Health-Scotland/knowledge-base/issues)** to see if the enhancement has already been suggested. If it has, add a comment to the existing issue instead of opening a new one.

#### How Do I Submit A (Good) Enhancement Suggestion?

Enhancement suggestions are tracked as [GitHub issues](https://guides.github.com/features/issues/). When you have an enhancement suggestion, create an issue and provide the following information in [the template](https://github.com/Public-Health-Scotland/knowledge-base/blob/master/.github/ISSUE_TEMPLATE/feature_request.md).

* **Use a clear and descriptive title** for the issue to identify the suggestion.
* **Provide a step-by-step description of the suggested enhancement** in as many details as possible.
* **Describe the current behavior** and **explain which behavior you expected to see instead** and why.
* **Include screenshots and animated GIFs** which help you demonstrate the steps or point out the part of the app the suggestion is related to.
* **Explain why this enhancement would be useful** to most users.
* **Does this enhancement exist on other applications?**
* **Specify the name and version of the browser you're using.**

### Pull Requests

The process described here has several goals:

* Maintain quality
* Fix problems that are important to users
* Engage the community in working toward the best possible application
* Enable a sustainable system for maintainers to review contributions

Please follow these steps to have your contribution considered by the maintainers:

1. Follow all instructions in the template, this will auto-populate when you open a Pull Request. The template can be seen [here](https://github.com/Public-Health-Scotland/knowledge-base/blob/main/.github/pull_request_template.md).
2. Follow the [styleguides](#styleguides)

While the prerequisites above must be satisfied prior to having your pull request reviewed, the reviewer(s) may ask you to complete additional design work, tests, or other changes before your pull request can be ultimately accepted.

### Resources

If you have a suggestions for content on the social page, have developed internal materials for Data Science, or are looking to help develop a new course, we want to hear from you. The process to do this just now is to email the [PHS Data Science team](phs.datascience@phs.scot). 

## Styleguides

### Git Commit Messages

See the [PHS GitHub Guidance](https://github.com/Public-Health-Scotland/GitHub-guidance) for the full guidance document, some main points are highlighted here:

* Use the present tense ("Add feature" not "Added feature")
* Use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* Limit the first line to 72 characters or less
* Reference issues and pull requests liberally after the first line
* Consider starting the commit message with an applicable emoji?:
    * :art: `:art:` when improving the format/structure of the code
    * :racehorse: `:racehorse:` when improving performance
    * :non-potable_water: `:non-potable_water:` when plugging memory leaks
    * :memo: `:memo:` when writing docs
    * :bug: `:bug:` when fixing a bug
    * :fire: `:fire:` when removing code or files
    * :white_check_mark: `:white_check_mark:` when adding tests
    * :lock: `:lock:` when dealing with security
    * :arrow_up: `:arrow_up:` when upgrading dependencies
    * :arrow_down: `:arrow_down:` when downgrading dependencies
