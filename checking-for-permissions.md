# Client Permissions

Sometimes you're going to have a command and start getting a `Forbidden` error. Why? Well, most likely you don't have permissions in the guild to do something. Commando will automatically check for the Send Messages permission and reroute the command to a DM, but for things like Embed Links or Manage Messages you may want to perform a permission check before using the command. Thankfully, this is quite simple.

Let's grab our say command example from the earlier chapter, as it would fail should the command be used without permissions. We'll start by going into it's `constructor`.

```js
super(client, {
    name: 'say',
    aliases: ['copycat', 'repeat', 'echo', 'parrot'],
    group: 'group2',
    memberName: 'say',
    description: 'Replies with the text you provide.',
    examples: ['say Hi there!'],
    args: [
        {
            key: 'text',
            prompt: 'What text would you like the bot to say?',
            type: 'string'
        }
    ]
});
```

Now, obviously the message delete is going to fail if the command is used without permission to Manage Messages. So, we need to perform a check before the command is run. Thankfully, commando now has a simple and easy way of doing this.

```js
super(client, {
    name: 'say',
    aliases: ['copycat', 'repeat', 'echo', 'parrot'],
    group: 'group2',
    memberName: 'say',
    description: 'Replies with the text you provide.',
    examples: ['say Hi there!'],
    clientPermissions: ['MANAGE_MESSAGES'],
    args: [
        {
            key: 'text',
            prompt: 'What text would you like the bot to say?',
            type: 'string'
        }
    ]
});
```

That's it!

