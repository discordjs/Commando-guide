# Adding More Command Groups

Before we make our new argument-powered command, I think we should place it within it's own command group. Then, we can have multiple commands sorted separately in our help command and folder structure.

First, head on over to our `index.js` file and find where we registered our commands.

```js
client.registry
    .registerDefaultTypes()
    .registerGroups([
        ['group1', 'Our First Command Group']
    ])
    .registerDefaultGroups()
    .registerDefaultCommands()
    .registerCommandsIn(path.join(__dirname, 'commands'));
```

Place a `,` after our `group1` and add another group called `group2`.

```js
client.registry
    .registerDefaultTypes()
    .registerGroups([
        ['group1', 'Our First Command Group'],
        ['group2', 'Our Second Command Group']
    ])
    .registerDefaultGroups()
    .registerDefaultCommands()
    .registerCommandsIn(path.join(__dirname, 'commands'));
```

You can add as many of these as you want. 

The next step is to create another folder in your `commands` folder, called `group2`, just like with our `group1` folder.

And there you go, another command group for our new command! 

