# Unknown Command Response Removal

Sometimes, you may want to remove the \(somewhat annoying\) unknown command response from your bot. Be it Cleverbot or other reason, sometimes you just want it gone, and it's quite simple to remove.

Head over to your `index.js` file and find your `client`. We're going to be adding a new setting here.

```js
const client = new commando.Client({
    commandPrefix: '<Insert Your Prefix Here>',
    owner: '<Insert Your User ID Here>',
    disableEveryone: true
});
```

All you have to do to remove the unknown command response is set `unknownCommandResponse` to `false`.

```js
const client = new commando.Client({
    commandPrefix: '<Insert Your Prefix Here>',
    owner: '<Insert Your User ID Here>',
    disableEveryone: true,
    unknownCommandResponse: false
});
```

And that's all there is to it.

