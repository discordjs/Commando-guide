# Client Permissions

Sometimes you're going to have a command and start getting a `Forbidden` error. Why? Well, most likely you don't have permissions in the guild to do something. Commando will automatically check for the Send Messages permission and reroute the command to a DM, but for things like Embed Links or Manage Messages you may want to perform a permission check before using the command. Thankfully, this is quite simple.

Let's grab our say command example from the earlier chapter, as it would fail should the command be used without permissions. We'll start by going into it's `run` method.

```js
run(msg, args) {
    const { text } = args;
    msg.delete();
    return msg.say(`\u180E${text}`);
}
```

Now, obviously the message delete is going to fail if the command is used without permission to Manage Messages. So, we need to perform a check before the command is run. We're also going to set this check to only run if the channel is not a DM, as in DM we do not need to check for permissions and it will error if we do.

```js
if (msg.channel.type !== 'dm')
    if (!msg.channel.permissionsFor(this.client.user).has('MANAGE_MESSAGES'))
        return msg.say('Error! I don\'t have permission to Manage Messages!');
```

Yeah, it's a little long, but this will prevent those pesky errors from popping up if the bot doesn't have permission to do something.

Place it in your `run` as the first thing done.

```js
run(msg, args) {
    if (msg.channel.type !== 'dm')
        if (!msg.channel.permissionsFor(this.client.user).has('MANAGE_MESSAGES'))
            return msg.say('Error! I don\'t have permission to Manage Messages!');
    const { text } = args;
    msg.delete();
    return msg.say(`\u180E${text}`);
}
```

Easy enough.

