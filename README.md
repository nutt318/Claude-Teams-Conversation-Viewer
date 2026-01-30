# Claude Teams Conversation Viewer

A lightweight, offline HTML tool for viewing Claude Teams conversation exports organized by user.

## Overview

This tool allows Claude Teams administrators to merge user data with conversation exports, making it easy to browse conversations by team member. All processing happens locally in your browser — no data is sent anywhere.

## Features

- **View conversations by user** — Select any team member to instantly see all their conversations
- **Load multiple conversation files** — Combine exports from different time periods
- **Search** — Find specific conversations or content within a user's history
- **Export to CSV** — Download a user's conversation summary as a spreadsheet
- **Drag & drop support** — Drag JSON files directly onto the upload zones
- **100% offline** — Works without an internet connection, all data stays on your machine

## Requirements

- A modern web browser (Chrome, Firefox, Edge, Safari)
- Two JSON files from your Claude Teams export:
  - **Users file** — Contains user UUIDs and names
  - **Conversations file(s)** — Contains conversation data with user UUID references

## Installation

1. Download the `claude-teams-viewer.html` file
2. Open it in your web browser (double-click or drag into browser)

That's it — no server, no dependencies, no installation required.

## Usage

### Step 1: Load Your Files

- **Users JSON** — Drag & drop or click to upload your users file
- **Conversations JSON** — Drag & drop or click to upload one or more conversation files

The tool auto-detects the field mappings (UUID, username, etc.)

### Step 2: Click "Load & View"

Once both files are loaded, click the button to process the data.

### Step 3: Browse Conversations

- Click any user in the left sidebar to view their conversations
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
