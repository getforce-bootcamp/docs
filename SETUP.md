### Requirements
- [Enable Dev Hub in your Org](https://www.youtube.com/watch?v=Y1pZ9sFcILo)
- [Install Salesforce CLI](https://developer.salesforce.com/tools/sfdxcli)
- [Install Git](https://git-scm.com/downloads)
- [Install Fork](https://git-fork.com/)
- [Install Visual Studio Code](https://code.visualstudio.com/download)
- [Set Up Visual Studio Code](https://trailhead.salesforce.com/content/learn/projects/quick-start-lightning-web-components/set-up-visual-studio-code)

## Clone Repository
Copy address of project repository.
<p align="center"><img width="913" alt="" src="https://user-images.githubusercontent.com/89274213/190679377-c5ea3a0e-27c2-4b42-9843-6f294f244238.png"></p>

Open **Fork** application and go to **File -> Clone**. Paste your url in a new window and click **Clone**.

<p align="center"><img width="600" alt="" src="https://user-images.githubusercontent.com/89274213/190686359-14397c89-1ac6-47a3-829e-954b0eff9be2.png"></p>

## Visual Studio Code
Open new generated folder in Visual Studio Code and paste next command to Terminal in order to authorize your hub org:
```
sfdx auth:web:login -d -a devhub
```
Authorize to your Salesforce org in a new opened login page:
<p align="center"><img width=400" alt="" src="https://user-images.githubusercontent.com/89274213/190689214-3af96c24-1ee0-4099-a62a-c41293441109.png"></p>

## Scratch Org
1. Create a scratch org:

    ```
    sfdx force:org:create -s -f config/project-scratch-def.json -a app
    ```

1. Push the app to your scratch org:

    ```
    sfdx force:source:push
    ```  
1. Open the scratch org:

    ```
    sfdx force:org:open
    ```
