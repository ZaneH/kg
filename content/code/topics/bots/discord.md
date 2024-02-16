---
title: Discord Bots
tags: discord, bots, python, javascript
---

## Welcome!

After building a few bots now, I thought I could dedicate a page to the topic.
Discord's API has gone through rapid iteration over the last 10 years, and
currently we're on API version 14. This page aims to be timeless, but who knows.

## Getting Started

There are three compelling libraries for building Discord bots (in my opinion):

1. [Pycord](https://github.com/Pycord-Development/pycord) - Pycord, a maintained fork of discord.py.
2. [Nostrum](https://github.com/Kraigie/nostrum) - Elixir Discord Library.
3. [discord.js](https://discord.js.org) - Discord.js, a JavaScript library. Most popular.

I've ranked them according to my own personal preferences. `discord.js` gets
-10 points for expecting you to be okay without type hints. `Pycord` gets +10
points for their easy-to-use decorators. `Nostrum` gets +5 points for being Elixir.

Getting started is nice and simple, here's the high-level steps for creating
a bot:

1. Create the project folder, install the library of your choosing.
2. Create an "Application" on the [Discord Developer Portal](https://discord.com/developers/applications).
3. Copy the bot token and paste it into your code (preferably as an environment variable).
4. Create a bot URL using the "URL Generator" from the sidebar.
    a. Check the 'bot' scope.
    b. You'll typically want 'Send Messages' and 'Read Message History' permissions at *least*.
5. Paste the bot URL into your browser and add the bot to your server.
6. Optionally, include the bot URL in your `README.md` file.

Once all this is done, you can start writing your bot code. Here's a simple example
that uses Pycord:

```python
import os
import discord
from discord.ext import commands
from dotenv import load_dotenv


class MyBot(discord.Bot):
    def __init__(self):
        super().__init__(intents=discord.Intents.default())

    async def on_ready(self):
        print(f'Logged in as {self.user}!')
        await self.sync_commands()


bot = MyBot()


@bot.slash_command(name='greet', description='Greet someone')
async def greet(ctx: commands.Context, user: discord.User):
    return await ctx.respond(f'Hello, <@{user.id}>!')

load_dotenv()
bot.run(os.getenv('DISCORD_TOKEN'))
```

## Gotchas & Quirks

- Modals can only contain text input fields (no user select menus, etc.)
- You need to define your intents when you create your bot. This is a new feature.
    - Typically `intents` are defined as `intents = discord.Intents.default()`

## Secret Message Formats

Send these into a Discord chat to see the magic happen.

- [Clickable slash commands](https://stackoverflow.com/a/73744289/3411191) - Displays an inline slash command users can click.
- Countdowns and dates
    - `<t:1708061519:R>` for example, will display the date in relative time.
    - Use web apps like [shyked.fr](https://discord-date.shyked.fr/) to generate these more easily.
- Mention a user by their ID: `<@1234567890>`