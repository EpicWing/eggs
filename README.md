# EpicWing Eggs

Run your own Discord bot on [EpicWing](https://github.com/EpicWing/epicwing-panel), Pterodactyl or any panel that imports Pterodactyl eggs. Pick the egg for your language, import it once and start your bot. No Dockerfile or setup scripts needed.

## Quick start

### 1. Pick your egg

| Your bot is written in | Download this file |
|---|---|
| Python (discord.py, py-cord, nextcord, ...) | [egg-discord-bot-python.json](https://github.com/EpicWing/eggs/releases/latest/download/egg-discord-bot-python.json) |
| JavaScript (discord.js, ...) | [egg-discord-bot-nodejs.json](https://github.com/EpicWing/eggs/releases/latest/download/egg-discord-bot-nodejs.json) |

Not sure? Look at the file that starts your bot: `.py` means Python, `.js` means Node.js. You only need one of the two files. If the link opens the file in your browser, right-click it and choose "Save link as".

### 2. Import it into your panel (once)

- **EpicWing:** open the admin area, go to the eggs and import the file.
- **Pterodactyl:** Admin > Nests > Import Egg, then choose the nest and the file.

### 3. Create a server from the egg

Create a new server and choose the new egg. Then fill in the form:

| Where is your bot code? | What to do |
|---|---|
| On GitHub or another git host | Enter the URL in **Git repository**. Set **Main file** to the file that starts your bot. |
| On your computer | Leave **Git repository** empty. After the server is created, upload your files with the file manager and set **Main file**. |

### 4. Add your bot token

Enter your token in the **Discord token** field. You can create it in the [Discord Developer Portal](https://discord.com/developers/applications) under your application > Bot. Never share your token with anyone.

Your bot reads it from the environment variable `DISCORD_TOKEN`. If you prefer, you can also put it into a `.env` file in the server folder.

### 5. Start the server

The console shows what your bot prints. Your bot should appear online in Discord after a few seconds.

**Example: a Python bot from GitHub**

| Field | Value |
|---|---|
| Git repository | `https://github.com/you/my-bot` |
| Main file | `bot.py` |
| Discord token | your token |

## What the eggs do

Both eggs are generic. Nothing in them is tied to one bot: you bring your own code and choose everything yourself.

- **Python egg** (Python 3.11, 3.12 or 3.13): on every start it installs the extra packages and the requirements file with `pip install --user`, then runs your main file.
- **Node.js egg** (Node.js 20, 22 or 24): on every start it installs the extra packages, runs `npm install` if a `package.json` exists, then runs your main file.

## All settings

| Setting | Description |
|---|---|
| Git repository (`GIT_ADDRESS`) | Repository URL. Leave empty to upload your own files. |
| Git branch (`BRANCH`) | Branch to clone. Empty means the default branch. |
| Git username / access token | Only for private repositories over HTTPS. |
| Update on start (`AUTO_UPDATE`) | Run `git pull` before every start (needs a git repository). |
| Main file (`MAIN_FILE`) | The file that starts your bot. |
| Requirements file (`REQUIREMENTS_FILE`) | Python only. Installed on every start if the file exists. |
| Extra packages (`EXTRA_PACKAGES`) | Optional list of extra pip or npm packages, separated by spaces. |
| Start arguments (`START_ARGS`) | Optional arguments added to the start command. |
| Discord token (`DISCORD_TOKEN`) | Optional. Passed to your bot as an environment variable. |

## Troubleshooting

| What you see in the console | What to do |
|---|---|
| `ModuleNotFoundError: No module named 'x'` | Add `x` to your requirements file, or enter it in **Extra packages**. |
| `Cannot find module 'x'` | Make sure `x` is listed in your `package.json`, or enter it in **Extra packages**. |
| File not found for your main file | Check the **Main file** setting. The path is relative to the server folder. |
| Login or "Improper token" error | Check the token in the **Discord token** field. A reset token in the Developer Portal is a new token. |
| Error about privileged or disallowed intents | Enable the intents your bot uses in the Developer Portal under Bot. |
| The repository was not cloned | The repository is only cloned if the server folder is empty. Delete the files and reinstall the server. |

## Good to know

- When you clone a private repository with a token, the token is stored in the git config inside the server folder. Use a read-only token.
- The eggs use the images from [`ghcr.io/ptero-eggs/yolks`](https://github.com/ptero-eggs/yolks). Pterodactyl lets you choose the version, EpicWing uses the first image in the list (Python 3.13 or Node.js 24).

## Compatibility

The eggs import cleanly into EpicWing. They use the standard Pterodactyl egg format (PTDL_v2), so they should also work in Pterodactyl and compatible panels. If something does not work in your panel, please open an issue.

## Support

- Discord: https://discord.gg/tc7xtNPsmh
- Email: support@epicwing.de or info@epicwing.de
- Questions and ideas: [Discussions](https://github.com/EpicWing/eggs/discussions)
- Bugs: [open an issue](https://github.com/EpicWing/eggs/issues/new/choose)

## Contributing

Issues and pull requests are welcome. New eggs go into the `eggs` folder. Please read [CONTRIBUTING.md](CONTRIBUTING.md) first and write names, descriptions and comments in English.

## License

[MIT](LICENSE). The Docker images come from the ptero-eggs project and have their own terms.
