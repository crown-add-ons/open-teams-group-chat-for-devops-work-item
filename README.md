# Open Teams Group Chat for DevOps Work Item

## Request Access

**This extension is currently invite-only.** To request access for your organization:

� **[Request Access Here](../../issues/new?template=access-request.md)**

## Support & Issues

- **[Report a Bug](../../issues/new?template=bug-report.md)** - Found an issue?
- **[Feature Request](../../issues/new?template=feature-request.md)** - Suggest improvements
- **[Get Help](../../issues/new?template=support-request.md)** - Need assistance?

## About

When installed, this extension gives [Azure DevOps](https://dev.azure.com) Board users a button to open a Teams Group Chat for the active work item.

**After installation, you need to create ONE custom field**: `Related Chat Id` (Text field) - see the setup instructions below for step-by-step details.

1. First click: Opens a new group chat for all of the people on the item.
2. Subsequent clicks:
   - Is the clicker already a member of the group chat? It opens the group chat.
   - Is the clicker not a member of the group chat? It opens a new chat and requests that somebody in that existing chat add the user to that chat.

## Why Use This Extension?

Group chats facilitate easy collaboration, and this extension's button facilitates group chats!

Clicking the button opens or reopens a Teams Group Chat for easy collaboration with a work item's stakeholders.

| Email | Teams Group Chat (via this extension) | Work Item Discussion |
|-------|---------------------------------------|---------------------|
| Emails often have too many or too few people involved. Want out of Reply Alls? Too bad, you're stuck. | If you're on the work item, you're added to the initial group automatically. Others can easily be added manually. Don't want to be in the group? You can choose to leave it! (or mute it) | Stakeholders may miss the conversation if they aren't used to being in DevOps. (Also, email notifications about DevOps discussions can be painful to manage.) |
| Folders, tagging, deleting, salutations, closings, big signatures (with pictures!).... Yuck! Also, there is an awkward bottom-up sorting of previous messages. | No time and space is wasted on that email stuff. Plus, a natural sorting order. (You can read messages top to bottom, oldest to newest.) | Awkward sorting. Want to read the messages in order? Too bad. Your eyes will constantly have to scan up two messages, then read down one. |
| It is easy to get off topic in email. It is too easy for emails to span many different topics and many levels of detail. | One chat per work item makes it easier to keep people on topic. It's also easier to keep the chats at the right level of detail. | |
| Overlapping threads when two people reply at the same time or don't reply to the most recent message. Yuck! | Chat participants all receive messages at the same time. If you want to bring somebody new into the conversation, its pretty easy for that person to scroll back just a little and get the context for what is going on. | |

Leave email and hidden discussions behind! Engage stakeholders even if they don't use Azure DevOps!

## Setup Instructions

### Prerequisites

- Organization Administrator or Process Administrator permissions
- Access to Azure DevOps Organization Settings

### Step 1: Create Required Custom Field

1. **Go to Organization Settings** → **Boards** → **Process**
2. **Select your process** (e.g., "Agile", "Scrum", "Basic")
3. **Choose work item type** (e.g., "User Story", "Bug", "Feature")
4. **Go to Fields tab** → Click **"+ New field"**
5. **Configure the field**:
   - **Name**: `Related Chat Id`
   - **Type**: Text (single line)
   - **Required**: No (leave unchecked)
6. **Click "Add field"**

### Step 2: Add Extension to Work Item Layout

1. **Go to Layout tab** for the a work item type
2. **Add the control** → **"+ Add a control"** → **"Custom control"**
3. **Select**: "Open Teams Group Chat"
4. **Configuration**: Choose the "Related Chat Id" field you created
5. **Click "OK"**

### Step 3: Test

- Go to any work item → You'll see the "Open Teams Chat" buttons
- Click to create and open Teams group chats!

## Required Permissions

This extension requests the following Azure DevOps permissions:

- **`vso.work`** (Work Items - Read & Write)
  - **Why needed**: To read work item details (title, assigned users) and save the Teams chat ID
  - **What it does**: Reads identity fields, saves chat ID to your custom field

- **`vso.identity`** (Identity - Read)
  - **Why needed**: To get the references to users on a work item
  - **What it does**: Adds those users to a Teams group chat

**Important**: This extension also requires users to authenticate with Microsoft Teams (via Microsoft Graph API) to create/access chats. Users will see a login prompt on first use.

The extension does not send receive or send any data outside of your Azure DevOps organization and your Microsoft Teams installation.

## Microsoft Teams Integration

The extension integrates with Microsoft Teams through the Microsoft Graph API:

- **Chat.ReadWrite** permission in Teams
- **Creates group chats** with work item stakeholders
- **Saves chat links** back to Azure DevOps for easy reopening
- **Handles access control** - creates new chats if users can't access existing ones
