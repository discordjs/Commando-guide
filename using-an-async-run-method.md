# Using an async run Method

`async` is a simple way to make your Promise-Powered code look _extremely_ neat. Normally with promises, we would use `.then` to continue running the command after the promise has resolved.

```js
message.say('Hi').then(msg => {
    msg.edit('Hello');
});
```

However, `async` can make this much easier to do.

```js
const msg = await message.say('Hi');
msg.edit('Hello');
```

Now we've completely dropped the indentation, and our code looks cleaner because of it.

Let's modify our first command, reply, to edit the message after it has been sent, and let's use `async` to do it.

First, mark the `run` method with the `async` keyword.

```js
const commando = require('discord.js-commando');

module.exports = class ReplyCommand extends commando.Command {
    constructor(Client) {
        super(Client, {
            name: 'reply',
            group: 'group1',
            memberName: 'reply',
            description: 'Replies with a Message.',
            examples: [';reply']
        });
    }

    async run(message) {
        return message.say('Hi, I\'m awake!');
    }
};
```

Now, let's edit the message we send from 'Hi, I'm awake!' to 'I want to go to bed.'.

```js
async run(message) {
    const msg = await message.say('Hi, I\'m awake!');
    return msg.edit('I want to go to bed.');
}
```

You can `await` anything that returns a Promise. In other words, anything you can perform a `.then` on can be swapped with `await`. `async` is very useful for making code cleaner, especially if you have lots of Promises you're performing `.then` on.

In the end, our Reply command looks like this:

```js
const commando = require('discord.js-commando');

module.exports = class ReplyCommand extends commando.Command {
    constructor(Client) {
        super(Client, {
            name: 'reply',
            group: 'group1',
            memberName: 'reply',
            description: 'Replies with a Message.',
            examples: [';reply']
        });
    }

    async run(message) {
        const msg = await message.say('Hi, I\'m awake!');
        return msg.edit('I want to go to bed.');
    }
};
```

Now just remember, don't use `async` for everything.

