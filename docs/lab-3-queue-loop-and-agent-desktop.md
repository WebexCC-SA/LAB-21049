# Lab 3 – Queue Loop and Agent Desktop

## Objectives:

* Learn the differences and similarities of how to build queues to route to agents.
  + Build WxCC teams and skill queues. Assign agents for routing.
  + Discuss the various queue routing options available in WxCC compared to CCE.
* Build the equivalent CCE queue script with a new WxCC flow and queues.
  + Build a queue loop and logic similar to the CCE templated script.
* Connect the 2 flows together and see how context data is passed.
  + Configure context data to pass vs. inherent in CCE
* Understanding the differences and flexibility of the WxCC agent desktop compared to Finesse agent desktop
  + Configure, modify, deliver a call to a WxCC native agent desktop.
* Complete an end-to-end call from customer to IVR to agent.

## Prerequisites:

* Complete Lab 2
* Download the required files for lab 3 and 4: [Agent Desktop and AI Agent Configs Files](./assets/download/Wx1_Lab-21049_Files.zip)

## Lab Contents:

* [3A – Queue Loop](#instructions-lab-3a-queue-loop)
* [3B – Agent Desktop](#instructions-lab-3b-agent-desktop)

## Instructions: Lab 3A – Queue Loop

* Within Collaboration Control Hub à Contact Center à “User Management”
* Click on Teams
* Build 2 Teams
  + Click “Create a Team”
  + Name: “STUxx\_Team1”
  + Parent Site: Site-1
  + Team Type: Agent Based
  + Skill profile: English Group
  + Multimedia profile: Default Multimedia Profile
  + Desktop layout: Global Layout
  + Leave Agents blank
  + Click “Create”
  + Click “Done”

![](assets/docx-image-3001.png)

  + Copy “STUxx\_Team1”
  + Rename “STUxx\_Team2”
  + Change Skill profile: Spanish Group
  + Click “Create”
  + Click “Done”

![](assets/docx-image-3002.png)

* Within Collaboration Control Hub à Contact Center à “User Management” select “Skill Management”
* Build 2 Skills
  + Click “Create a Skill”
  + Create a skill
    - Name: STUxx\_English
    - Type: Proficiency
    - Leave dynamic skill off
    - Service level threshold: 120
    - Click “Create”

![](assets/docx-image-3003.png)

  + Create another skill by duplicating the English Skill
    - Name: STUxx\_Spanish
    - Type: Proficiency
    - Leave dynamic skill off
    - Service level threshold: 120
    - Click “Create”

![](assets/docx-image-3004.png)

* Within Collaboration Control Hub à Contact Center à “User Management” select “Skill Profiles”
  + Click “Create a skill profile”
    - General: STUxx\_English
    - Select STUxx\_English and value 10
    - Click “Create”

![](assets/docx-image-3005.png)

  + Create another skill profile with Copy button
    - Rename: STUxx\_English\_Spanish
    - Select Spanish at value 10 and decrease the English value to 5
    - Click “Create”

![](assets/docx-image-3006.png)

![](assets/docx-image-3007.png)

  + Enable User Contact Center Functions
    - Within Collaboration Control Hub à Contact Center à “Contact Center User” select “STUxx\_Agent ”
    - Agent
      * Enable the “Contact Center” slider
      * Set Site to Site-1
      * Teams: Add Agent to “STUxx\_Team1”
      * Desktop Profile: Agent-Profile
      * Multimedia Profile: Default\_Multimedia\_Profile
      * Skill Profile: Add Agent to Skill Profile “STUxx\_English”
      * Click “Save”

![](assets/docx-image-3008.png)

  + - Supervisor
      * Contact Center -> Contact Center User->Enable contact center user
      * Select supervisor user
      * Enable the “Contact Center” slider
      * Primary Team: “STUxx\_Team1”
      * Site: Site-1
      * Teams: STUxx\_Team2
      * Desktop Profile: Agent-Profile
      * Multimedia Profile: Default\_Multimedia\_Profile
      * Skill Profile: STUxx\_English\_Spanish
      * Save

![](assets/docx-image-3009.png)

* Build 2 Queues
  + Within Collaboration Control Hub à Contact Center à “Customer Experience select “Queues”
  + Click “Create a queue”
    - Name the queue: STUxx\_TeamQueue
    - Description: CCE Skill-based routing equivalent
    - Contact direction: Inbound queue
    - Channel type: Telephony
    - Agent Assignment: Teams
    - Routing Pattern: Longest available

![](assets/docx-image-3010.png)

  + - Call Distribution: Click Create a group
      * Select your STUxx\_Team1
      * Save

![](assets/docx-image-3011.png)

  + - Create Group (Again) in Call Distribution
      * Priority: 2 from drop down
      * Add Group after: 10 seconds
      * Select your STUxx\_Team2
      * Save

![](assets/docx-image-3012.png)

  + - Advanced Settings
      * Select “Service Monitoring”
      * Select “Allow pause/resume for calls”
      * Leave recording pause duration at 10 seconds
      * Service Level Threshold: 30
      * Maximum time in queue: 7200 (2 hours)
      * Default music in queue: defaultmusic\_on\_hold.wav
      * Click “Create”
      * Click “Done”

![](assets/docx-image-3013.png)

  + Create 2nd Queue with Copy button of the “STUxx\_TeamQueue”
    - Name: “STUxx\_SkillQueue”
    - Description: CCE Attribute routing equivalent
    - Contact direction: Inbound queue
    - Channel type: Telephony
    - Select “Use skills-based routing for the queue”
    - Skill assignment type: “Assign skills to the queue”
    - Routing Pattern: Best available

![](assets/docx-image-3014.png)

  + - Click “Add Skill Requirement”
    - Skill Type: Proficiency
    - Skill Name: STUxx\_English (replacing xx with your student number)
    - Condition: IS
    - Skill Value: 10
    - Click Add skill requirement

![](assets/docx-image-3015.png)

  + - Click “Refresh the List” and you will see only your Agent in the Eligible User List.

![](assets/docx-image-3016.png)

  + - Press “clear all”
    - Skill Type: Proficiency
    - Skill Name: STUxx\_English
    - Condition: >=
    - Skill Value: 5
    - Click Add skill requirement
    - Click “Refresh the List” and you will see both your Agent and Supervisor
    - Save

![](assets/docx-image-3017.png)

  + - Keep all Advanced Settings the same
    - Click “Create”
    - Click “Done”

![](assets/docx-image-3018.png)

* Build the Queue loop Flow
  + - Within Collaboration Control Hub à Contact Center à Customer Experience à Select Flows ”
  + Click “Manage Flows” à Create flows
  + Use Template: “Simple Inbound Call to Queue”
  + Name the flow: STUxx\_Queue\_Flow\_Lab3
  + Click “Create Flow”

![](assets/docx-image-3019.png)

  + Update Flow Description: “CCE to WxCC Queue flow for Labs 3, 5, 6”
  + Under the Decryption settings section: “Enable decryption”, Click on “I Agree” and Save

![](assets/docx-image-3020.png)

  + Create flow Variables: Under the “Variable definition” section à Configuration
    - Click Create flow variable
    - Name: menu\_selection
    - Description: Track caller intent for routing.
    - Variable type: String
    - Default value: (optional)
    - Select “Agent Viewable”
    - Desktop label: “Caller Intent”
    - Click Create

![](assets/docx-image-3021.png)

  + Under the predefined variables Click on “+ Add global variables”
    - Select the “STUxx\_CallPath” and both existing “TransferDestination” and “TransferResult” global variables
    - Click “Add”

![](assets/docx-image-3022.png)

  + Delete the “WelcomePrompt” node and “EndFlow” node that goes with it.

![](assets/docx-image-3023.png)

  + Under Flow Control section of the Flow Designer Node Palette: add a Case node to the canvas after the NewPhoneContactNode
    - Edit the Activity Label and update the name: Case\_MenuOption
    - Select Variable: menu\_selection
    - Replace Case 0 with “English”
    - Replace Case 1 with “Spanish”

![](assets/docx-image-3024.png)

  + Drag a Set Variable node to canvas
  + Select the new Set Variable node
    - Rename the Activity Label: UpdateCallPath\_EnglishQueue
    - Activity description: Update the caller path variable
    - Select “STUxx\_CallPath” global variable in the Variable pull down
    - Set value: `{% raw %}{{STUxx_CallPath}}.EnglishQ{% endraw %}`

![](assets/docx-image-3025.png)

  + Right Click on the UpdateCallPath\_English node and Copy/Paste
  + Select the new Set Variable node
    - Rename the Activity label: UpdateCallPath\_SpanishQueue
    - Description: Update the caller path variable
    - Select “STUxx\_CallPath” global variable in the Variable pull down
    - Set value: `{% raw %}{{STUxx_CallPath}}.SpanishQ{% endraw %}`
  + Connect Case node English path to UpdateCallPath\_EnglishQueue node
  + Connect Case node Spanish path to UpdateCallPath\_SpanishQueue node
  + Connect Case node Default path to UpdateCallPath\_EnglishQueue node

![](assets/docx-image-3026.png)

  + Select the Queue node
    - Rename to : English\_Queue
    - Contact handling: Static queue
    - Queue: STUxx\_TeamQueue

![](assets/docx-image-3027.png)

  + Make another queue node by copying the English\_Queue Node
  + Select the new Queue node
    - Rename to : Spanish\_Queue
    - Contact handling: Static queue
    - Queue: STUxx\_SkillQueue

![](assets/docx-image-3028.png)

  + Connect UpdateCallPath\_EnglishQueue exit path to English\_Queue node.
  + Connect UpdateCallPath\_SpanishQueue exit path to Spanish\_Queue node.
  + Connect the new Spanish\_Queue node exit to the existing Music Node.
  + Connect the new Spanish\_Queue node failure path to EndFlow node
  + Select Music node and review settings. No changes needed.
  + Select PlayMessage node and review settings. No changes needed.

![](assets/docx-image-3029.png)

  + Click on “Validation”. It will likely identify 2 errors.
  + Click on “NewPhoneContact” error in validation menu
  + Connect the “NewPhoneContact” exit path to the “Case\_MenuOption” node

![](assets/docx-image-3030.png)

  + Validation should now run again and show 0 errors.
  + Publish Flow using the Latest version label.
* Connect the IVR and Queue flows.
  + Return to Control Hub à Flows, which should still be opened in a previous browser tab.
  + Open your “STUxx\_Lab2” flow and go into Edit mode
  + Disconnect the Play\_Option\_Selection node from the DisconnectContact node

![](assets/docx-image-3031.png)

  + Drag a Set Variable node and “Goto” node to the canvas end
  + Select the new Set Variable node
    - Rename: UpdateCallPath\_Queue
    - Description: Update the caller path variable
    - Select “STUxx\_CallPath” global variable in the Variable pull down
    - Set value: `{% raw %}{{STUxx_CallPath}}.ToQueue{% endraw %}`

![](assets/docx-image-3032.png)

  + Connect the “Play\_Options\_Selection” node to the new “UpdateCallPath\_Queue” node
  + Connect the “UpdateCallPath\_Queue” exit to the new Goto node

![](assets/docx-image-3033.png)

  + Select the GoTo node
    - Rename: Goto\_Queue
    - Description: Goto a new flow to queue the call.
    - Flow destination settings à Destination type: Flow
    - Select “Static Flow”
    - Flow: Select STUxx\_Queue\_Flow\_Lab3 built previously from the pull down.
    - Choose version label: Latest
    - Scroll to the bottom to set Decryption settings: Enable decryption

![](assets/docx-image-3034.png)

![](assets/docx-image-3035.png)

![](assets/docx-image-3036.png)

  + - Click Validation
    - Publish as Latest

![](assets/docx-image-3037.png)

## Instructions: Lab 3B – Agent Desktop

* Pull up an incognito browser
* Log in as an agent with your agent account at <https://desktop.wxcc-us1.cisco.com/>
  + Select “STUxx\_Team1”
  + Handle calls using: “Desktop”
  + Save & Continue
  + Click to acknowledge emergency service notification for using desktop/webrtc
  + If prompted for microphone permission, click allow
* Return to the browser tab for Collaboration Control Hub à Contact Center à “Desktop Experience à Select Desktop Layouts
* Copy the Global Layout
  + Rename: STUxx\_Desktop\_Layout
  + Description: (optional)
  + Remove the default teams and add your 2 new teams “STUxx\_Team1 and STUxx\_Team2 from pull down.
  + Click “Download default desktop layout”
  + Find the download and open the file in notepad or notepad++
    - Change the “appTitle” on row 4 from “Webex Contact Center” to “STUXX\_My Test Agent”
    - Set the “logo” on row 5 to url: `{% raw %}https://storage.googleapis.com/gcp-wxcctoolkit-nprd-41927.appspot.com/assets/1HWbEUeZk1YqiTLqMlB93ABQcPN2/cisco-webex-meeting-logo-png_seeklogo-372182.png{% endraw %}`
    - Save notepad file with new name: STUxx\_Desktop.json

![](assets/docx-image-3038.png)

  + Return to control hub window
  + Click on Replace File
  + Select the new desktop file name and click open
  + Click Create

![](assets/docx-image-3039.png)

  + Return to your incognito browser containing the agent desktop login session
  + Click refresh button and Reload
  + You should now see the Webex logo and your new appTitle in the top-left corner of the agent desktop
    - If you do not see this change, double-check your desktop layout json to ensure you edited the appTitle and logo within the “agent” section and not the “supervisor” or “supervisorAgent” sections.
* Keep agent not ready
* Call into your new flow, pick a menu option, and enter the queue. You should now hear queue music.
* Mute your phone and turn off speakerphone to avoid creating a feedback loop in the next step.
* Using the dropdown on the top-right corner, make agent available and take the call
* You will see Journey Data Services (JDS) events from our earlier test calls for your phone number. These are created natively in WxCC. You can also use JDS APIs to insert custom context events to augment your caller event stream.
* End the call when finished. Select any wrap-up code available.

## Finish Lab 3
