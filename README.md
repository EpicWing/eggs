# EpicWing Eggs

Ready-to-use eggs (server templates) for [EpicWing](https://github.com/EpicWing/epicwing-panel) and other panels that use the Pterodactyl egg format (PTDL_v2).

## Eggs

| Egg | File | What it does |
|---|---|---|
| Discord Bot Python | [`eggs/egg-discord-bot-python.json`](eggs/egg-discord-bot-python.json) | Runs any Discord bot written in Python (3.11, 3.12 or 3.13) |
| Discord Bot Node.js | [`eggs/egg-discord-bot-nodejs.json`](eggs/egg-discord-bot-nodejs.json) | Runs any Discord bot written in JavaScript (Node.js 20, 22 or 24) |

Both eggs are generic. Nothing in them is tied to one bot: you bring your own code and choose everything yourself.

## Import

1. Download the egg file you need.
2. Open the admin area of your panel and import the file (in Pterodactyl: Admin > Nests > Import Egg).
3. Create a server from the new egg.

## Run your bot

**With git:** enter the repository URL and, if you want, a branch. For private repositories over HTTPS, also enter a username and an access token. The repository is cloned during the installation, but only if the server folder is empty.

**Without git:** leave the repository empty and upload your files with the file manager.

| Variable | Description |
|---|---|
| `GIT_ADDRESS` | Repository URL. Leave empty to upload your own files. |
| `BRANCH` | Branch to clone. Empty means the default branch. |
| `GIT_USERNAME` / `GIT_ACCESS_TOKEN` | Only for private repositories over HTTPS. |
| `AUTO_UPDATE` | Run `git pull` before every start (needs a git repository). |
| `MAIN_FILE` | The file that starts your bot. |
| `REQUIREMENTS_FILE` | Python only: pip requirements file, installed on every start if it exists. |
| `EXTRA_PACKAGES` | Optional list of extra pip or npm packages, separated by spaces. |
| `START_ARGS` | Optional arguments added to the start command. |
| `DISCORD_TOKEN` | Optional. Passed to your bot as an environment variable. |

Your bot can read its token from the `DISCORD_TOKEN` environment variable or from a `.env` file in the server folder.

On every start the Python egg installs the extra packages and the requirements file with `pip install --user`. The Node.js egg installs the extra packages and runs `npm install` if a `package.json` exists.

## Good to know

- With a token, the clone URL (and so the token) is stored in the git config inside the server folder. Use a read-only token.
- The eggs use the images from [`ghcr.io/ptero-eggs/yolks`](https://github.com/ptero-eggs/yolks). Pterodactyl lets you choose the version, EpicWing uses the first image in the list.

## Compatibility

The eggs import cleanly into EpicWing. They use the standard Pterodactyl egg format (PTDL_v2), so they should also work in Pterodactyl and compatible panels. If something does not work in your panel, please open an issue.

## Support

- Discord: https://discord.gg/tc7xtNPsmh
- Email: support@epicwing.de or info@epicwing.de
- Questions and ideas: [Discussions](https://github.com/EpicWing/eggs/discussions)
- Bugs: [open an issue](https://github.com/EpicWing/eggs/issues/new/choose)

## Contributing

Issues and pull requests are welcome. New eggs go into the `eggs` folder. Please write names, descriptions and comments in English.

## License

[MIT](LICENSE). The Docker images come from the ptero-eggs project and have their own terms.
