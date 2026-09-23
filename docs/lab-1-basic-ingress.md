# Lab 1 – Basic Ingress

## Objective:

1. Build a simple script in Webex Contact Center (WxCC) using the existing Contact Center Enterprise (CCE) flow as a template.
2. Understand how a call starts within a WxCC Flow and similarities to CCE dialed numbers, call types, and scripts.
3. Configure and test native Webex Text-to-Speech

## Prerequisites:

* Lab 0 familiarity with both CCE and WxCC environment and logins.

## Instructions: Lab 1

* You should still be logged in as [STUxx.admin@wx1ccelab.wbx.ai](mailto:STUxx.admin@wx1ccelab.wbx.ai) from Lab 0. If not:
  + On your student workstation open a new Firefox/Chrome browser and log into Collaboration Control Hub (<HTTPS://admin.webex.com>)
  + Enter your username **(**[**STUxx.admin@wx1ccelab.wbx.ai**](mailto:STUxx.admin@wx1ccelab.wbx.ai)**)** where “xx” is your student number
  + Enter your password: **Migration101!**
* Build Inbound Call Flow
  + From the Left Menu --> Under the Customer Experience Section --> “Click on Flows”

![](assets/docx-image-1001.png)

  + Create a new flow from template a Manage Flows a Create Flows

![](assets/docx-image-1002.png)

  + Within Webex Flow Designer a Select “Use a template”
  + Click Next

![](assets/docx-image-1003.png)

  + Select “Hello World” and click “Next”

![](assets/docx-image-1004.png)

**Note:** If you click on “Preview”; the Flow Design opens a pop up with the following details:

  + A Visual Representation of the Main Flow and all Event Flows
    - Description of the flow
    - Flow Details
    - Any Pre-requisites
    - Flow Breakdown
    - Activities Used
  + Rename the flow
    - Update the flow name from “HelloWorld\_Template” to “STUxx\_ Lab1”
    - Click Create Flow

![](assets/docx-image-1005.png)

  + Under the “General Settings” Section of the Global flow properties a update the Flow description to “My 1st Webex Contact Center Flow”

![](assets/docx-image-1006.png)

  + Under the “Decryption Settings” Section of the Global flow properties a Click “enable decryption”,

![](assets/docx-image-1007.png)

  + Review the “Debug details data disclosure”
  + Click “I agree” and “Save”

![](assets/docx-image-1008.png)

  + Show line grid slider.
    - View global flow properties
    - Auto arrange.
    - Undo
    - Redo
    - Fit to View
    - Zoom Out
    - Zoom In

![](assets/docx-image-1009.png)

  Note: WxCC currently does not have line connectors or comment boxes. You can add Notes in the “Activity description” for any given Node.
  
  + Modify the Welcome Message Text-To-Speech (TTS)
    - Scroll down to the “Text-to-speech message” free-form text box
    - Replace the existing “Hello World” message with “You have successfully installed the Cisco Unified V X M L server.”

![](assets/docx-image-1010.png)

  + Add an additional TTS message
    - Click on “Add text-to-speech message”
    - Add message “Just kidding. You have successfully built your first WxCC Flow.”

![](assets/docx-image-1011.png)

  + Preview the audio prompts:
    - Click on “Preview prompt”

![](assets/docx-image-1012.png)

    - In the Choose a voice to test the prompt dialog box select “en-US-Maria” or “en-US-Daniel”. There are several other voice options. Feel free to listen to them in other languages as time permits.

![](assets/docx-image-1013.png)

  + Validate your flow
    - Click on Validation in the lower right-hand corner of the Flow Designer

![](assets/docx-image-1014.png)

  + Publish the Flow. Use “Latest” version label
    - “Latest” version label is checked by default
    - Click “Publish Flow”

![](assets/docx-image-1015.png)

![](assets/docx-image-1016.png)

+ Build Entry Point
  - Navigate back to Control Hub Contact Center, which should still be opened in another browser tab
  - From the Left Menu --> Under the Customer Experience Section --> Click on “Channels” ![](assets/docx-image-1017.png)
  - Click on “Create a channel”

![](assets/docx-image-1018.png)

  + Update the configuration:
    - Name: STUxx\_Lab1\_EP
    - Channel Type: Inbound Telephony
    - Service level threshold: 120
    - Timezone: America/Chicago
    - Routing flow: STUxx\_Lab1
    - Music on hold: SandboxUpload1.wav
    - Version label: Latest
    - Phone numbers: Click “add”
      * Webex Calling Location: Site1
      * PSTN number: Select an available phone number from the drop-down list
      * Actions: click the ![](assets/docx-image-1019.png)
    - Click “Create”

![](assets/docx-image-1020.png)

* Call the number you selected. Hear the greeting

## Finish Lab 1
