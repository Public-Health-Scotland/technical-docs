# Access Posit Workbench

* [New User](#new-user)
* [Deactivated User](#deactivated-user)
* [Logging in](#logging-in)
  * [Starting a session](#starting-a-session)

## New user

If you're new to Posit Workbench and require access for your role, a user account and relevant access are set up by DaS, including access to Posit Package Manager. This follows a similar process to the 'Access to Data' process, requires line manager approval, and is subject to the [Acceptable Usage Policy](Acceptable%20Usage%20Policy%20for%20Posit%20Workbench.md). Accounts may be deactivated after a period of inactivity; if this affects you, see [Deactivated User](#deactivated-user).

1. Go to [ServiceNow](https://nhsnss.service-now.com/phs/) > Digital & Security > Service Catalog > Make a Request
2. Select 'Corporate Applications' as the Product or Service
3. Another dropdown will appear where you can select the appropriate Posit application. In this case, Workbench.
4. Complete the rest of the form, and attach authorisation from your line manager (similar to the Access to Data process).
5. Submit the request!

## Deactivated user

As part of the standard licence management processes for Posit, to keep us compliant with our licence agreement, we regularly review activity across the platform. Where accounts are found to be inactive, you will receive communication about the deactivation of your account. This process maintains user settings and data, with reactivation prioritised to be expected within 48 hours. 

To request reactivation, email the Data Science team ([phs.datascience@phs.scot](mailto:phs.datascience@phs.scot)) **with your LDAP username** and this will be actioned. 

## Logging in

The Posit Workbench server is accessed via a web browser. To log in, follow the steps below:

1. Ensure you are connected to the VPN (or connected to the internal network if you're on-site).

2. Open a web browser.

3. Navigate to Posit Workbench at: [https://pwb-prod.publichealthscotland.org/](https://pwb-prod.publichealthscotland.org/)

4. You will be presented with the following login page:

    ![Posit Workbench login screen](https://user-images.githubusercontent.com/45657289/186685760-da0d9dc6-cfe8-4afc-93fd-7afaaf6fd91d.png)

5. Enter your LDAP username and password (the same credentials you use to log in to your computer).

6. Click the "Sign In" button (circled in red above), or press the "enter" key on your keyboard.

7. If the credentials you entered are correct, you will be presented with the following home page:

    ![Posit Workbench landing page](https://user-images.githubusercontent.com/45657289/199207826-9fb88d1c-88e6-4418-9cec-1ec8a0f02875.png)

### Starting a session

1. From the screen shown above, click the "+ New Session" button (circled in red above)

2. This will provide a pop-up with some options, as shown below for how to set up your session:
    - The 'Session Name' can be left as the default, or you can provide something more specific for you to identify the session later. This could be useful if you require multiple sessions open at once.
    - The 'Editor' allows you to select an IDE (Integrated Development Environment): RStudio (default), Jupyter Lab, Jupyter Notebook, or VS Code.
    - 'Cluster' can only be Kubernetes
    - There is separate guidance for selecting a suitable session size in [Posit Workbench and Kubernetes](Posit%20Workbench%20and%20Kubernetes.md).

        ![Posit Workbench New Session Popup](https://user-images.githubusercontent.com/33964310/213692731-889e1f04-c2da-4f2f-b5bf-f82c445b58ae.png)

3. Once you are satisfied with the details entered on the 'New Session' screen, click the "Start Session" button.

> Due to the setup of the server, the session can take up to 1 min to become available. Once available, you may automatically join or can click on the session listed on the home page.

![Posit Workbench Active Session - ready](https://user-images.githubusercontent.com/45657289/199208971-bf977d57-b042-4e43-9e15-b9b107dc89bc.png)

> If the session takes longer or fails to open, this could indicate an issue and should be raised through the appropriate support channels. This is detailed in the [Posit Support](Posit%20Support.md) document.

4. Once the session has opened, you will need to read the prompt in the console pane, including the Acceptable Usage Policy, and follow the instructions.
