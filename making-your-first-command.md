# Making Your First Command

So now that we've set up a command group and registered our command folder, we're ready to make our first command file! First, you're going to need to, of course, create a new file for the command. Hop over to your `commands` folder, and then your `group1` folder, and make a new file called `reply.js`. This is going to be a simple command that only replies with a message when used. We'll go into arguments and all that later.

Once you have your file, let's get started!

#### Creating Your Command Class

Before you do anything, at the start of your file, you're going to need to require commando again.

```js
const commando = require('discord.js-commando');
```

This will allow our command to... Well, exist.

Now, commands are classes exported with `module.exports`. So let's create the class and set `module.exports` to it.

```js
module.exports = class ReplyCommand extends commando.Command {
    constructor(client) {
        super(client, {
            name: 'reply',
            group: 'group1',
            memberName: 'reply',
            description: 'Replies with a Message.',
            examples: [';reply']
        });
    }
```

Don't let this scare you, it's actually very simple.

`name` is the name of the command.  
`group` is the command group it is a part of.  
`memberName` is the name of the command within the group.  
`description` is the help text displayed when the help command is used.  
`examples` is an array of examples on how to use the command.

There are many more properties, but more on those later on. For now, these are the ones we're going to focus on.

#### Creating Your Run Method

The next thing we're going to need is a `run` method. This should go right below the constructor for the command. Inside, let's return a message:

```js
    run(message) {
        return message.say('Hi, I\'m awake!');
    }
};
```

That also closed off our command class' brackets, so yay!

Anyway, as you can see, the `run` method is simply the code you want the bot to run when the command is used. This can be anything you can do in normal discord.js, as commando is simply an extension.

You may have also noticed that I used `message.say` instead of `message.channel.send`. This is commando's magic. Instead of `send`, use `say`. Instead of `sendEmbed`, use `embed`. Instead of `sendCode`, use `code`, you get the idea. The only real exception I can think of is files, which are still `message.channel.sendFile`.

So when all that is done, your file should look like this:

```js
const commando = require('discord.js-commando');

module.exports = class ReplyCommand extends commando.Command {
    constructor(client) {
        super(client, {
            name: 'reply',
            group: 'group1',
            memberName: 'reply',
            description: 'Replies with a Message.',
            examples: [';reply']
        });
    }

    run(message) {
        return message.say('Hi, I\'m awake!');
    }
};
```

Now, fire up the bot as normal and use your command! It should automatically be `<prefix>reply` to use it.

In the next tutorial we'll dive into how to use arguments in your commands! See you then!

