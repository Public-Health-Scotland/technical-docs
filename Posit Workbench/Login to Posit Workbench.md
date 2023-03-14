# Log in to Posit Workbench

## Logging in to Posit Workbench

The Posit Workbench server is accessed via a web browser. To log in, follow the steps below:

1. Ensure you are connected to the VPN (or connected to the internal network if you're on-site).

2. Open a web browser.

3. Navigate to Posit Workbench at: [https://pwb.publichealthscotland.org/](https://pwb.publichealthscotland.org/)

4. You will be presented with the following login page:

    ![Posit Workbench login screen](https://user-images.githubusercontent.com/45657289/186685760-da0d9dc6-cfe8-4afc-93fd-7afaaf6fd91d.png)

5. Enter your LDAP username and password (the same credentials you use to login to your computer).

6. Click the "Sign In" button (circled in red above), or press the "enter" key on your keyboard.

7. If the credentials you entered are correct, you will be presented with the following home page:

    ![Posit Workbench landing page](https://user-images.githubusercontent.com/45657289/199207826-9fb88d1c-88e6-4418-9cec-1ec8a0f02875.png)

## Starting a new session

1. From the screen shown above, click the "+ New Session" button (circled in red above)

2. This will provide a popup with some options as shown below for how to set up your session:
    - The 'Session Name' can be left as the default or you can provide something more specific for you to identify. This could be useful if you require multiple sessions open at once.
    - The 'Editor' allows you to select an IDE (Integrated Development Environment): RStudio (default), Jupyter Lab, Jupyter Notebook, or VS Code.
    - 'Cluster' can only be Kubernetes
    - There is separate guidance for selecting a suitable session size in [Posit Workbench and Kubernetes](Posit%20Workbench%20and%20Kubernetes.md).

        ![Posit Workbench New Session Popup](https://user-images.githubusercontent.com/33964310/213692731-889e1f04-c2da-4f2f-b5bf-f82c445b58ae.png)

3. Once you are satisfied with the details entered on the 'New Session' screen, click the "Start Session" button.

> Due to the setup of the server, the session can take up to 1 min to become available. Once available, you may automatically join or can click on the session listed on the home page.

![Posit Workbench Active Session - ready](https://user-images.githubusercontent.com/45657289/199208971-bf977d57-b042-4e43-9e15-b9b107dc89bc.png)

> If the session takes longer or fails to open, this could indicate an issue and should be raised through the appropriate support channels. This is detailed in the [Posit Support](Posit%20Support.md) document.

4. Once the session has opened, you will need to read the prompt in the console pane, including the Acceptable Usage Policy, and follow the instructions.
