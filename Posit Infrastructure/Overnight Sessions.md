# Overnight Sessions

## Purpose

This document aims to provide users with information on running Posit Workbench sessions overnight.

## Background

An automated process has been put in place to close sessions in Posit Workbench at 9pm every evening.

This automated process can be overridden by including the word "NIGHT" at the start of the name of the relevant Posit Workbench session, **when the session is started**.

## Process to start a "NIGHT" session

A Posit Workbench session that a user would like to continue running past 9pm must be named with the word "NIGHT" **when the session is started**.  The following steps must be carried out to ensure that the session remains open past 9pm:

1. After successfully logging into Posit Workbench, the user will be presented with the following screen:

![The Posit Workbench homepage with the + New Session button circled in red](https://user-images.githubusercontent.com/45657289/199207826-9fb88d1c-88e6-4418-9cec-1ec8a0f02875.png)

2. Click the "+ New Session" button (circled in red above) to open the New Session dialogue box (see screenshot below):

![New Session dialogue with the word NIGHT highlighted in yellow at the start of the session name](https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/62a2a8ff-2df5-4832-8c4f-681eb028e713)

3. Edit the text in the "Session Name" field such that the word "NIGHT" precedes all other text, e.g. "NIGHT My R Session" (see screenshot above).

4. Amend any other settings as required in the "New Session" dialogue box, and click the blue "Start Session" button.  The session will start as normal.

**Important Note:** If you open a project from within a session started by following the steps above, the process of opening that project will start another session and close your "NIGHT" session.  As such, the session that the project opens in will no longer have "NIGHT" at the start of its name, and it will be closed at 9pm by the automated process.

## Process to open a "NIGHT" project

1. Firstly, ensure that the project's .Rproj file and root directory (i.e. the directory that contains the .Rproj file) both share the same name, and that the name has the word "NIGHT" at the start, e.g. "/conf/linkage/output/NIGHT my project/NIGHT my project.Rproj"

2. Follow the steps outlined at [https://github.com/Public-Health-Scotland/technical-docs/blob/main/Posit%20Infrastructure/How%20to%20Login%20to%20Posit%20Workbench.md] to log in to Posit Workbench and start a new session.

3. Follow steps outlined at [https://github.com/Public-Health-Scotland/technical-docs/blob/main/Posit%20Infrastructure/FAQs.md#projects] to open the project.
