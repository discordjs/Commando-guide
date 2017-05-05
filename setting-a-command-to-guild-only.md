# Setting a Command to Guild Only

You may have noticed that should you use your say command in a DM, you are going to get a `Forbidden` error due to attempting to delete a message from the other user in DM. One easy way around this? Setting the command to guild only!

First, let's go into your say command's file and find our command data.

```js
super(client, {
    name: 'say',
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

After `examples` \(though it can be anywhere in this section\) let's add a `guildOnly` setting and set it to `true`.

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

And that's all there is to it! Now, when used in a DM, the bot will not permit the command to be used, and you will no longer receive errors... Unless the bot doesn't have permissions in the guild. But more on that in the next chapter.

