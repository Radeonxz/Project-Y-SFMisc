# Create a Hello World Lightning Web Component

## Create a Salesforce DX Project

Now that you’ve set up your development environment, you can create a simple Lightning web component.

1. In Visual Studio Code, open the Command Palette by pressing `Ctrl+Shift+P` (Windows) or `Cmd+Shift+P` (macOS).
2. Type `SFDX`.
3. Select **SFDX: Create Project**.
4. Press **Enter** to accept the standard option.
5. Enter `HelloWorldLightningWebComponent` as the project name.
6. Press **Enter**.
7. Select a folder to store the project.
8. Click **Create Project**. You should see something like this as your base setup.

## Authorize Your Trailhead Playground

1. Type `SFDX`.
2. Select **SFDX: Authorize an Org**.
3. Press **Enter** to accept the Project Default login URL option.
4. Press **Enter** to accept the default alias.
5. This opens the Salesforce login in a separate browser window.
6. Log in using your Trailhead Playground credentials.
7. If prompted to allow access, click **Allow**.
8. After you authenticate in the browser, the CLI remembers your credentials.

## Create a Lightning Web Component

1. In Visual Studio Code, open the Command Palette by pressing **Ctrl+Shift+P** (Windows) or **Cmd+Shift+P** (macOS).
2. Type `SFDX`.
3. Select **SFDX: Create Lightning Web Component**. Don't use **SFDX: Create Lightning Component**. (This creates an Aura component.)
4. Enter `helloWorld` for the name of the new component.
5. Press **Enter** to accept the default `force-app/main/default/lwc`.
6. Press **Enter**.
7. View the newly created files in Visual Studio Code.
8. In the HTML file, `helloWorld.html`, copy and paste the following code.

```
<template>
  <lightning-card title="HelloWorld" icon-name="custom:custom14">
    <div class="slds-m-around_medium">
      <p>Hello, {greeting}!</p>
      <lightning-input label="Name" value={greeting} onchange={changeHandler}></lightning-input>
    </div>
  </lightning-card>
</template>
```

9. Save the file.
10. In the JavaScript file, `helloWorld.js`, copy and paste the following code.

```
import { LightningElement } from 'lwc';
export default class HelloWorld extends LightningElement {
  greeting = 'World';
  changeHandler(event) {
    this.greeting = event.target.value;
  }
}
```

11. Save the file.
12. In the XML file `helloWorld.js-meta.xml`, copy and paste the following code.

```
<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata" fqn="helloWorld">
  <apiVersion>45.0</apiVersion>
  <isExposed>true</isExposed>
  <targets>
    <target>lightning__AppPage</target>
    <target>lightning__RecordPage</target>
    <target>lightning__HomePage</target>
  </targets>
</LightningComponentBundle>
```

13. Save the file.

## Deploy to Your Trailhead Playground

1. Right-click the `default` folder under `force-app/main`.
2. Click **SFDX: Deploy Source to Org**.
3. In the Output tab of the integrated terminal, view the results of your deployment. You should have also received a notice that states: `SFDX: Deploy Source to Org ... ended with exit code 0`. This means that the command ran successfully.

## Add Component to App in Lightning Experience

1. In Visual Studio Code, open the Command Palette by pressing **Ctrl+Shift+P** (Windows) or **Cmd+Shift+P** (macOS).
2. Type `SFDX`.
3. Select **SFDX: Open Default Org**.
   This opens your Trailhead Playground in a separate browser.
4. From the App Launcher (App Launcher), find and select **Sales**.
5. Click Setup gear then select **Edit Page**.
6. Drag the `helloWorld` Lightning web component from the Custom area of the Lightning Components list to the top of the Page Canvas.
7. Click **Save**.
8. Click **Activate**.
9. Click **Assign as Org Default**.
10. Click **Save**.
11. Click Save again, then click Back arrow to return to the page.
12. Refresh the page to view your new component.
