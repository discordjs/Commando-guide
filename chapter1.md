# Getting Started

When you got your first bot up and running with Discord.js, you should've installed Discord.js using npm, Node.js' Package Manager. The same applies to Commando, which must be separately installed. You can do this in one of two ways:

Stable: `npm i -S discord.js-commando`  
Master: `npm i -S gawdl3y/discord.js-commando`

Master is usually preferred due to having more features, but stable is usually less likely to contain bugs.

#### Installing Discord.js Master

Now, you'll later find out that should you install discord.js Stable from npm, at the time of writing, that the help command will give you an error whenever it is used. This is due to a bug in the way messages are split on Stable. To avoid this, I recommend you go ahead and install Discord.js master as well: 

`npm i -S hydrabolt/discord.js`

#### Creating Your index.js File

While it doesn't have to be called `index.js`, the index file is your main file for your bot, which handles everything from registering new commands to logging in your client. It's quite similar to standard Discord.js in many ways, but there are a few extra steps that need to be done to get your bot up and running.

First thing is to require Commando. Contrary to what you may think, you do **not** need to require Discord.js to use Commando. That is, unless you are going to use a RichEmbed, but more on that later.

For now, simple require Commando. We'll also be requiring `path` for use later on. Don't worry, you don't have to install `path`.

```js
const commando = require('discord.js-commando');
const path = require('path');
```

Look familiar? That's just about the same way you required Discord.js in your first bot. The next step is to create a new Commando Client. There's also a few options we are going to set. Some of these are optional, but recommended.

```js
const client = new commando.Client({
    commandPrefix: '<Insert Your Prefix Here>',
    unknownCommandResponse: false,
    owner: '<Insert Your User ID Here>',
    disableEveryone: true
});
```

Looks quite similar to your Discord.js Client doesn't it? Well, aside from all the options and stuff.

In `commandPrefix`, you should insert the prefix you intend to have for your bot. As of writing, you can only have one, so choose wisely! However, note that a mention will **always** be allowed alongside your prefix you set here. In other words, this prefix and mentions are how you will use your bot. **No, there is no way to disable mentions being a prefix!**

The next setting, `unknownCommandResponse`, is basically the bot telling you it could not find that command if the user uses the prefix + an unknown command name. We want to set this to `false` in order to comply with the [Best Bot Practices](https://github.com/meew0/discord-bot-best-practices).

After that is the `owner` field, which should contain the User ID for the owner of the bot. **The user you set here has complete control over the bot, can use eval and other Owner-Only Commands, and ignores command throttling!** So, be sure to only give this to yourself.

The final option, `disableEveryone`, simply prevents the bot from mentioning `@everyone`. This is simply to prevent things from getting annoying. After all, do you want someone mentioning everyone with the bot? Didn't think so.

Next we're going to register the command groups, args types, and default commands, and register the commands in a folder called `commands`. You can name the folder whatever you want, but I personally recommend `commands` , as it... Well, it makes the most sense.

```js
client.registry
    .registerDefaultTypes()
    .registerGroups([
        ['group1', 'Our First Command Group']
    ])
    .registerDefaultGroups()
    .registerDefaultCommands()
    .registerCommandsIn(path.join(__dirname, 'commands'));
```

Remember how I said we'd need path? There you go.

Doing this we've also created our first command group, in the folder `group1` in our `commands` folder. It will be displayed in the help command as 'Our First Command Group'. You can name both of these whatever you like.

Should you want to disable a default command, say, the prefix command, you can pass that in `registerDefaultCommands`.

```js
.registerDefaultCommands({
    prefix: false
})
```

Next, we're going to create a ready event, which is about the same as the one in your first Discord.js Bot.

```js
client.once('ready', () => {
    console.log('Logged in!');
    client.user.setGame('Game');
});
```

This will send `Logged in!` to your console when the bot is ready, and set the Bot's Game to 'Game'. Set that to whatever you wish.

After that, let's add an `unhandledRejection` catcher.

```js
process.on('unhandledRejection', console.error);
```

This is just to catch any Unhandled Promise Rejections so we can get the full error stack for them.

Last but certainly not least, let's log the bot in.

```js
client.login('Your Secret Token');
```

You can also use environment variables or a `config.json` for your token instead of passing it directly.

And there you have it! You've set up your `index.js` file! You should now create the `commands` and `group1` folders, in the end your file structure should look like this, along with whatever `.gitignore` or `config.json` you may have:

```markdown
commands
- group1
index.js
package.json
```

And your `index.js` file should look something like this:

```js
const commando = require('discord.js-commando');
const path = require('path');

const client = new commando.Client({
    commandPrefix: '<Insert Your Prefix Here>',
    unknownCommandResponse: false,
    owner: '<Insert Your User ID Here>',
    disableEveryone: true
});

client.registry
    .registerDefaultTypes()
    .registerGroups([
        ['group1', 'Our First Command Group']
    ])
    .registerDefaultGroups()
    .registerDefaultCommands()
    .registerCommandsIn(path.join(__dirname, 'commands'));
    
client.once('ready', () => {
    console.log('Logged in!');
    client.user.setGame('Game');
});

process.on('unhandledRejection', console.error);

client.login('Your Secret Token');
```

In the next section, we'll create our first command! How exciting! See you then!

