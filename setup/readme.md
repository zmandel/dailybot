# Setup instructions
Note: You might want to first use a "test" channel with just you as a member in the channel and tag. Once its working, replace with the final values.

1. Pick a Teams channel where the bot will publish Daily responses (channel 1) , and a channel where the "daily.xlsx" historical data will be saved (channel 2). Both channels could be the same. The team from "Channel 1" must have a [tag](https://support.microsoft.com/en-us/office/using-tags-in-microsoft-teams-667bd56f-32b8-4118-9a0b-56807c96d91e) that defines the team members for the daily.
   
2. Download [daily.xlsx](https://github.com/zmandel/dailybot/blob/main/setup/daily.xlsx) and place it somewhere in "channel 2" files. The Power Automate flow publisher must have "write" permission to this file. It can be placed on any subdirectory or the root. If you want to create your own file make one with a single [table](https://support.microsoft.com/en-us/office/overview-of-excel-tables-7ab0bb7d-3a9e-4b56-a3c9-6c94334e492c) and columns: date, time, squad, name, role, before, today, blocking.
   
3.  Download the flow package from [Releases](https://github.com/zmandel/dailybot/releases) for your language, then import it from Microsoft Power Automate [Import Package](https://learn.microsoft.com/en-us/power-automate/export-import-flow-non-solution#import-a-flow). You may also generate your own "zip" package using the [source](https://github.com/zmandel/dailybot/tree/main/flow) and an optional custom language [translation](https://github.com/zmandel/dailybot/tree/main/translations). During import, it will guide you to create the necessary connections to Teams, Excel online and so on. 
   
4.  Edit the flow and fill-in the numbered steps at the top, following the instructions inside each step.
    - **0 Define Recurrence**: Customize the time-zone, hour to run.
    - **1 Define email to send daily summary**: leave empty for none
    - **2 Define URL of channel to post**: this is your "channel 1" URL. Copy from "Copy Link to Channel" in the Teams Channel to post the daily. Starts with "https<span>://teams.microsoft.com/l/channel/..."
    - **3 Define participating users (tag)**: This is the tag mentioned at the top of these instructions.
    - **4 Define timezone**: Set it based on the examples inside the step.
    - **5 Define language**: Used for certain texts like the weekday name.
    - **6 Define excel channel**:  this is your "channel 2" URL.
    - **7 Define excel file**: pick the same channel as the one in the previous step, and the path to the excel file.
    - Optionally, the "Translations" step allows for customization of all texts:
      <details><summary>Translations customizations</summary>
      - deadlineAlert, obligatoryFieldError, Obligatory, achievedBeforeQuestion, goalsTodayQuestion, placeholderBlocking, blockersQuestion, sendButton: For the "Daily" form sent to each team member.<br>
      - thankyouAfterSend, expiredTimeAlertPre, expiredTimeAlertMiddleLink, expiredTimeAlertPost: For the reply after the user sends the form.<br>
      - achievedBeforeTitle, goalsTodayTitle, blockersTitle: For the post the bot makes for each filled form.<br>
      - replyToUserPre, replyToUserLink, replyToUserPost: For the bot reply to the user, listing their post link and goals for today.<br>
      - nameField: For the name column in the table posted to the channel.<br>
      - prefixNothing: prefix text for detecting single-words in "blockers" that should be ignored, like "none", "ning" (for ninguno/ningun/ninguna in spanish) etc.<br>
       </details>
       
5. Enable the flow.
