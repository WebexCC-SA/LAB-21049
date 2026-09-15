# Lab 2 – DTMF IVR Menu

## Objectives:

* Recreate the CCE script template’s DTMF menu using native WxCC flow building elements.
* Understand the differences between global variable and flow variables relative to CCE global variable and peripheral/ECC variables.
  + Create and use global variables and flow variables.
* See basic tracing and debugging of flows in WxCC and compare to monitoring a CCE script.

## Prerequisites:

* Complete Lab 1

## Instructions: Lab 2

* Create a reportable Global Variable for tracking
  + We will insert in our flows to start tracking and will show how to report on it in a later lab.
  + From the Left Menu --> Under the Customer Experience Section --> “Click on Flows”
  + Click on “Global Variables” tab
  + Click on “Create a global variable”

![](assets/docx-image-2001.png)

  + Click “Create a global variable” button in the upper right
    - Name: STUxx\_CallPath
    - Description: “Path the caller took through the flow”
    - Variable type: String
    - Report settings: Make Reportable
    - Click “Create” ![](assets/docx-image-2002.png)
* Build 2nd flow
  + Copy flow you created in lab 1A
    - Click the … for STUxx\_Lab1 and select “Copy”

![](assets/docx-image-2003.png)

  + Open the newly-copied flow named “Copy\_STUxx\_Lab1\_...”
  + Toggle the “Edit” slider to edit the flow
  + Rename/Edit name the flow to “STUxx\_Lab2”

![](assets/docx-image-2004.png)

  + Save new name

![](assets/docx-image-2005.png)

  + Click in open area to bring up Global Flow properties
  + Update the flow description: “Flow for Labs 2 and 4”

![](assets/docx-image-2006.png)

  + Add a flow variable
    - Under the “Variable definition” click “Create flow variables”

![](assets/docx-image-2007.png)

  + - Name: menu\_selection
    - Description: Track the option selected from the menu.
    - Variable type: String
    - Default value: (leave blank)
    - Enable “Agent Viewable”
    - Desktop label: “Caller Intent”
    - Click Create

![](assets/docx-image-2008.png)

  + Create a second flow variable
    - Click Create flow variables
    - Name: ni\_nm\_counter
    - Description: Track the no input and no matches.
    - Variable Type: Integer
    - Default value: 0
    - Click Create
  + Under Global variables click on “+ Add global variables”
    - Select your “STUxx\_CallPath” with xx matching your student number, and both existing “TransferDestination” and “TransferResult” global variables
    - Click “Add”

![](assets/docx-image-2009.png)

  + Under the Search activities on the left hand side of the Flow Designer 🡪 Search for “Set Variable”

![](assets/docx-image-2010.png)

  + Move the NewPhoneContact node to the left to make some room between it and the WelcomeMessage node. Then drag a Set Variable node between the NewPhoneContact node and the WelcomeMessage node
  + Delete the path from the NewPhoneContact to the WelcomeMessage

![](assets/docx-image-2011.png)

  + Connect the NewPhoneContact exit to the new Set Variable Node.

![](assets/docx-image-2012.png)

  + Click on the new Set Variable Node
    - Rename the node/change the Activity label: SetInitialData
    - Description: Set or initialize and variables for use later.

![](assets/docx-image-2013.png)

  + - Under “Variable settings“ select “STUxx\_CallPath” from the drop down
    - Set value: “STUxx\_Lab2\_IN” replacing xx with your student number

![](assets/docx-image-2014.png)

  + Connect SetInitialData success exit path to WelcomeMessage node

![](assets/docx-image-2015.png)

  + Click on the “WelcomeMessage” node
    - Change 1st TTS message: “This is my flow for lab 2”
    - Delete the 2nd TTS message

![](assets/docx-image-2016.png)

  + Clear the “Search Activities” field and add a new Menu Node after the WelcomeMessage
  + Delete the success path out arrow of the Welcome Message and connect to new Menu Node
  + Select Menu Node
    - Rename the node/change the Activity label “Main\_Menu”. ![Lights On with solid fill](assets/docx-image-2017.png)Remember to click on the check mark to save the Activity label.

![](assets/docx-image-2018.png)
  + - Scroll down to the “prompt section”
    - Select Enable text-to-speech
    - Select “Cisco Cloud Text-to-Speech” from Connector pull down
    - Click “Add text-to-speech message” button
    - Add text to speech messages for 2 options: “Press 1 for English. Press 2 for Spanish”
    - Click trashcan to delete audio file entry
    - Minimize the “prompt” section

![](assets/docx-image-2019.png)

  + - Expand the “Custom menu links” section
    - Select Digit Number “1” from pull down.
    - Name the option in Link Description “English”
    - Click “+Add new”
    - Select Digit Number “2” from pull down.
    - Name the option in Link Description “Spanish”

![](assets/docx-image-2020.png)

  + Drag a “Set Variable” Node on to the Flow Designer Canvas after the Menu
  + Connect “English” to this set variable node
  + Click on the Set Variable Node
    - Rename the node/change the Activity label: SetVar\_Opt1
    - Description: (Optional)
    - Under the Variable settings select “menu\_selection” variable from the drop-down menu
    - Set value: “English”

![](assets/docx-image-2021.png)

  + Click “+ Add new” under Variable settings to set another variable
    - Select “STUxx\_CallPath” variable from the pulldown
    - Set value: '{{STUxx_CallPath}}.english'
      * Feel free to test with test expression icon![](assets/docx-image-2022.png) , entering STUxx\_Lab2\_IN from the SetInitialData node as the value for STUxx\_CallPath

