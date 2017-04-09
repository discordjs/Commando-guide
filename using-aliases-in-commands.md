# Using Aliases in Commands

Aliases are simply different ways to call the same command. They're extremely simple to do.

Let's, once again, grab our say command. Head over to all of the command properties.

```js
super(Client, {
    name: 'say',
    group: 'group2',
    memberName: 'say',
    description: 'Replies with the text you provide.',
    examples: [';say Hi there!'],
    guildOnly: true,
    args: [{
        key: 'text',
        prompt: 'What text would you like the bot to say?',
        type: 'string'
    }]
});
```

Underneath the `name` property, let's place the aliases. We'll set them to copycat, repeat, echo, and parrot.

```js
super(Client, {
    name: 'say',
    aliases: [
        'copycat',
        'repeat',
        'echo',
        'parrot'
    ],
    group: 'group2',
    memberName: 'say',
    description: 'Replies with the text you provide.',
    examples: [';say Hi there!'],
    guildOnly: true,
    args: [{
        key: 'text',
        prompt: 'What text would you like the bot to say?',
        type: 'string'
    }]
});
```

Now, you can use `<prefix>say`, `<prefix>copycat`, `<prefix>echo`, etc. and all of them will call our say command.

