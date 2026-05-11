
**Prompt:**

> You are given a Google Meet transcript. Extract all action items and format them as a "Due Outs" list for Slack using this structure:
> 
> **Due Outs:**
> 
> - @Name to [action]
> 
> Rules:
> 
> - One bullet per action item
> - Start each with the assigned person's @name
> - Use active, concise language ("to send…", "to follow up…", "to review…")
> - Group multiple items per person as separate bullets
> - If no owner is clear, flag it as **[UNASSIGNED]**
> 
> Transcript: [PASTE HERE]