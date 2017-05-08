# Checking for User Permissions

In the last chapter we talked about how to check for bot permissions, in this chapter, we're going to be using a `hasPermission` method to check whether or not the user is the owner before using the command.

The `hasPermission` method can be anything you want, as long as it returns `true` or `false`. When it returns `true`, the command will run. When it returns `false`, the user will not be allowed to use the command.

Doing this is quite simple.

```js
hasPermission(msg) {
    return this.client.isOwner(msg.author);
}
```

This will return `false` if the user is not the owner of the bot and `true` if they are.

The `hasPermission` method should be placed separate from the `run` method, like so \(if you wanted your say command to only be usable by the owner\):

```js
const { Command } = require('discord.js-commando');

module.exports = class SayCommand extends Command {
    constructor(client) {
        super(client, {
            name: 'say',
            aliases: ['copycat', 'repeat', 'echo', 'parrot'],
            group: 'group2',
            memberName: 'say',
            description: 'Replies with the text you provide.',
            examples: ['say Hi there!'],
            guildOnly: true,
            args: [
                {
                    key: 'text',
                    prompt: 'What text would you like the bot to say?',
                    type: 'string'
                }
            ]
        });    
    }

    hasPermission(msg) {
        return this.client.isOwner(msg.author);
    }

    run(msg, args) {
        if (msg.channel.type !== 'dm')
            if (!msg.channel.permissionsFor(this.client.user).has('MANAGE_MESSAGES')) 
                return msg.say('Error! I don\'t have permission to Manage Messages!');
        const { text } = args;
        msg.delete();
        return msg.say(`\u180E${text}`);
    }
};
```

Simple.

And remember, it can be anything that returns true or false. For example, if we wanted to check if the user has the Ban Members permission:

```js
hasPermission(msg) {
    return msg.member.hasPermission('BAN_MEMBERS');
}
```

_Anything_ that returns `true` or `false` can be used.

