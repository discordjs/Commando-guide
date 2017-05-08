# Using Aliases in Commands

Aliases are simply different ways to call the same command. They're extremely simple to do.

Let's, once again, grab our say command. Head over to all of the command properties.

```js
super(client, {
    name: 'say',
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
```

Underneath the `name` property, let's place the aliases. We'll set them to copycat, repeat, echo, and parrot.

```js
super(client, {
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
```

Now, you can use `<prefix>say`, `<prefix>copycat`, `<prefix>echo`, etc. and all of them will call our say command.

Also, note that aliases and command names are automatically case insensitive. `say` `SaY` and `sAy` are all valid here. Auto-Aliases are also created for aliases and command names containing a hyphen \(-\). For example, `server-info` will automatically have `serverinfo` as an alias without needing to list it in the aliases. Cool, huh?

