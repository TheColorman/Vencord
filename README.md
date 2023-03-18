# Vencord x Acrylic - Colorman fork

Super scuffed fork of Vencord that allows Acrylic to be installed alongside it. (Also compatible with OpenAsar).  
It only works for Windows, and not even sure about Windows 11.  
I also add plugins that haven't been merged on the main Vencord repo.

Vencord source: https://github.com/Vendicated/Vencord  
Acrylic source: https://github.com/uwu/Acrylic

Note that I've changed some of the CSS in `Acrylic/theme.css` to make it less transparent. My CSS starts is everything from `/* Custom */` to `/* End of custom */`, so feel free to play around with it to get it to your liking.

# Installation (Vencord)

The Vencord part of this is just copied from https://github.com/Vendicated/Vencord/blob/main/docs/1_INSTALLING.md.

## Dependencies

-   Install Git from https://git-scm.com/download
-   Install Node.JS LTS from here: https://nodejs.dev/en/

## Installing Vencord

> ❗ If this doesn't work, see [Manually Installing Vencord](#manually-installing-vencord)

Install `pnpm`:

> ❗ This next command may need to be run as admin/sudo depending on your system, and you may need to close and reopen your terminal for pnpm to be in your PATH.

```shell
npm i -g pnpm
```

> ❗ **IMPORTANT** Make sure you aren't using an admin/root terminal from here onwards. It **will** mess up your Discord/Vencord instance and you **will** most likely have to reinstall.

Clone TheColorman/Vencord:

```shell
git clone https://github.com/TheColorman/Vencord
cd Vencord
```

Install dependencies:

```shell
pnpm install --frozen-lockfile
```

Build Vencord:

```shell
pnpm build
```

Inject vencord into your client:

```shell
pnpm inject
```

Then fully close Discord from your taskbar or task manager, and restart it. Vencord should be injected - you can check this by looking for the Vencord section in Discord settings.

# Installation (Acrylic)

Okay, from here on it's time to get Acrylic to work.  
First, you want to change the path on the final line of the `Acrylic/main.js` file:

```js
//! Replace this with the path to your Vencord folder.
require("W:\\Projects\\Vencord\\dist\\patcher.js");
```

Just replace the "`W:\\Projects\\Vencord`" part with wherever you cloned this repository.  
Now navigate to `C:\Users\[username]\AppData\Local\Discord\app-[newest version]\resources` (or wherever you've installed Discord). Replace `Discord` with `DiscordPTB` or `DiscordCanary` as needed.  
In there you should see a file ending in `.asar`. Make a copy of that, and rename it to `original.asar`.  
Then create an `app/` folder if there isn't one already.  
Now copy everything from the `Acrylic/` folder in this repo into the `app.asar/` and `app/` folders (yes, both). Click Yes when it asks if you want to replace files.

Finally, you need to open up the `dist/patcher.js` file. Then replace all the places where it mentions an asar file with `original.asar`. For example, it might say "`_app.asar`", or "`app.asar`". Replace that with "`original.asar`".

# Updating Vencord

Start by pulling the latest changes to the repo:

```shell
git pull
```

If it fails you probably have some changes, just stash them and reapply them after pulling.

Once you've pulled, run the steps from [Installing Vencord](#installing-vencord) again. If it fails to inject, remove the app.asar folder in the Discord `resources` directory (see [Installation (Acrylic)](#installation-acrylic)).  
Once it has patched successfully, you need to redo the steps in [Installation (Acrylic)](#installation-acrylic).
