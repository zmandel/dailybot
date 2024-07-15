### Daily "Scrum" Bot for Microsoft Teams
Microsoft Power Automate flow for compiling team Dailys.
Get the team ready for the daily by compiling the data before each daily.

The bot asks each team member every work morning for their daily, giving a 1.5 hour deadline to fill.
Once all fill it (or time expires) it is consolidated and shared with the team.

**Features:**

- **Automated Check-ins**: Each morning, the bot sends a chat form to team members to gather their daily status. The form, which includes a set deadline, prompts responses on:
  - Achievements from the previous day.
  - Objectives for the current day.
  - Any blockers or urgent alerts.

- **Real-Time Updates**: After submitting, the bot immediately posts each team member's response to a designated channel.

- **Daily Summary Compilation**: After gathering all responses or reaching the set deadline, the bot aggregates the data into a table and posts it in the channel.

- **Email Distribution**: The compiled table is then automatically emailed to relevant stakeholders.

- **Historical Tracking**: All responses are preserved in an Excel table, facilitating historical analysis.

- **Simple Setup**: The bot is designed for easy installation. Configurable fields like the Team, Channel, Hour to send etc. are numbered steps placed at the beginning of the workflow.

- **Multilingual Support**:
  - All language-specific texts are centralized in a single JSON file for straightforward localization.
  - Ready-to-use translations are available in both English and Spanish.

- **Ready for AI analysis**: The historical data in the Excel table contains columns to enable data analisis with GenAI with these columns:
  - date, time, squad, name.
  - role: from the office365 user directory.
  - before, today: achieved yesterday, today.
  - blocking: blocking issues or alerts.

Download the package zip from "Releases".

**This genAI prompt** works great with [Google Gemini Pro 1.5](https://aistudio.google.com/app/prompts/new_chat). Place it in the "system prompt" and attach the excel file to the first user message:

---
**Task**: As an expert program manager, your role is to synthesize a team progress report from daily scrum entries presented in an Excel table.

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
 - Key Events & Milestones
 - Team Member Performance (for each member "name")
 - Role Member Performance (for each "role") based on your team member performance report.
 - Areas of improvements

---
