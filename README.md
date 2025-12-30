# ShinBot

A Discord bot designed for personal servers that provides dynamic private voice channel creation and management.

## Features

### Dynamic Voice Channel Creation
- **Admin Setup**: Administrators can create a special "Join to create your own channel" voice channel in any category using the `/createvoice` slash command
- **Automatic Private Channels**: When a user joins the designated channel, the bot automatically creates two personalized voice channels:
  - **Private Channel**: A fully private voice channel where only the user has full permissions
  - **Join Channel**: A secondary channel where users can join to be moved into the private channel (viewable by members but speaking restricted)

### Permission Management
- **Private Channel Access**: Only the channel owner has full permissions (view, connect, speak, move members)
- **Member Role Integration**: Other server members with the "Member" role can see the join channel but cannot speak
- **Everyone Role**: @everyone role is denied view access to maintain privacy

### Automatic Cleanup
- **Smart Deletion**: When the channel owner leaves their private channels, both channels are automatically deleted
- **Resource Management**: Prevents channel clutter by removing unused private channels

## Commands

### `/createvoice`
- **Description**: Creates a special voice channel that triggers private channel creation
- **Usage**: `/createvoice category:<category_id>`
- **Permissions**: Administrator only
- **Parameters**: 
  - `category`: The Discord category ID where the voice channel will be created

## Setup

1. **Install Dependencies**:
   ```bash
   npm install
   ```

2. **Environment Variables**:
   Create a `.env` file with:
   ```
   TOKEN=your_discord_bot_token
   CLIENT_ID=your_bot_client_id
   GUILD_ID=your_server_guild_id
   ```

3. **Required Server Roles**:
   - Ensure your server has a "Member" role for proper permission handling
   - The bot requires "Manage Channels" permission

4. **Run the Bot**:
   ```bash
   node index.js
   ```

## How It Works

1. An administrator uses `/createvoice` to set up a trigger channel in a category
2. When any user joins the "Join to create your own channel" voice channel:
   - The bot creates two new private voice channels with the user's name
   - The user is automatically moved to their private channel
   - Both channels have restricted permissions for privacy
3. When the user leaves their private channels, both channels are automatically deleted

## Dependencies

- **discord.js**: v14.16.3 - Discord API wrapper
- **dotenv**: v16.4.7 - Environment variable management

## Requirements

- Node.js runtime environment
- Discord bot application with proper intents (Guilds, Guild Messages, Message Content, Guild Voice States)
- Server administrator permissions for initial setup
