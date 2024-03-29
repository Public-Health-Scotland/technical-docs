# Posit Support Information

## Purpose

This document aims to provide users of Posit Team applications with contact information for seeking support.

## Requesting a change to your Posit Workbench Kubernetes Profile

The Kubernetes Profile that a user's account is assigned to determines the maximum amount of CPU and/or Memory (RAM) that the user can request for a Posit Workbench session.

The form at [https://forms.office.com/e/VEutAJ8p9Y](https://forms.office.com/e/VEutAJ8p9Y) allows you to submit a request for a change to your Posit Workbench Kubernetes Profile, or a request on behalf of someone else.

Before submitting the request, please consult the [Posit Workbench and Kubernetes](Posit%20Workbench%20and%20Kubernetes.md) document for recommendations on how many CPUs and memory are likely to be required.

Authorisation for the request is required from the person's line manager, and will be sought automatically via Microsoft Approvals in Microsoft Teams.  Once authorisation has been granted:

1. Go to [ServiceNow](https://nhsnss.service-now.com/phs/) > Digital & Security > Service Catalog > Make a Request
2. Select 'Corporate Applications' as the Product or Service
3. Another dropdown will appear where you can select the appropriate Posit application. In this case, Workbench.
4. Complete the rest of the form, and attach the PDF authorisation generated by Microsoft Approvals to the request.
5. Submit the request!

## All other types of support request

Public Health Scotland's Data Science team will be providing first-line support for Posit Team applications and will be triaging all queries and requests for support with Posit applications. Before raising a support request, please make sure to try the following troubleshooting steps that may resolve the issue you are experiencing more quickly:

- **Check the Console Prompt**: At the start of every new session, you are asked to confirm the Acceptable Usage Policy for Posit, this means that if you switch projects, the prompt will come up again. While this is expected, it can be easy to forget and means code won't run. 
- **Check Error Messages**: The Posit Team applications, R, Shiny, Python and any other programming language you may be using all generate error messages when something goes wrong. This is expected behaviour in many cases and can be related to the code you have written, a malfunction in a connected system such as a database or publishing platform, or the application or infrastructure itself. Error messages can be confusing and may not initially appear to bear any resemblance or connection to your code, but they can help you understand the issue and suggest the steps to take to resolve it. Make sure to read the error message carefully and try to understand what it is telling you, even by just pasting it into Google to see if anybody else has experienced a similar problem _and found a solution_.  The [Stack Overflow](https://stackoverflow.com/) website really can be your friend in these instances.
- **Restart Session**: Oh yeah, the old _turn it off and on again..._ - it does help though, restarting the session or logging out and logging in again can fix the issue. This can clear up any temporary issues that might be causing the problem.
- **Consult with Peers**: The [PHS R User Group on Teams](https://teams.microsoft.com/l/team/19%3ae9f55a12b7d94ef49877ff455a07f035%40thread.tacv2/conversations?groupId=ec4250f9-b70a-4f32-9372-a232ccb4f713&tenantId=10efe0bd-a030-4bca-809c-b5e6745e499a) has many of your colleagues, some of which may be familiar with the issue you're experiencing, consider reaching out to them when coding issues occur - they're a friendly bunch!
- **Search Documentation**: Extensive online documentation with troubleshooting guides, tutorials, and user forums where you can ask questions and get answers from other users are available for Posit Workbench and specific coding problems. Some of this is internal, available on the [PHS Data Science Knowledge Base](https://public-health-scotland.github.io/knowledge-base/).
- **Check Connectivity**: If you're experiencing connectivity issues, check your internet connection or network settings. You might need to check firewalls, VPN settings, or other network configurations. This might be the case if you're having issues connecting to other internal systems, in which case, contact DaS directly through [Service Now](https://nhsnss.service-now.com/phs/).
- **Check Access Permissions**: Ensure that you have access permissions to the server or specific data sets. Check with someone else in your team, or DaS (via [Service Now](https://nhsnss.service-now.com/phs/)) to confirm your access permissions. _All database connections that were available on the old server infrastructure have been migrated and made available for testing during UAT._
- **Check Browser**: Sometimes, the issue might be related to the browser you are using. This has been identified in a couple of areas already with Mozilla Firefox. Try using a different browser to see if the issue persists; all Chromium based browsers are tested and work as expected (i.e. Microsoft Edge and Google Chrome).

If you have followed these troubleshooting steps and the issue still persists, please raise a support request by providing the following details (you can also use this form to reach out with questions about the infrastructure).:

- Specific steps taken that led to the issue
- Error messages or symptoms
- As exact a time as possible when the error occurred (to the second if possible)
- Steps you have already taken to resolve the issue
- Any recent changes made to your system or the server
- Any relevant log files or screenshots that can help identify the issue

In essence, please provide as much detail as possible in your request.  The more detail, the easier it will be to find the cause of the issue you are experiencing.

Please complete the form at [https://forms.office.com/e/pqmmNMkhT6](https://forms.office.com/e/pqmmNMkhT6). **Any request/query must use this process to ensure that they can be assigned and followed through by someone in the team, but also to ensure wider problems are identified and resolved.**

The team aim to respond to all queries and requests for support submitted via this form as quickly as possible.

**Queries** and **requests** for support with Posit applications cannot be made directly in Service Now by users, unless explicitly authorised by the Data Science team.

**Please do not raise a request or incident in Service Now related directly to Posit applications unless requested by a member of the Data Science team.**
