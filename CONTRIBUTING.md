# Contributing to the PHS Data Science Knowledge Base

Firstly, thanks for taking the time to check out this guide and thinking about contributing!

The following is a set of guidelines for contributing to PHS technical documentation. As the back-end to the [PHS Data Science Knowledge Base documentation page](https://public-health-scotland.github.io/knowledge-base/docs/), there are specific requirements to ensure that the documentation is consistent and accessible.

#### Table Of Contents

[Code of Conduct](#code-of-conduct)

[I just have a question!](#i-just-have-a-question)

[Documentation Structure](#documentation-structure)

[How Can I Contribute?](#how-can-i-contribute)

* [Reporting Bugs](#reporting-bugs)
* [Requesting New Content](#requesting-new-content)
* [Pull Requests](#pull-requests)
* [Style Guides](#style-guides)

## Code of Conduct

This project and everyone participating in it are governed by the [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behaviour to [phs.datascience@phs.scot](mailto:phs.datascience@phs.scot).

## I just have a question!

> **Note:** Please don't file an issue to ask a question. You'll get faster results by using the resources below.

Whether your question is about the resources available or something about new content, the Data Science team will be able to help. A good place to start will be the [R User Group on Teams](https://teams.microsoft.com/l/team/19%3ae9f55a12b7d94ef49877ff455a07f035%40thread.tacv2/conversations?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a) or email the [Data Science team](mailto:phs.datascience@phs.scot).

## Documentation Structure

This repo forms the back-end for the [PHS Data Science Knowledge Base documentation page](https://public-health-scotland.github.io/knowledge-base/docs/). This requires a specific structure, which is outlined below, see also the [Markdown Style Guide](#markdown-style-guide) below.

### Folders / Directories

All directories need to be on a single level, with no sub-directories. Currently, the following directories are used:

* *Posit Infrastructure* - all specific content related to the Posit infrastructure, including Workbench and Package Manager.
* *Python* - content for Python within PHS.
* *R* - content for R within PHS.
* *Version Control* - content for version control within PHS.
* *Glossary* - used to host the Data Science glossary, should not be added to.

### Files

Files created should be a `.md` file within a directory, with the following considerations:

* *File name* should be human readable, in title case, with spaces. The name is directly used in the navigation bar, so should be as descriptive as possible.
  * Where the document is a step-by-step set of instructions that are universal, the file name should start with "How to ".
  * Where the document is a recommended practice, the file name should start with "Recommended ".
* *File structure* should follow standard markdown linting rules.
* *The purpose* of the document should be set out first, identifying what the document is for and what it covers.
* *Content of the document* should be written in a way that is accessible to all users, with no jargon or technical terms. Where possible, links to other documents should be used to explain concepts. If suitable, documentation to learn about concepts can be developed separately from instructions to perform a task.
* *Within-repo links* should be relative to the root of the repo. For example, a link to the `Posit Infrastructure` directory would be `[Posit Infrastructure](/Posit%20Infrastructure)`.
* *External links* should be absolute links, with the full URL. For example, a link to the Public Health Scotland website would be `[Public Health Scotland](https://publichealthscotland.scot)`.

## How Can I Contribute?

### Reporting Bugs

This section guides you through submitting a bug report. Bugs in this context are likely to include everything from typos, to false or misleading content as part of documentation. Following the guidelines set out here helps understand your report, reproduce the behaviour, and find related reports.

Before creating bug reports, please check [this list](#before-submitting-a-bug-report) as you might find out that you don't need to create one. When you are creating a bug report, please [include as many details as possible](#how-do-i-submit-a-good-bug-report). Fill out [the required template](https://github.com/Public-Health-Scotland/knowledge-base/blob/master/.github/ISSUE_TEMPLATE/bug_report.md), the information it asks for helps us resolve issues faster.

> **Note:** If you find a **Closed** issue that seems like it is the same thing that you're experiencing, open a new issue and include a link to the original issue in the body of your new one.

#### Before Submitting A Bug Report

* **Perform a cursory search of [current issues](https://github.com/Public-Health-Scotland/technical-docs/issues)** to see if the problem has already been reported. If it has **and the issue is still open**, add a comment to the existing issue instead of opening a new one.

#### How Do I Submit A (Good) Bug Report?

Bugs are tracked as [GitHub issues](https://guides.github.com/features/issues/). After you've determined a bug exists, use the appropriate template to [create an issue](https://github.com/Public-Health-Scotland/technical-docs/issues/new/choose).

The templates should prompt for relevant information. In addition, ensure you provide a clear and descriptive title, leaving the initial placeholder of "BUG" or "REQ".

### Requesting New Content

This section guides you through submitting a request, including completely new documentation and minor improvements to existing functionality. Following these guidelines helps maintainers and the community understand your suggestion and find related suggestions.

Before creating enhancement suggestions, please check [this list](#before-submitting-a-suggestion) as you might find out that you don't need to create one. When you are creating an enhancement suggestion, please [include as many details as possible](#how-do-i-submit-a-good-enhancement-suggestion). Then, fill in the appropriate template by [submitting an issue](https://github.com/Public-Health-Scotland/technical-docs/issues/new/choose).

#### Before Submitting a Suggestion

* **Perform a [cursory search](https://github.com/Public-Health-Scotland/technical-docs/issues)** to see if the enhancement has already been suggested. If it has, add a comment to the existing issue instead of opening a new one.

#### How Do I Submit A (Good) Enhancement Suggestion?

Enhancement suggestions are tracked as [GitHub issues](https://guides.github.com/features/issues/). When you have an enhancement suggestion, create an issue and follow the template prompts to provide as much detail as possible. If you're planning on submitting a pull request, you can be slightly less verbose in the description of what you'd like. You can then follow the [Pull Request Guidelines](#pull-requests) below.

### Pull Requests

The process described here has several goals:

* Maintain quality
* Fix problems that are important to users
* Engage the community in working toward the best possible documentation
* Enable a sustainable system for maintainers to review contributions

Please follow these steps to have your contribution considered by the maintainers / reviewers (the [Data Science team](mailto:phs.datascience@phs.scot)):

1. Follow all instructions in the template, this will auto-populate when you open a Pull Request.
2. Follow the [style guides](#style-guides)
3. On the pull request, set the [Data Science Team](https://github.com/orgs/Public-Health-Scotland/teams/data-science) as reviewer.  
   **Note:** setting the reviewers would only be possible if you are a member of the [All PHS Team](https://github.com/orgs/Public-Health-Scotland/teams/all-phs). If you are not a member of that team, please request to join with the button in the top-right corner of the [team's page](https://github.com/orgs/Public-Health-Scotland/teams/all-phs).

While the prerequisites above must be satisfied prior to having your pull request reviewed, the reviewer(s) may ask you to complete additional design work, tests, or other changes before your pull request can be ultimately accepted.

## Style Guides

### Git Style Guide

See the [PHS GitHub Guidance](Version%20Control/GitHub%20Guidance.md) for the full guidance document, some main points are highlighted here:

#### Commits

* use the present tense ("Add feature" not "Added feature")
* use the imperative mood ("Move cursor to..." not "Moves cursor to...")
* are limited to 72 characters or less

#### Branches

* are named in lowercase, with hyphens between words, referencing the issue they are targeting
* short-lived for specific issues, and deleted once merged

### Markdown Style Guide

#### Headings

* use `#` for the main heading, `##` for sub-headings, and so on, this should be incremental

#### Lists

* use either `-` or `*` for unordered lists, do not mix
* use `1.` (and so on) for ordered lists

#### Links

* use relative links where possible, for example `[Posit Infrastructure](/Posit%20Infrastructure)`
* external links should be absolute, for example `[Public Health Scotland](https://publichealthscotland.scot)`, do not leave bare URLs

#### Images

* use relative links where possible, for example `![Posit Infrastructure](/Posit%20Infrastructure/posit-infrastructure.png)`
