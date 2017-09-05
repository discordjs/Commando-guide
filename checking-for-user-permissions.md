# User Permissions

In the last chapter we talked about how to check for bot permissions, in this chapter, we're going to be using a `hasPermission` method and the `userPermissions` option to check whether or not the user is the owner or has a certain permission before using the command.

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
        const { text } = args;
        msg.delete();
        return msg.say(text);
    }
};
```

Simple.

You can also return a string for a custom response.

```js
hasPermission(msg) {
    if (!this.client.isOwner(msg.author)) return 'Only the bot owner(s) may use this command.';
    return true;
}
```

Neat, huh?

Another thing you might want to do is check for specific user permissions, such as if a user has permissions in the current channel to manage messages. We can do that even more simply with the `userPermissions` option.

```js
super(client, {
    name: 'say',
    aliases: ['copycat', 'repeat', 'echo', 'parrot'],
    group: 'group2',
    memberName: 'say',
    description: 'Replies with the text you provide.',
    examples: ['say Hi there!'],
    userPermissions: ['MANAGE_MESSAGES'],
    args: [
        {
            key: 'text',
            prompt: 'What text would you like the bot to say?',
            type: 'string'
        }
    ]
});
```

Just like `clientPermissions`.

