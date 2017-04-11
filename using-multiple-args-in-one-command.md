# Using Multiple Args in One Command

Sometimes you may want to collect more than one piece of content from a message. Well, you're in luck, as Commando makes using multiple Arguments very simple.

Let's create a simple command to send a DM to the user mentioned, and the content of the DM will be the content of the message after the mention.

First, you know the drill, let's create our command class and run method.

```js
const { Command } = require('discord.js-commando');

module.exports = class SayCommand extends Command {
    constructor(client) {
        super(client, {
            name: 'dm',
            group: 'group2',
            memberName: 'dm',
            description: 'Sends a message to the user you mention.',
            examples: [';dm @User Hi there!'],
            args: []
        });    
    }

    run(message, args) {

    }
};
```

Now, let's define our args a little differently. Remember, `args` is just an array of objects.

```js
args: [{
    key: 'user',
    prompt: 'Which user do you want to send the DM to?',
    type: 'user'
},
{
    key: 'content',
    prompt: 'What would you like the content of the message to be?',
    type: 'string'
}]
```

Simple, isn't it? Now, let's make the run method.

```js
run(message, args) {
    const user = args.user;
    const content = args.content;
    return user.send(content);
}
```

See how easy it is? Now, the command has multiple args.

```js
const { Command } = require('discord.js-commando');

module.exports = class SayCommand extends Command {
    constructor(client) {
        super(client, {
            name: 'dm',
            group: 'group2',
            memberName: 'dm',
            description: 'Sends a message to the user you mention.',
            examples: [';dm @User Hi there!'],
            args: [{
                key: 'user',
                prompt: 'Which user do you want to send the DM to?',
                type: 'user'
            },
            {
                key: 'content',
                prompt: 'What would you like the content of the message to be?',
                type: 'string'
            }]
        });    
    }

    run(message, args) {
        const user = args.user;
        const content = args.content;
        return user.send(content);
    }
};
```

Doesn't get much simpler than that.

