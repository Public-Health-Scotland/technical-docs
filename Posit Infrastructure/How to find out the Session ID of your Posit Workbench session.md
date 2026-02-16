# Find out the Session ID of your Posit Workbench Session

## Background

When a Workbench Session is requsted by the user, it is assigned a Session ID.  This is a long string of letters and numbers that uniquely identify the session.  The Session ID corresponds to metrics and logs that are produced by the Posit Workbench application and collected for onward analysis and debugging of issues.

## Steps to find out the Session ID of your Posit Workbench Session

1. If you have not already done so, log into Posit Workbench and start a session, following the instructions at [https://github.com/Public-Health-Scotland/technical-docs/blob/main/Posit%20Infrastructure/How%20to%20Login%20to%20Posit%20Workbench.md] if necessary.
2. After the session has started, navigate to the [Posit Workbench homepage](https://pwb.publichealthscotland.org) and identify the session you would like the Session ID of in the list of sessions e.g. circled in red below:
<img width="434" alt="image" src="https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/9496f0a2-1eb2-4466-bf35-5d56e2088f1f">

3. Click the "Info" button of the session (highlighted in yellow above) to bring up a dialog box containing further information about the session:
<img width="517" alt="image" src="https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/6fa50075-7552-4cc0-a9e1-3aa8f0eaca2f">

4. Click on "Launcher Diagnostics" (highlighted in yellow above) to view a tab with further details:
<img width="515" alt="image" src="https://github.com/Public-Health-Scotland/technical-docs/assets/45657289/c4e2839a-ed4d-413b-9a16-204b994a7947">

5. The Session ID of the session is highlighted in yellow above - it is a long string of letters and numbers.
6. To close the dialog box, click the "Close" button, circled in red above.

## Alternative method

The Session ID can be found in the URL (i.e. web address) when a session is open.  In the address bar of your web browser you will see a URL such as

```
https://pwb.publichealthscotland.org/s/bd664cfc78a31605322d7/?launcher=1
```

The long string of letters and numbers (in this case <code>bd664cfc78a31605322d7</code>) is the Session ID of the session.

This method can be useful to capture the Session ID of a session that has crashed or failed to launch successfully.
