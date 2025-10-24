# 🗓️ Calendar Agent - AI-Powered Calendar Management

An intelligent calendar assistant built with n8n that uses AI to manage your Google Calendar through natural language conversations.

## 🌟 Features

- 📅 **Create Events** - Schedule meetings and appointments
- 👥 **Add Attendees** - Invite participants to events
- 🔍 **Get Events** - View your calendar schedule
- ❌ **Delete Events** - Remove cancelled appointments
- ✏️ **Update Events** - Modify existing calendar entries
- 🤖 **Natural Language** - Just chat naturally, the AI handles the rest
- ⏰ **Smart Duration** - Automatically sets 1-hour duration if not specified

---

## 🎯 How It Works

Simply chat with the assistant using natural language:
- "Schedule a meeting with john@example.com tomorrow at 2pm"
- "What's on my calendar for next Monday?"
- "Delete my 3pm meeting today"
- "Move tomorrow's meeting to 4pm"
- "Create a team standup every day at 9am"

---

## 🚀 Quick Start

### Prerequisites

- n8n instance (cloud or self-hosted)
- Google Calendar account
- OpenAI API key (or Groq for free alternative)

### Installation

1. **Import the Workflow**
   ```
   - Download the 🤖Calendar Agent.json file
   - In n8n: Import from File → Select the JSON file
   ```

2. **Set Up Credentials**

   **Google Calendar:**
   - Click on any Google Calendar node
   - Add new credential
   - Authenticate with your Google account
   - Accept calendar permissions
   - Update calendar email in all nodes (replace "nateherk88@gmail.com")

   **OpenAI API:**
   - Click "OpenAI Chat Model1" node
   - Add your OpenAI API key
   - Or replace with Groq for free usage (see below)

3. **Activate the Workflow**
   - Toggle "Active" switch at the top
   - Click "Chat" button to start using

---

## 💡 Usage Examples

### Create Solo Event
```
Schedule a dentist appointment tomorrow at 10am
```

```
Create a 30-minute workout session at 6am
```

### Create Event with Attendees
```
Schedule a meeting with sarah@company.com and john@example.com 
tomorrow at 2pm about the project review
```

```
Book a lunch meeting with boss@work.com on Friday at 12pm
```

### View Calendar
```
What's on my calendar today?
```

```
Show me all my meetings next week
```

```
What do I have scheduled for December 15th?
```

### Delete Event
```
Cancel my 3pm meeting today
```

```
Delete the project review meeting on Monday
```

### Update Event
```
Move tomorrow's 2pm meeting to 4pm
```

```
Change my dentist appointment to 11am instead of 10am
```

---

## 🌍 Multi-Language Support

The agent works in **Arabic** and **English**:

```
احجز اجتماع مع ali@example.com غداً الساعة 3 عصراً
```

```
ما هي مواعيدي يوم الأحد؟
```

```
احذف اجتماع الساعة 5 مساءً اليوم
```

---

## 🔧 Configuration

### Chat Interface

The workflow includes a **Chat Trigger** that provides an intuitive interface:
- No coding required
- Conversational interaction
- Message history
- Works on web and mobile

### Customization

#### 1. Change Calendar Email
Replace `nateherk88@gmail.com` with your email in ALL nodes:
- Create Event with Attendee
- Create Event
- Get Events
- Delete Event
- Update Event

#### 2. Customize Agent Behavior
Edit the **Calendar Agent** node system message:

```javascript
System Message:
"You are a calendar assistant for [Your Company Name]. 
Your responsibilities include creating, getting, and deleting 
events in the user's calendar.

Default meeting duration: 30 minutes
Working hours: 9am - 6pm
Time zone: UTC+2"
```

#### 3. Set Default Duration
The agent assumes 1-hour duration if not specified. You can change this in the system message.

---

## 💰 Using Free Alternatives

### Replace OpenAI with Groq (Free)

