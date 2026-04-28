# CLUTCH — Claude's Live Usage & Team Conversation History

![CLUTCH](images/clutch-dark-tag.jpg)

A lightweight, offline HTML tool for viewing Claude Teams conversation exports organized by user — with daily, weekly, and monthly usage summaries.

## Overview

CLUTCH allows Claude Teams administrators to merge user data with conversation exports, making it easy to browse conversations by team member and track usage trends over time. All processing happens locally in your browser — no data is sent anywhere.

## Features

- **Team overview dashboard** — Instantly see team-wide stats and activity after loading
- **View conversations by user** — Click any team member to see all their conversations
- **Usage summary** — See daily, weekly, and monthly conversation counts per user
- **Projects support** — Load your projects export to see project activity alongside conversations
- **Folder picker** — Select your entire export folder and CLUTCH auto-detects the right files
- **Load multiple conversation files** — Combine exports from different time periods
- **Search** — Find specific conversations or content within a user's history
- **Export to CSV** — Download a user's conversation summary as a spreadsheet
- **100% offline** — Works without an internet connection, all data stays on your machine

## Screenshots

![CLUTCH Dark](images/clutch-dark-notag.jpg)

![CLUTCH Light](images/clutch-light-tag.jpg)

## Requirements

- A modern web browser (Chrome, Firefox, Edge, Safari)
- **Organisation admin access** — Only the original org admin can export data from Claude Teams. You must be the admin of the Claude Teams organisation to generate the export files used by this tool.
- JSON files from your Claude Teams export:
  - **Users file** — Contains user UUIDs and names
  - **Conversations file(s)** — Contains conversation data with user UUID references
  - **Projects file** *(optional)* — Contains project data associated with your organisation

## Installation

1. Download the `clutch.html` file
2. Open it in your web browser (double-click or drag into browser)

That's it — no server, no dependencies, no installation required.

## Getting Your Export Files

1. Log in to [claude.ai](https://claude.ai) as an **organisation admin**
2. Navigate to **Settings → Organisation → Export data**
3. Download and extract the export — you'll get a folder containing JSON files including `users.json`, `conversations.json`, and `projects.json`
4. In CLUTCH, click **"Select Export Folder"** and point it at the extracted folder — files are auto-detected automatically

## Usage

### Step 1: Load Your Files

- **Users JSON** — Drag & drop or click to upload your users file
- **Conversations JSON** — Drag & drop or click to upload one or more conversation files

The tool auto-detects the field mappings (UUID, username, etc.)

### Step 2: Click "Load & View"

Once both files are loaded, click the button to process the data.

### Step 3: Browse Conversations

- Click any user in the left sidebar to view their conversations
- Switch between **Conversations** and **Usage Summary** tabs to see activity trends
- Use the search box to filter conversations
- Click a conversation to expand and read the messages
- Use "Export CSV" to download the selected user's conversation list

### Adding More Conversations

Click "+ Add More Conversations" in the sidebar to load additional conversation files at any time. The new data merges automatically.

### Starting Over

Click "Start Over" to clear all data and load new files.

## Expected File Formats

### Users JSON

```json
[
  {
    "uuid": "abc123-...",
    "full_name": "John Smith"
  },
  {
    "uuid": "def456-...",
    "full_name": "Jane Doe"
  }
]
```

The tool looks for common field names: `uuid`, `id`, `user_id` for the identifier, and `full_name`, `name`, `username`, `email` for the display name.

### Conversations JSON

```json
[
  {
    "uuid": "conv-123...",
    "name": "Conversation Title",
    "created_at": "2025-01-15T10:30:00Z",
    "account": {
      "uuid": "abc123-..."
    },
    "chat_messages": [
      {
        "uuid": "msg-1",
        "text": "Hello!",
        "sender": "human",
        "created_at": "2025-01-15T10:30:00Z"
      },
      {
        "uuid": "msg-2",
        "text": "Hi! How can I help?",
        "sender": "assistant",
        "created_at": "2025-01-15T10:30:05Z"
      }
    ]
  }
]
```

The tool links conversations to users via the `account.uuid` field (or similar).

## Privacy & Security

- **All processing is local** — Your data never leaves your computer
- **No external requests** — The tool works completely offline
- **No data storage** — Nothing is saved; refresh the page to clear everything

## Troubleshooting

### "Could not auto-detect field mappings"

Your file structure may differ from expected. Check that your users file has identifiable UUID and name fields, and that conversations have a user reference field.

### Users showing 0 conversations

The UUID field in your conversations may not match the UUID field in your users file. Verify that the user UUIDs correspond between the two files.

### Large files loading slowly

The tool handles large files but limits the display to 100 conversations at a time for performance. Use the search feature to find specific conversations.

## License

MIT License — Free to use and modify.
