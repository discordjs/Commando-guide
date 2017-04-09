# Using Client Values in a Command

This one is easy. Say you wanted to use a client value in your command, for example, you wanted to get the amount of guilds the bot was in. Normally, you'd do this:

```js
client.guilds.size
```

However, in Commando, you have to use `this` to get these values.

```js
this.client.guilds.size
```

That's all there is to it.