1. **Get Groq API Key**
   - Sign up at [console.groq.com](https://console.groq.com)
   - Create API Key (free, no credit card)

2. **In n8n:**
   - Delete "OpenAI Chat Model1" node
   - Add "Groq Chat Model" node
   - Connect to "Calendar Agent" node
   - Add Groq credentials
   - Select model: `llama-3.1-70b-versatile`

**Why Groq?**
- ✅ Completely free
- ✅ Faster than OpenAI
- ✅ No credit card required
- ✅ Great Arabic support

---

## 🔐 Security & Privacy

- **Credentials**: Stored securely in n8n
- **Calendar Access**: Limited to actions you authorize
- **AI Processing**: Your calendar data is sent to OpenAI/Groq for processing
- **Best Practice**: Test with a secondary calendar first

---

## 📊 Workflow Structure

```
Chat Trigger
    ↓
Calendar Agent (AI)
    ↓
├─ Create Event
├─ Create Event with Attendee
├─ Get Events
├─ Delete Event
└─ Update Event
    ↓
Success / Error Response
```

---

## 🐛 Troubleshooting

### "Insufficient Quota" Error
**Problem**: OpenAI account has no credits

**Solution**:
- Add credits to OpenAI account, OR
- Switch to Groq (free alternative)

### Google Calendar Authentication Failed
**Problem**: Can't connect to Google Calendar

**Solution**:
- Re-authenticate Google Calendar in credentials
- Ensure calendar permissions are granted
- Check if calendar email matches in all nodes

### Agent Not Responding
**Problem**: Chat doesn't work

**Solution**:
- Ensure workflow is Active
- Check OpenAI/Groq API key is valid
- Verify Chat Trigger webhook is enabled

### Event Not Created
**Problem**: Calendar events not appearing

**Solution**:
- Verify calendar email is correct in nodes
- Check date/time format
- Ensure you have write permissions to the calendar

### "Event Not Found" Error
**Problem**: Can't delete or update events

**Solution**:
- Agent must fetch events first before deleting/updating
- Be specific with event details (date, time, title)
- Check if event exists in the specified time range

---

## 🎨 Advanced Usage

### Integration with Other Workflows

You can call this agent from other workflows using **Execute Workflow** node:

```json
{
  "query": "Schedule team meeting tomorrow at 3pm"
}
```

### Webhook API

Convert to API by replacing Chat Trigger with Webhook:

```bash
POST https://your-n8n.com/webhook/calendar-agent
Content-Type: application/json

{
  "query": "What's on my calendar today?"
}
```

### Scheduled Tasks

Combine with Schedule Trigger for automated calendar management:
- Daily calendar summaries
- Weekly schedule emails
- Auto-cleanup of old events
- Recurring event creation

### Multiple Calendars

To manage multiple calendars:
1. Duplicate the Calendar Agent workflow
2. Change calendar email in each workflow
3. Use different Chat Trigger webhooks
4. Or add calendar selection logic

---

## 📝 Smart Features

### Automatic Duration
If you don't specify duration, the agent assumes 1 hour:
```
"Meeting at 2pm" → 2pm to 3pm
```

### Natural Language Understanding
The agent understands various formats:
- "tomorrow at 3pm"
- "next Monday at 10:30am"
- "December 25th at noon"
- "in 2 hours"

### Event Chaining
The agent intelligently chains actions:
```
"Delete my 2pm meeting and reschedule it for 4pm"
→ First gets events, deletes, then creates new one
```

---

## 🎯 Use Cases

### Personal Assistant
- Schedule personal appointments
- Track family events
- Manage workout schedule
- Plan vacations

### Business Calendar
- Schedule client meetings
- Team coordination
- Project milestones
- Meeting room bookings

### Team Management
- Coordinate team schedules
- Schedule standups
- Track deadlines
- Organize team events

### Event Planning
- Wedding planning
- Conference organization
- Party scheduling
- Course timetables

---

## 🤝 Contributing

Have ideas to improve this workflow?
- Add recurring events support
- Implement reminder notifications
- Add timezone handling
- Integrate with other calendar services

---

## 📄 License

This workflow is provided as-is for educational and commercial use.

---

## 🆘 Support

Need help?
- Check n8n documentation: [docs.n8n.io](https://docs.n8n.io)
- Visit n8n community: [community.n8n.io](https://community.n8n.io)
- Google Calendar API: [developers.google.com/calendar](https://developers.google.com/calendar)
- OpenAI docs: [platform.openai.com/docs](https://platform.openai.com/docs)
- Groq docs: [console.groq.com/docs](https://console.groq.com/docs)

---

## ⚡ Quick Tips

1. **Be Specific**: Include date, time, and duration for best results
2. **Test First**: Try with a test calendar before using your main calendar
3. **Use Natural Language**: The AI understands casual phrasing
4. **Check Before Deleting**: Always verify before deleting important events
5. **Use Groq**: Save money with the free alternative
6. **Update Calendar Email**: Don't forget to change the hardcoded email in all nodes

---

## 📚 Example Commands Cheat Sheet

| Action | Example Command |
|--------|----------------|
| Create | "Schedule lunch at noon tomorrow" |
| With Attendee | "Meeting with john@example.com at 3pm" |
| View | "What's my schedule today?" |
| Delete | "Cancel my 5pm appointment" |
| Update | "Move tomorrow's meeting to 4pm" |
| Range | "Show meetings next week" |
| Specific | "What's on December 1st?" |

---

Made with ❤️ using n8n and AI

**Star this workflow if you find it useful!** ⭐
