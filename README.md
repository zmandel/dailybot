# Daily "Scrum" Bot for Microsoft Teams
Microsoft Power Automate flow for compiling team Dailys.

Get the team ready by compiling the data before each daily.

The bot asks each team member every work morning for their daily, giving a 1.5 hour deadline to fill.
Once all fill it (or time expires) it is consolidated and shared with the team, timed a few minutes before the synchronous Daily.

<table style="border-collapse: collapse; width: 100%;">
  <tr>
    <td><img src="https://github.com/user-attachments/assets/33c971fb-091c-4dba-b0bf-8fa511ec5413" alt="Teams Form" style="width:350px;"/></td>
    <td style="text-align: center;">⇉<br>⇉<br>⇉</td>
    <td ><img src="https://github.com/user-attachments/assets/3c2f2da6-3ef4-4e23-a698-07afcba8a50a" alt="Teams Table" style="width:550px;"/></td>
  </tr>
</table>


## Features

- [x] **Automated Check-ins**: Each morning, the bot sends a chat form to team members to gather their daily status. The form, which includes a set deadline, prompts responses on:
  - Achievements from the previous day.
  - Objectives for the current day.
  - Any blockers or urgent alerts.

- [x] **Real-Time Updates**: After submitting, the bot immediately posts each team member's response to a designated channel.

- [x] **Daily Summary Compilation**: After gathering all responses or reaching the set deadline, the bot aggregates the data into a table and posts it in the channel.

- [x] **Email Distribution**: The compiled table is then automatically emailed to relevant stakeholders.

- [x] **Historical Tracking**: All responses are preserved in an Excel table, facilitating historical analysis.

- [x] **Simple Setup**: The bot is designed for easy installation. Configurable fields like the Team, Channel, Hour to send etc. are numbered steps placed at the beginning of the workflow.

- [x] **Multilingual Support**: Ready-to-use translations are available in both English and Spanish. All language-specific texts are centralized in a single JSON step.

- [x] **Ready for genAI analysis**: The historical data in the Excel table contains columns to enable AI data analisis. Included below is a sample genAI prompt that generates a surprisingly rich and accurate status report with an analysis per user, per role, and the team as a whole.

- [x] **Aditional features**:
   - The first user to send the daily is rewarded with a crown 👑. Use it to give recognition and foment an early form submission.
   - Once the user sends the form response, their "goals for today" are sent to their chat along with a link to their response posted.
   - The "role" of each user is queried from the "Office365 user directory" and included in the excel table to help genAI analysis.
   - The "Blockers" field ignores single-words like "none", based on "translations.prefixNothing" to keep that column clean in the consolidated reports.

## Installation
From [Releases](https://github.com/zmandel/dailybot/releases/), download the package for your language, then install it from Microsoft Power Automate "Import Package". You may also generate your own "zip" package using the source and your custom language translation (see the [translations](https://github.com/zmandel/dailybot/tree/main/translations) directory).

## Technical details
  - The Daily form is inlined in the chat by using "Adaptive Cards" for Teams.
  - The form is sent to each user in parallel by using Power Automate´s "Concurrency control" feature in the "for-each" loop, and with a set deadline.
  - To handle parallelism inside that loop, only "compose" actions are used as local "write" variables (except "orderedUsers" but in a safe way)
  - The "Define language" step is used for the names of the week days.
 
## Generate a project status report with genAI
This prompt works great with [Google Gemini Pro 1.5](https://aistudio.google.com/app/prompts/new_chat) to generate a status report with an analysis per user, per role, and the team as as a whole. Place it in the "system prompt", use a very low or zero Temperature and attach the excel file to the first user message:

```
**Task**: As an expert project manager, your role is to synthesize a team progress report from daily scrum entries presented in an Excel table.

**Input Data**: The provided Excel table consists of daily scrum reports from each team member. The table is structured with the following columns:

- date: The date of the report.
- time: The time when the report was recorded.
- squad: The name of the team (its always the same in this case).
- name: The name of the reporting team member.
- role: The role of the team member within the team.
- before: Achievements from the previous day as reported by the team member (the day before this row´s "date").
- today: Goals set for the current day by the team member (the day of this row´s "date").
- blocking: Current impediments reported that might affect the day's tasks (the day of this row´s "date").

**Steps**:
Read the Table: Start by sequentially reading each row of the table from top to bottom. Treat the scrum entries as parts of a continuous narrative. Note key events and milestones.
Tracking Consistency: For each team member, track how tasks listed under "today" in one report are addressed in the "before" section of subsequent reports. This will assess the planning consistency and follow-through of each individual.
Identify Blockers: Pay special attention to the "blocking" column to identify any recurring or significant obstacles that could impact team progress.

**Expected Outcome**:
Generate a comprehensive progress report with these sections:
 - Overall Team Observations
 - Key Events & Milestones (past, current and future)
 - Team Member Performance (for each member "name")
 - Role Member Performance (for each "role") based on your team member performance report.
 - Areas of improvements (at member, role and team levels)

```
