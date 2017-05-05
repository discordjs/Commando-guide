# Using an async run Method

`async` is a simple way to make your Promise-Powered code look _extremely_ neat. Normally with promises, we would use `.then` to continue running the command after the promise has resolved.

```js
msg.say('Hi').then(message => {
    message.edit('Hello');
});
```

However, `async` can make this much easier to do.

```js
const message = await msg.say('Hi');
message.edit('Hello');
```

Now we've completely dropped the indentation, and our code looks cleaner because of it.

Let's modify our first command, reply, to edit the message after it has been sent, and let's use `async` to do it.

First, mark the `run` method with the `async` keyword.

```js
async run(msg) {
    return msg.say('Hi, I\'m awake!');
}
```

Now, let's edit the message we send from 'Hi, I'm awake!' to 'I want to go to bed.'.

```js
async run(msg) {
    const message = await msg.say('Hi, I\'m awake!');
    return message.edit('I want to go to bed.');
}
```

You can `await` anything that returns a Promise. In other words, anything you can perform a `.then` on can be swapped with `await`. `async` is very useful for making code cleaner, especially if you have lots of Promises you're performing `.then` on.

In the end, our Reply command looks like this:

```js
const { Command } = require('discord.js-commando')

module.exports = class ReplyCommand extends Command {
    constructor(client) {
        super(client, {
            name: 'reply',
            group: 'group1',
            memberName: 'reply',
            description: 'Replies with a Message.'
        });
    }

    async run(msg) {
        const message = await msg.say('Hi, I\'m awake!');
        return message.edit('I want to go to bed.');
    }
};
```

Now just remember, don't use `async` for everything.