![](assets/docx-image-2023.png)

  + Right click on “SetVar\_Opt1” and copy. If the browser prompts you to approve, click Allow.
    - Right click mouse in open space under “SetVar\_Opt1” and “paste”
    - Rename the node/change the Activity label: SetVar\_Opt2
    - Description: (Optional)
    - For variable “menu\_selection”
    - Set value: “Spanish”
    - For variable 'STUxx_CallPath', set value: '{{STUxx_CallPath}}.spanish'
      * (Feel free to test with test expression icon)
    - Connect Main\_Menu option 2 path to new “SetVar\_Opt2” node

![](assets/docx-image-2024.png)

  + Drag a “PlayMessage” node to canvas
  + Connect the success paths of both “SetVar” nodes to the new PlayMessage Node

![](assets/docx-image-2025.png)

  + Open the PlayMessage node
    - Rename the node/change the Activity label: Play\_Option\_Selection
    - Select Enable text-to-speech
    - Select “Cisco Cloud Text-to-Speech” from Connector pull down
    - Click “Add text-to-speech message” button twice
    - Click trashcan to delete audio file entry
    - In the first text-to-speech message: “You picked {{menu\_selection}} path” (no quotes)
    - In the second text-to-speech message: “This was option {{Main\_Menu.OptionEntered}}” (no quotes)
  + Connect the exit of the PlayMessage node to the DisconnectContact Node

![](assets/docx-image-2026.png)

* Menu Error Path build
  + Drag another PlayMessage node to the canvas
  + Connect the Main\_Menu node “No-Input Timeout” and “Unmatched Entry” to the new PlayMessage node
  + Click on PlayMessage node
  + Rename the node/change the Activity label: Play\_Menu\_Error
  + Select Enable text-to-speech
  + Select “Cisco Cloud Text-to-Speech” from Connector pull down
  + Click “Add text-to-speech message”
  + In the text-to-speech message: “Your entry was not recognized” (no quotes)
  + Click trashcan to delete audio file entry

![](assets/docx-image-2027.png)

  + Drag a Set Variable node to the canvas
    - Connect the outbound of the “Play\_Menu\_Error” node to the newly-added Set Variable node

![](assets/docx-image-2028.png)

  +  Click on the Set Variable Node
    - Rename the node/change the Activity label: Increment\_NI\_NM\_Counter
    - Description: (Optional)
    - Select “ni\_nm\_counter” variable from the drop down menu
    - Set value: {{ni\_nm\_counter+1}}
    - Click on formula test icon in set value box (looks like </>)
    - Press “Test expression”. Should see Test Result of 1
    - Change the ni\_nm\_counter to 5
    - Press “Test expression”. Should see Test Result of 6
    - Press “Apply changes” or “Close” if no changes were made

![](assets/docx-image-2029.png)

  + Drag a “Condition” node to the canvas
  + Connect the outbound of the Increment\_NI\_NM\_Counter node to the new condition node

![](assets/docx-image-2030.png)

  + Click on the new Condition Node
    - Rename the node/change the Activity label: Check\_NI\_NM\_Counter
    - Description: (Optional)
    - Set Condition Expression to value: {{ni\_nm\_counter>2}}
    - Click on formula test icon in set value box (looks like </>)
    - Press “test Expression”. Should see Test Result of “false”
    - Change the ni\_nm\_counter to 5
    - Press “Test expression”. Should see Test Result of “true”
    - Press “Apply changes” or “Close” if no changes were made

![](assets/docx-image-2031.png)

  + Connect the “True” path of the Condition node to the DisconnectContact Node

![](assets/docx-image-2032.png)

  + Connect the “False” path back to the Main\_Menu node. If you aren’t able to see both on the screen at once, you can zoom out with CTRL + the mouse wheel or by clicking the ![](assets/docx-image-2033.png) a the bottom of the screen.

![](assets/docx-image-2034.png)

  + Enable Validation at the bottom-right
  + Resolve any errors
  + Publish Flow
* In Control Hub 🡪 Channels rename your Entry point from STUxx\_Lab1\_EP to STUxx\_Lab2\_EP
* Change your “Routing Flow” dropdown from “STUxx\_Lab1” to “STUxx\_Lab2”
* Click Save

![](assets/docx-image-2035.png)

* Make three (3) calls into your flow and test the Main\_menu paths
  + For the 1st call – select option 1 and listen to the prompts
  + For the 2nd call – select option 2 and listen to the prompts
  + For the 3rd call – do not select an option and listen to the prompts

**Bonus Exercise (Time Permitting)**

* Navigate back to your STUxx\_Lab2 browser tab
  + Select Analyze at bottom left side of the screen

**![](assets/docx-image-2036.png)**

* Click “Last 15 minutes” under the “Set the date and time range for your data” section
    - Take note of the date and time range options
  + Click on Main\_Menu node to drill down
    - For the interaction with outcome “error” -> Click on “View in debug”

**![](assets/docx-image-2037.png)**

  + We are now in the Debug view for this call. Notice the animated “--- blue lines” show the path of this specific call through the flow
  + In the list of activities on the bottom-left, select “Main\_Menu” activity name showing outcome “Error”
  + You should see No-input timeout = 3, matching our condition node logic

**![](assets/docx-image-2038.png)**

  + Optionally, look at other interactions that were successful

**![](assets/docx-image-2039.png)**

  + Select Design at bottom right to exit back to build

## Finish Lab 2
