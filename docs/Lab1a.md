## Objective:

1. Build a simple script in Webex Contact Center (WxCC) using the existing Contact Center Enterprise (CCE) flow as a template.
2. Understand how a call starts within a WxCC Flow.

## Prerequisites:

* Lab 0 familiarity with both CCE and WxCC environment and logins.

## Steps

* Open up CCE Script Editor

![](assets/docx-image-001.png)

* Open up “Wx1\_BasicFlow1” script

![](assets/docx-image-002.png)

* On your student workstation open a new Firefox/Chrome browser
* Log into Collaboration Control Hub (<HTTPS://admin.webex.com>)
  + Enter your username **(**[**STUxx.admin@wx1ccelab.wbx.ai**](mailto:STUxx.admin@wx1ccelab.wbx.ai)**)** where “xx” is your student number
  + Enter your password **(Migration101!)**

![](assets/docx-image-003.png)

![](assets/docx-image-004.png)

  + Accept the Terms of Service

![](assets/docx-image-005.png)

  + Click Accept All
* Click on the Contact Center under the Services section

![](assets/docx-image-006.png)

* Build Inbound Call Flow
  + From the Left Menu --> Under the Customer Experience Section --> “Click on Flows”

![](assets/docx-image-007.png)

* + Create a new flow from template 🡪 Manage Flows 🡪 Create Flows

![](assets/docx-image-008.png)

* + Within Webex Flow Designer 🡪Select “Use a template”
  + Click Next

![](assets/docx-image-009.png)

* + Select “Hello World” and click “Next”

![](assets/docx-image-010.png)

**Note:** If you click on “Preview”; the Flow Design opens a pop up with the following details:

* + - A Visual Representation of the Main Flow and all Event Flows
    - Description of the flow
    - Flow Details
    - Any Pre-requisites
    - Flow Breakdown
    - Activities Used
  + Rename the flow
    - Update the flow name from “HelloWorld\_Template” to “stuxx\_ Lab1”
    - Click Create Flow

![](assets/docx-image-011.png)

* + Under the “General Settings” Section of the Global flow properties 🡪 update the Flow description to “My 1st Webex Contact Center Flow”

![](assets/docx-image-012.png)

* + Under the “Decryption Settings” Section of the Global flow properties 🡪 Click “enable decryption”,

![](assets/docx-image-013.png)

* + Review the “Debug details data disclosure”
  + Click “I agree” and “Save”

![](assets/docx-image-014.png)

* + Show line grid slider.
    - View global flow properties
    - Auto arrange.
    - Undo
    - Redo
    - Fit to View
    - Zoom Out
    - Zoom In

![](assets/docx-image-015.png)

* + - Before you ask…WxCC currently does not have line connectors or comment boxes. You can add Notes in the “Activity description” for any given Node.
  + Modify the Welcome Message Text-To-Speech (TTS)
    - Click on the “WelcomeMessage” Play Message Activity Box
    - Update the existing message with “You have successfully installed the Cisco Unified V X M L server.”

![](assets/docx-image-016.png)

* + Add an additional TTS message
    - Click on “Add text-to-speech message”
    - Add message “Just kidding. You have successfully built your first WxCC Flow.”

![](assets/docx-image-017.png)

* + Preview the audio prompts:
    - Click on “Preview prompt”

![](assets/docx-image-018.png)

* + - In the Choose a voice to test the prompt dialog box select “en-US-Maria” or “en-US-Daniel”. There are several other voice options. Feel free to listen to them in other languages as time permits.

![](assets/docx-image-019.png)

* + Validate your flow
    - Click on Validation in the lower right-hand corner of the Flow Designer

![](assets/docx-image-020.png)

* + Publish the Flow. Use “latest” version label
    - Click “Publish Flow”

![](assets/docx-image-021.png)

![](assets/docx-image-022.png)

* Build Entry Point
  + Navigate back to Control Hub Contact Center
  + From the Left Menu --> Under the Customer Experience Section --> Click on “Channels”

![](assets/docx-image-023.png)

* + Click on “Create a channel”

![](assets/docx-image-024.png)

* + - Name: stuxx\_Lab1\_EP
    - Channel Type: Inbound Telephony
    - Service level threshold: 120
    - Timezone: America/Chicago
    - Routing flow: stuxx\_Lab1
    - Music on hold: SandboxUpload1.wav
    - Version label: Latest
    - Phone numbers: Click “add”
      * Webex Calling Location: Site1
      * PSTN number: Select an available phone number from the drop-down list
      * Actions: click the ![](assets/docx-image-025.png)
    - Click “Create”

![](assets/docx-image-026.png)  
![](assets/docx-image-027.png)

* Call the number. Hear the greeting
