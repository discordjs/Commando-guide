# Using Args in Commands

Sometimes when using commands we may want to get data from our user to narrow down the command further. In this section we'll create a command that pulls a string from the message and says it back to the user.

A `string` argument is simply the text after the command name and prefix. For example, `!say Hi there!` would cause our arg to be `Hi there!`. It's quite simple to create one. For our example, we'll be making the aforementioned say command.

First, go into your `group2` folder and make a new file called `say.js`. You know the drill. Once you have it, set up your command class and everything just like the one in our reply command.

```js
const commando = require('discord.js-commando');

module.exports = class SayCommand extends commando.Command {
    constructor(client) {
        super(client, {
            name: 'say',
            group: 'group2',
            memberName: 'say',
            description: 'Replies with the text you provide.',
            examples: [';say Hi there!']
        });
    }

    run(message) {

    }
};
```

Place a `,` after the `examples` field, we're going to be adding an `args` field.

The `args` field is simply an array of objects, each containing data for that argument.

```js
super(client, {
    name: 'say',
    group: 'group2',
    memberName: 'say',
    description: 'Replies with the text you provide.',
    examples: [';say Hi there!'],
    args: [{
        key: 'text',
        prompt: 'What text would you like the bot to say?',
        type: 'string'
    }]
});
```

See? Simple.

`key` is the name of the argument, when you define it in your `run` method, this is what we'll be using.  
`prompt` is the text that displays if no argument is provided. For example: someone just uses `<prefix>say`. That prompt will come up asking for the text.  
`type` is the type the argument is a part of. This can be many things, including `string`, `integer`, `user`, `member`, you get the idea. We'll go over more of these later.

Now, head on over to your `run` method and, firstly, define args and set our `text` arg to a variable.

```js
run(message, args) {
    const text = args.text;
}
```

Next, let's make the `run` method return the message.

```js
run(message, args) {
    const text = args.text;
    return message.say(text);
}
```

Let's also make it delete our original message before saying it.

```js
run(message, args) {
    const text = args.text;
    message.delete();
    return message.say(text);
}
```

And there we have it, a say command using args! Let's spruce it up a little with a Zero-Width Space.

```js
const commando = require('discord.js-commando');

module.exports = class SayCommand extends commando.Command {
    constructor(client) {
        super(client, {
            name: 'say',
            group: 'group2',
            memberName: 'say',
            description: 'Replies with the text you provide.',
            examples: [';say Hi there!'],
            args: [{
                key: 'text',
                prompt: 'What text would you like the bot to say?',
                type: 'string'
            }]
        });    
    }

    run(message, args) {
        const text = args.text;
        message.delete();
        return message.say(`\u180E${text}`);
    }
};
```

And now we're done!

