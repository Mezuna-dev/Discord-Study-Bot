# Discord Study Bot
 
A Discord bot for tracking study sessions, managing assignments, and competing with friends on a leaderboard. The bot automatically logs time spent in voice channels and supports manual task tracking via slash commands.
 
## Features
 
- **Voice Channel Tracking** - Automatically records time spent in voice channels
- **Task Tracking** - Manually start and stop named study tasks
- **Assignment Management** - Add, list, complete, and clear assignments with due dates
- **Personal Stats** - View your total voice and task study time
- **Leaderboard** - See the top 10 studiers in your server
 
## Architecture
 
The project uses a two-process architecture:
 
- **Bot** (`bot/main.py`) - Discord.py bot that listens to Discord events and slash commands
- **API** (`api/api.py`) - FastAPI backend that handles business logic and database operations
- **Database** (`database/`) - SQLAlchemy ORM backed by SQLite
 
The bot communicates with the API over HTTP (`http://localhost:8000`).
 
## Requirements
 
- Python 3.8+
- A Discord bot token
 
## Installation
 
1. Clone the repository:
   ```bash
   git clone https://github.com/Mezuna-dev/Discord-Study-Bot.git
   cd Discord-Study-Bot
   ```
 
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
 
3. Create a `.env` file in the project root:
   ```
   DISCORD_BOT_TOKEN=your_token_here
   ```
 
## Running
 
The API and bot must run as separate processes. Start the API first:
 
```bash
python api/api.py
```
 
Then, in a separate terminal, start the bot:
 
```bash
python bot/main.py
```
 
## Commands
 
### Task Tracking
 
| Command | Description |
|---|---|
| `/starttask <name>` | Start tracking a named study task |
| `/stoptask` | Stop the current task and log its duration |
| `/mystats` | View your total task and voice channel study time |
 
### Assignments
 
| Command | Description |
|---|---|
| `/addassignment <title> <due_date> [description]` | Add an assignment (due date format: `YYYY-MM-DD`) |
| `/assignments` | List all your assignments |
| `/completeassignment <assignment_id>` | Mark an assignment as completed |
| `/clearassignments` | Delete all your assignments |
 
### Server
 
| Command | Description |
|---|---|
| `/leaderboard` | Show the top 10 users by total study time |
| `/ping` | Check that the bot is responsive |
 
## Database Schema
 
The SQLite database (`discord_bot.db`) is created automatically on first run with the following tables:
 
- **Guild** - Discord servers using the bot
- **User** - Discord users tracked per guild
- **VoiceSession** - Voice channel join/leave events with duration
- **UserEvent** - Manual task start/stop events with duration
- **Assignment** - User assignments with due dates and completion status
 
## Configuration
 
| Variable | Description |
|---|---|
| `DISCORD_BOT_TOKEN` | Your Discord bot token (required, set in `.env`) |
 
The API base URL defaults to `http://localhost:8000` and is configured in `bot/main.py`.
 
## Required Bot Permissions & Intents
 
Enable the following in the [Discord Developer Portal](https://discord.com/developers/applications):
 
**Privileged Gateway Intents:**
- Server Members Intent
- Message Content Intent
- Voice States (required for voice channel tracking)
 
**Bot Permissions:**
- Send Messages
- Use Application Commands
