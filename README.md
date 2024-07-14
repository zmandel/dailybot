### Daily "Scrum" Bot for Microsoft Teams

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
