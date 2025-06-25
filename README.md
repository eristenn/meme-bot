# 🤖 Discord Meme Bot

This project is a lightweight Python-based Discord bot that listens for a user command (`$meme`) and responds by fetching and posting a random meme from Reddit. It was designed to demonstrate understanding of API integration, asynchronous event-driven programming, and bot deployment in the Discord ecosystem.

---

## 🛠️ What I Built

The bot was implemented using the `discord.py` library, which wraps the Discord API for Python developers. The bot listens for specific message events in a Discord server and responds to the `$meme` keyword with a meme image retrieved from an external API.

Key components I implemented:

- **Bot Registration & Configuration**: I created and configured the bot through the Discord Developer Portal. This included enabling privileged intents (e.g., message content access), generating an OAuth2 invite link with the appropriate permissions, and securely managing the bot token.
  
- **Message Event Handling**: Using the `discord.Client` class, I overrode the `on_message` asynchronous method to detect incoming user messages. The bot intelligently ignores messages it sends itself to prevent infinite response loops.
  
- **External API Integration**: I integrated with the [Meme API](https://github.com/D3vd/Meme_Api), a public JSON-based API that returns meme content from Reddit. I used the `requests` library to retrieve meme data and parse the response using Python's built-in `json` module.

- **Security Considerations**: Bot tokens were handled securely and not hard-coded in production scenarios. This implementation version includes a placeholder and comments on how to safely manage credentials using environment variables or a `.env` file.

---

## 💡 Technologies Used

- **Python 3** — Main programming language
- **discord.py** — Python wrapper for the Discord API
- **requests** — For HTTP communication with the Meme API
- **JSON Parsing** — To handle structured API responses

---

## ⚙️ How It Works

- When the bot is running and connected to a Discord server, it listens for incoming messages.
- If a user sends a message that starts with `$meme`, the bot sends a GET request to the Meme API.
- The bot extracts the meme image URL from the JSON response and posts it back into the same Discord channel.
- The bot ignores its own messages and handles asynchronous communication using `async`/`await` to avoid blocking.

---

## 📌 Code Snippet (Core Logic)

```python
async def on_message(self, message):
    if message.author == self.user:
        return
    if message.content.startswith('$meme'):
        await message.channel.send(get_meme())
